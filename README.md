# ANZ Tech Hub - Getting Started with Full-Stack Application Development on SAP BTP.

## Description

This repository contains the material for the SAP TechHub session: Getting Started with Full-Stack Application Development on SAP BTP with the Cloud Application Programming model.  

## Overview

The goal of this hands-on tutorial is to help developers implementing business applications on SAP BTP including the integration with the SAP cloud suite. 
This session introduces attendees to...

- Building a CAP application with a SAP Fiori Elements UI app
- Adding custom logic, local launchpad, authorization and tests for local development
- Deploying the application to BTP Cloud Foundry environment
- [Optional] Remote Service Integration (connect to an API from S/4HANA)
- [Optional] Replication of data from remote service
- [Optional] Create a pre-built integration package for the remote service

With tips and tricks along the way.

## Requirements

The requirements to follow the exercises in this repository are...
- You have an [enterprise global account](https://help.sap.com/docs/btp/sap-business-technology-platform/getting-global-account#loiod61c2819034b48e68145c45c36acba6e) in SAP BTP. To use services for free, you can sign up for a CPEA (Cloud Platform Enterprise Agreement) or a Pay-As-You-Go for SAP BTP global account and make use of the free tier services only. See [Using Free Service Plans](https://help.sap.com/docs/btp/sap-business-technology-platform/using-free-service-plans?version=Cloud).
- You have an S-user or P-user. See [User and Member Management](https://help.sap.com/docs/btp/sap-business-technology-platform/user-and-member-management).
- You are an administrator of the global account in SAP BTP.
- You have a subaccount in SAP BTP to deploy the services and applications.
    > See this [tutorial](https://developers.sap.com/tutorials/prepare-btp-cf.html) for preparing SAP BTP (create subaccount and add entitlements).
    > If you provide your own subaccount or use a free trial account there is no need to suffix object names with your userid (`<xxx>`).

    > Access an [existing BTP trial account](https://cockpit.hanatrial.ondemand.com/cockpit#/home/trial) or create a [new BTP trial account](https://cockpit.hanatrial.ondemand.com/cockpit#/home/trial). __For a trial account: Please choose either the US or EU region for your subaccount to ensure all required service entitlements are available in the trial account__.


- You have one of the following browsers that are supported for working in SAP Business Application Studio:
    - Mozilla Firefox
    - Google Chrome
    - Microsoft Edge
- You have a running instance of SAP HANA Cloud and SAP Work Zone Standard.
    > See this [tutorial](https://developers.sap.com/mission.hana-cloud-database-get-started.html) for preparing a SAP HANA Cloud instance.
    > See this [tutorial](https://developers.sap.com/group.launchpad-cf-create-site.html) for subscribing to SAP Build Work Zone, Standard Edition.

- You have a running instance of SAP Business Application Studio with a __Full Stack Cloud Application__ dev space. See this [tutorial](https://developers.sap.com/tutorials/appstudio-onboarding.html) on setting up Business Application Studio (_it is already setup on trial accounts_).
    > You can also use vscode as the code editor. See this [tutorial](https://developers.sap.com/tutorials/btp-app-prepare-dev-environment-cap.html) to setup your local machine.

> Note: When using BAS from a BTP trial account it is not considered to be within the BTP IP address range so when setting up your HANA Cloud instance you need to allow connections from anywhere!

> Map HANA Cloud instance to your CF org and space.
> This can be done by editing the HANA Cloud configuration in the HANA tools app.
> Find the org id with `cf org <org-name> --guid`
> Find the space id with `cf space <space-name> --guid`.

<!-- Assign Entitlements start -->

### Configure the entitlements

**Prerequisite:** You must have an administrator role for SAP BTP.

To deploy the Incident Management applications, you need the following entitlements:

| Service     |      Plan      |  Quota required |
| ------------- | :-----------: | ----: |
| Cloud Foundry runtime | MEMORY |   1  |
| SAP Build Work Zone, standard edition    |  standard (Application) |   1 |
| SAP HANA Cloud |   hana | 1  |
| SAP HANA Cloud |   tools (Application)   |   1 |
| SAP HANA Schemas & HDI Containers | hdi-shared | 1 |
| SAP Application Logging Service | standard/lite | 1  |
| SAP Business Application Studio | standard-edition (application) | 1 |

## Exercises

- [Exercise 1: Introduction to Application Development Using CAP](./exercises/Introduction%20to%20Application%20Development%20Using%20CAP/README.md)
- [Exercise 2: Build a CAP Application](./exercises/Build%20a%20CAP%20Application/README.md)
- [Exercise 3: Add Fiori Elements UIs](./exercises/Add%20Fiori%20Elements%20UIs/README.md)
- [Exercise 4: Add Custom Logic](./exercises/Add%20Custom%20Logic/README.md)
- [Exercise 5: Use a Local Launch Page](./exercises/Use%20a%20Local%20Launch%20Page/README.md)
- [Exercise 6: Add Authorization](./exercises/Add%20Authorization/README.md)
- [Exercise 7: Add Test Cases](./exercises/Add%20Test%20Cases/README.md)
- [Exercise 8: Deploy in SAP BTP, Cloud Foundry Runtime](./exercises/Deploy%20in%20SAP%20BTP,%20Cloud%20Foundry%20Runtime/README.md)
- [Exercise 9: Integrate Your Application with SAP Build Work Zone, Standard Edition](./exercises/Integrate%20Your%20Application%20with%20SAP%20Build%20Work%20Zone,%20Standard%20Edition/README.md)
- [Exercise 10: Logging, Tuning & Hybrid Development](./exercises/Hybrid%20Development/README.md)
- [Exercise 11: OPTIONAL - Implement Remote Service Connectivity](./exercises/Implement%20Remote%20Service%20Connectivity/README.md)
- [Exercise 12: OPTIONAL - Enable Replication for the Remote Entity](./exercises/Enable%20Replication/README.md)
- [Exercise 13: OPTIONAL - Creating Prebuilt Integration Packages for Reuse](./exercises/Prebuilt%20Integration%20Packages/README.md)
- [Further reading and tutorials](./exercises/Further%20Reading/README.md)

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
