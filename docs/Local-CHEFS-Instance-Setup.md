[Home](index) > [Developer](Developer) > [Contributors](Contributors) > **Local CHEFS Instance Setup**
***

This document will help developers looking to install CHEFS on their local machines for testing and development. Following this documentation will set up an isolated sandbox CHEFS instance for investigation and research prior to preparing pull requests or code commits. 

**On this page:**
* [Prerequisites](#prerequisites)
* [Setup](#setup)
* [Build](#build)


# Prerequisites
<!-- **[Back to top](#top)** -->

Node v16. You can't go any higher than this as some of the dependencies rely on an older OpenSSL routine which is only available in Node v16. If you try running it with a higher version of Node (e.g. node 20.x) you will get  
```    
Error: error:0308010C:digital envelopes routines::unsupported  
... //details removed
opensslErrorStack: [ 'error:03000086:digital envelopes routines::unsupported' ],  
library: 'digital envelope routines',  
reason: 'unsupported',  
code: 'ERR_OSSL_EVP_UNSUPPORTED'
```  
> Possible resolution can be achieved by setting the env variable in the developer's shell.    
The command to run is  ``` export NODE_OPTIONS=--openssl-legacy-provider ```

An IDIR account is required to access CHEFS. 

Request an SSO Integration from the [Common Hosted Single Sign-on (CSS)](https://bcgov.github.io/sso-requests) page in order to obtain a resource and secret that will be used for authentication when building CHEFS. View the [detailed documentation](https://github.com/bcgov/common-hosted-form-service/wiki/Pathfinder-SSO-client) about requesting the Pathfinder SSO integration. 

Ensure that [Docker](https://www.docker.com/get-started/) is installed on your local machine. Using Docker allows for a quick CHEFS build on your local machine however this is not how the production environment is hosted. 

# Setup
<!-- **[Back to top](#top)** -->

Start by cloning the [CHEFS source code](https://github.com/bcgov/common-hosted-form-service) onto your local machine and download `build_package.zip` linked below.

[build_package.zip](https://github.com/bcgov/common-hosted-form-service/files/11479953/build_package.zip)

Unzip the file and move the `local.json` file such that the CHEFS directory structure follows `/common-hosted-form-service/app/config/local.json`. The `chefs_build` directory contains the directory structure and docker file for building CHEFS.

Open `realm-export.json`  located at `chefs_build/docker/imports/keycloak` and search for `XXXXXXXXXXXX`. This value must match the `clientSecret` value in `local.json` so that the CHEFS API can connect to your Keycloak instance. By default, these are set to be equal and don’t need to be altered.

Navigate to the [CSS](https://bcgov.github.io/sso-requests) page, log in with your IDIR, and download the ‘Development’ Installation JSON from your SSO Integration. 

Back in the `realm-export.json` file, search for `YYYYYYYYYYYY` and replace it with the resource you obtained from the downloaded JSON file. Search for `ZZZZZZZZZZZZ` and replace it with the secret. 

All the files are now configured and you can run Keycloak and PostgreSQL. 

Note that realm-export.json is configured with the SSO integration for the “Development” environment, and will only work with the resource and secret from the Development JSON. 

# Build
<!-- **[Back to top](#top)** -->

Start Docker, open a terminal in the `/chefs_build` directory, and run the following command:

    docker compose up

This will start up an instance for your Keycloak and PostgreSQL containers. If you don’t want to keep the terminal open, you can append a -d to the end of the command above.

Next, open a terminal in the directory `/common-hosted-form-service/app` and run the following commands:

    npm install
    npm run migrate
    npm run seed:run
    npm run serve

This will start the process for the CHEFS API.

Open another terminal in the directory `/common-hosted-form-service/app/frontend` and run the following commands:

    npm install
    npm run serve

This will start the process for the CHEFS front end.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)