# Further Reading and Tutorials

## Use real systems for remote services

We have covered a lot in the previous exercises. Enough to get you going from scratch with building production quality cloud applications on SAP BTP.

Throughout the tutorials we used the [SAP Business Accelerator Hub](api.sap.com)

> The Business Accelerator Hub was previously known as the API Business Hub. Its API's are directly available from within the Service Center panel in BAS.

The Business Accelerator Hub provides a sandbox service for testing SAP's API's.

The following tutorials will show you how to switch from the sandbox to a real business system with very little effort.

1. __S/4HANA Public Cloud__ - [Consume Remote Services from SAP S/4HANA Public Cloud](https://developers.sap.com/mission.btp-consume-external-service-cap.html)

2. __S/4HANA Private Cloud / On-premise__ - [Consume Remote Services from SAP S/4HANA (on-prem)](https://developers.sap.com/mission.btp-consume-external-service-s4hana-cap.html)

3. For other systems see [Extending business systems with SAP BTP](https://help.sap.com/docs/btp/sap-business-technology-platform/btp-extensions) in the SAP Help.

## CAP in Java

[Tutorial on building CAP services in Java - including reuse services](https://developers.sap.com/mission.cap-java-app.html)

## CI/CD

Evidence shows that getting new software in front of the users as quickly as possible and iterating on it leads to better outcomes. Devops is a series of practices to help enable this and a core part of it is CI/CD.

CI/CD automates the testing, integration and deployment of your code.

> As a developer, you will start a new project and as you build it out and make changes requested by users you will likely be testing locally yourself. But there will come a time when you start making changes; pushing to prod; and finding out that you broke something else. This is why you need automated testing. It gives you - the developer - reassurance.

SAP BTP includes the [SAP Continuous Integration and Delivery service](https://discovery-center.cloud.sap/serviceCatalog/continuous-integration--delivery?region=all) that is ready to go with very minimal configuration and allows you to run your automated tests; validate the code (linting) and also deploy to BTP subaccounts.

The service can pickup changes to your code from the git repository and automatically run the CI/CD pipeline. Developers can receive notifications of success/failure.

[Tutorial to use CI/CD with your CAP project](https://developers.sap.com/tutorials/cicd-start-cap.html).

## Fiori Elements

[Detailed FE tutorial with custom pages and extensions](https://github.com/SAP-samples/teched2023-DT262)

## SAP BTP Runtimes

Throughout these exercises we have been using the SAP BTP Cloud Foundry environment to deploy our CAP service. Note that we can also use a managed Kubernetes environment with the SAP BTP Kyma runtime.

[CAP deployment guidelines](https://cap.cloud.sap/docs/guides/deployment/)

CAP provides support for Kyma deployments via Helm (`cds add helm`). See this [tutorial](https://developers.sap.com/mission.btp-deploy-cap-kyma.html) for a how-to on deploying CAP services to Kyma.

## Modularisation

We've seen within these exercises how we could easily modularise our business partner remote service into a separate npm module that can be used in other projects. In this case the code is included into our project at build time (`node_modules`).

We can also modularise across completely separate CAP projects and even in different SAP BTP subaccounts. For example, with our incidents app, we may want to add an Equipment field. `Equipment` could be provided by a different CAP service built by another developer. We can use the same technique we use here with business partners to call this other CAP service to get the equipment and the projects managed separately. This is a way to create reuse services.

> Authorization can be via principal propagation or technical user.

Another possibility is with the database, SAP HANA Cloud. Each CAP project uses an `hdi container` on SAP HANA Cloud. HDI Containers are separate schema's so that one cannot talk to the other in any way.
However, with the use of synonyms and authorisations we can allow cross-hdi container access. See this blog post on [how to share tables across different cap projects](https://blogs.sap.com/2021/10/03/how-to-share-tables-across-different-cap-projects/).

> It is recommended to take an **API-first** approach for better decoupling and not to jump into cross-hdi-container access unless necessary for your circumstances.

## CDS REPL / CDS Notebooks

You can experiment and test with CDS using a REPL or Notebooks. This is a handy way to experiment with and fine-tune your data queries when building a CAP app. For example:

Enter a CDS repl with:

```
cds r
```

Once in the repl, load the data model with:

```
cds.test()
```

Now you can run CQL (CDS Query Language) on your data model, e.g.:

```
var { ProcessorService } = cds.services
await SELECT.from(`ProcessorService.Customers`).limit(2)
```

> Excellent blog post on [understanding cql queries](https://blogs.sap.com/2023/05/15/sapcap-understanding-cql-queries-node.js/).


## Typescript

Typescript is fully supported and recommended for SAPUI5 and CAP.

When using the Fiori Application Generator (from the Template Wizards page in BAS) there is an option under __advanced settings__ where you can enable Typescript for your fiori app.

See [here](https://cap.cloud.sap/docs/node.js/typescript#enable-typescript-support) for for full Typescript support in CAP.

CAP (`@sap/cds`) comes with Typescript types (built-in) but there is an additional package that can be user to automatically add types to your own entities - [cds typer](https://cap.cloud.sap/docs/tools/cds-typer#cds-typer-vscode). **cds typer** can even be used when not creating a full-blown typescript cap project.
> Add types with `cds add typer`

## Cloud ALM

A tutorial to take your through the process of instrumenting your BTP application for monitoring nby SAP Cloud ALM (Health Checks and Real User Monitoring): [Observability for your SAP BTP applications with SAP Cloud ALM](https://github.com/SAP-samples/teched2023-XP261).

# Undeploy your app from SAP BTP

You can undeploy your app and all its services by running the following:

```bash
cf undeploy incident-management-<xxx> --delete-service-keys --delete-services
```

__This will leave the BTP backing services still running (HANA Cloud, Work Zone).__

> You can see what MTAs have already been deployed with this cloud foundry cli command:
```
cf mtas
```

