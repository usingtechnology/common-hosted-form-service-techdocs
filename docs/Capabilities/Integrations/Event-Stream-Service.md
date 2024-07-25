[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **CHEFS Event Stream Service** 
***  
# CHEFS Event Stream Service

**NOTE (July 25, 2024) - this is in active development and not yet released. This documentation will be updated as development progresses.**

CHEFS is adding an Event Streaming Service which allows Form Owners to consume and process real-time data about the forms (ex. a new version of the form has been published) and submissions. 

Currently, Form Owners can configure event notifications via webhook (see [Event Subscription](./Event-Subscription.md)). These events are elementary, with metadata providing the IDs and event types. Generally, once the event notification is received the external application/service calls back to CHEFS via the CHEFS API to retrieve the full event data (form schema, submission data). This approach works but unnecessarily loads the CHEFS API service, degrading performance for all forms. More significantly, the logic for when and why an event is fired is directly coded into CHEFS. This is unsustainable as each external application may have different requirements for why an event is fired - a callback to CHEFS API is needed to determine if the event should be processed. 

Moving forward, CHEFS will fire events (with encrypted payloads) and allow the consumers to define the logic for processing on their end. An Event Streaming Service allows multiple consumers to process the same event. For instance, the Form Owner can process the submission data, while a metrics reporter can add a count to their submissions totals, another service can analyze service loads by sector.

This initial phase will introduce the Event Streaming Service as a component of CHEFS with the intention that this component grows, matures and becomes a Common Component.

## nats.io
[NATS](https://nats.io) is a connective technology built for the ever increasingly hyper-connected world. It is a single technology that enables applications to securely communicate across any combination of cloud vendors, on-premise, edge, web and mobile, and devices. NATS consists of a family of open source products that are tightly integrated but can be deployed easily and independently. NATS is being used globally by thousands of companies, spanning use-cases including microservices, edge computing, mobile, IoT and can be used to augment or replace traditional messaging.

NATS has been used successfully by many other projects within BC Government. It can be scaled horizontally and runs without the need for a paid operator (i.e. [Kafka](https://kafka.apache.org)). 

NATS has official clients in multiple mainstream languages so Form Owners shouldn't have to adopt a new language to write their event consumers.

### Event Stream
The CHEFS Event Stream is implemented as a [NATS JetStream](https://docs.nats.io/nats-concepts/jetstream). 

JetStream offers many benefits over a traditional publisher/subscriber relationship: replay policies, durability, bulk handling, starting from a specific sequence, and starting from a specific date.

As a stream producer we can set retention limits such as maximum message age, and maximum number of messages in the stream.


### Consumers
NATS allows a variety of consumer types and this is required reading: [JetStream Consumers](https://docs.nats.io/nats-concepts/jetstream/consumers).



## CHEFS Stream

CHEFS will publish events to a stream named: `CHEFS`.

Under this stream will be two major subject prefixes: 

1. `PUBLIC.forms`
2. `PRIVATE.forms`


Consumers specify which subjects they wish to process and often use wildcards. For example: a consumer can specify `PUBLIC.forms.>` and `PRIVATE.forms.submissions.>`. This would consume ALL public forms events and only private submission events.

`PUBLIC.forms` can be consumed by any client. These events will contain only metadata and no personal/private information. 

`PRIVATE.forms` can be consumed by any client but not fully understood. The payloads of these events will contain encrypted data. Only known and approved clients will have the key to decrypt the private information (ex. a form submission).

`PRIVATE.forms` events will generally be a superset of the `PUBLIC.forms` events with the extra encrypted information in the payloads. As the system evolves there may be more types of `PUBLIC.forms` events that contain different types of metadata (ex. for metrics on Ministry or whether form is API enabled, etc.).

### Events

As stated, the two major subjects are `PUBLIC.forms` and `PRIVATE.forms`; these will be further specified as follows:

`PUBLIC|PRIVATE.<domain>.<class>.<type>.<form id>`

- domain = `forms`
- class = `schema` or `submission`.
- type = `created`, `deleted`, `modified` and more
- form id = the id of the form firing these events


Using wildcards a consumer could listen for events on a specific form id or a specific type (i.e. only listen to submission created events across any form).


- `PUBLIC.forms.schema.published.<form id>`
- `PUBLIC.forms.schema.unpublished.<form id>`
- `PUBLIC.forms.submission.created.<form id>`
- `PUBLIC.forms.submission.modified.<form id>`
- `PUBLIC.forms.submission.deleted.<form id>`

More events to come.

### Event Metadata
The event metadata contains data from the subject (domain, class, type, form id) which will allow subject specific processing if the consumer/listener/subscriber is using wildcard subjects.

Other metadata will be provided as needed per type and only if the data is *NOT* considered private.

| Attribute | Notes |
| --- | --- |
| `source` | `chefs` - where did this event originate? |
| `domain` | `forms` - top level classification for event |
| `class` | `submission` or `schema` - secondary classification for event |
| `type` | `created`, `deleted`, `modified` - tertiary classification for event |
| `formId` | uuid - CHEFS form id . Form that originates the event |
| `formVersionId` | uuid - CHEFS form version id. Only if value exists at time of event. |
| `submissionId` | uuid - CHEFS submission id. Only applies for `submission` class events. |
| `draft` | boolean - For `submission` class events, the submission.draft value |

An example to show the overall structure of an event message is: 

```json
{
  meta: {
    source: 'chefs',
    domain: 'forms',
    class: 'submission'
    type: 'modified',
    formId: <uuid>,
    formVersionId: <uuid>,
    submissionId: <uuid>,
    draft: false,
  },
  payload: {
    data: <encrypted>
  }

```

### NATS Message Metadata

nats messages contain very valuable metadata that consumers should leverage for optimal processing. Each message on the stream will have a [sequence number](https://github.com/nats-io/nats.docs/blob/803d660c33496c9b7ba42360945be58621bbba0b/nats-concepts/seq_num.md) and a timestamp. Consumers can schedule batch consumption based on the sequence or timestamp of their last processed event. 

### Example Consumer
The following is a trivialized example of a [pull consumer](https://docs.nats.io/nats-concepts/jetstream/consumers). It is up to the external application that consumes/listens to the events to decide how to set up their consumer. This is one way in one language (JavaScript). Please review the documentation about [consumers](https://docs.nats.io/nats-concepts/jetstream/consumers) and review the approved [examples](https://natsbyexample.com) for more information.

The example will ask for a batch of messages every 5 seconds - illustrating some basic pull behaviour. We can see as it processes the messages that there is a sequence number (`m.seq`) and a timestamp (`m.info.timestampNanos`) which we could leverage for different [delivery policies](https://docs.nats.io/nats-concepts/jetstream/consumers#deliverpolicy) such as get all messages since X sequence number.

**Do not use this code for your client! Simplified example only!**

```js
const { AckPolicy, connect } = require("nats");

// connection info
const servers = ["localhost:4222", "localhost:4223", "localhost:4224"];

let nc = undefined; // nats connection
let js = undefined; // jet stream
let jsm = undefined; // jet stream manager
let consumer = undefined; // pull consumer (ordered, ephemeral)

// stream info
const STREAM_NAME = "CHEFS";
const FILTER_SUBJECTS = ["PUBLIC.forms.>", "PRIVATE.forms.>"];
const MAX_MESSAGES = 2;
const DURABLE_NAME = "pullConsumer";

const printMsg = (m) => {
  // illustrate grabbing the sequence and timestamp from the nats message...
  try {
    const ts = new Date(m.info.timestampNanos / 1000000).toISOString();
    console.log(
      `msg seq: ${m.seq}, subject: ${m.subject}, timestamp: ${ts}, streamSequence: ${m.info.streamSequence}, deliverySequence: ${m.info.deliverySequence}`
    );
    // illustrate (one way of) grabbing message content as json
    console.log(JSON.stringify(m.json(), null, 2));
  } catch (e) {
    console.error(`Error printing message: ${e.message}`);
  }
};

const init = async () => {
  if (nc && nc.info != undefined) {
    // already connected.
    return;
  } else {
    // open a connection...
    try {
      // no credentials provided.
      // anonymous connections have read access to the stream
      console.log(`connect to nats server(s) ${servers} as 'anonymous'...`);
      nc = await connect({
        servers: servers,
      });

      console.log("access jetstream...");
      js = nc.jetstream();
      console.log("get jetstream manager...");
      jsm = await js.jetstreamManager();
      await jsm.consumers.add(STREAM_NAME, {
        ack_policy: AckPolicy.Explicit,
        durable_name: DURABLE_NAME,
      });
      consumer = await js.consumers.get(STREAM_NAME, DURABLE_NAME);
    } catch (e) {
      console.error(e);
      process.exit(0);
    }
  }
};

const pull = async () => {
  console.log("fetch...");
  let iter = await consumer.fetch({
    filterSubjects: FILTER_SUBJECTS,
    max_messages: MAX_MESSAGES,
  });
  for await (const m of iter) {
    printMsg(m);
    m.ack();
  }
};

const main = async () => {
  await init();
  await pull();
  setTimeout(main, 5000); // process a batch every 5 seconds
};

main();

const shutdown = async () => {
  console.log("\nshutdown...");
  console.log("drain connection...");
  await nc.drain();
  process.exit(0);
};

process.on("SIGTERM", shutdown);
process.on("SIGINT", shutdown);
process.on("SIGUSR1", shutdown);
process.on("SIGUSR2", shutdown);
process.on("exit", () => {
  console.log("exit.");
});

```

## Encryption

To securely facilitate transmission of sensitive data between systems, CHEFS will encrypt the payloads for `PRIVATE.forms` events. 

Initially, CHEFS will encrypt the payload using an `aes-256-gcm` that requires a  `sha256` hash as a key (256 bits/32 bytes/64 characters).

CHEFS will use the [cryptr](https://github.com/MauriceButler/cryptr) JavaScript library. External applications are not required to use Node.js/JavaScript but will have to test their own implmentation or library.

The Form Designer will have to `enable` private messages and encryption. CHEFS can generate a key or the Form Designer can provide the key. In either case, only CHEFS and the Form Designer should know the key. The Form Designer should store the key securely and make it accessible to their application/service/system following best practices.

Since the Form Designer can specify the key they can use the same key for all of their forms. This will simplify processing in their systems. Plans for CHEFS include grouping of forms which also alleviates the complexity of mapping 1-to-1 key-to-form.

