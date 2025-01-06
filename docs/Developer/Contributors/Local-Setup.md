[Home](index) > [Developer](Developer) > [Contributors](Contributors) > **Local Setup**
***

This document will help developers looking to install CHEFS on their local machines for testing and development. Following this documentation will set up an isolated sandbox CHEFS instance for investigation and research prior to preparing pull requests or code commits.

<!-- **On this page:**
* [Prerequisites](#prerequisites)
* [Setup](#setup)
* [Build](#build) -->


# Prerequisites
<!-- **[Back to top](#top)** -->

An IDIR account is required to access CHEFS.

Request an SSO Integration from the [Common Hosted Single Sign-on (CSS)](https://bcgov.github.io/sso-requests) page in order to obtain a resource and secret that will be used for authentication when building CHEFS. View the [detailed documentation](Pathfinder-SSO-client) about requesting the Pathfinder SSO integration.

Ensure that [Docker](https://www.docker.com/get-started/) is installed and running on your local machine. Using Docker allows for a quick CHEFS build on your local machine however this is not how the production environment is hosted.

# Setup
<!-- **[Back to top](#top)** -->

Start by cloning the [CHEFS source code](https://github.com/bcgov/common-hosted-form-service) onto your local machine.

CHEFS development takes place using a dev container. Open the cloned report in Visual Studio Code and you will be prompted to build the container.

The `.devcontainers/chefs_local` directory contains the `local.json` file for running CHEFS.

> Note: Previously local development used a Keycloak container for auth. While this container and its configuration still exist, local development is configured to use the dev SSO environment. This may change in the future to use the Keycloak container and allow CHEFS to run without the BC Gov SSO.

# Running CHEFS
<!-- **[Back to top](#top)** -->

In the sidebar select the `Build and Debug` item and in the dropdown menu select `CHEFS` and click the green arrow. This will start the API and the frontend.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
