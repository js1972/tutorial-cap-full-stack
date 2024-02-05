# Exercise 13 - OPTIONAL - Creating Prebuilt Integration Packages for Reuse

In this exercise, you will see how we can convert our use of the Business Partner remote API into an integration package which can be embedded into an application. The goal is to make reusable code available for others, to let them benefit from prefabricated integrations.

## Build

Create a new `npm` package outside of our incident management project.

```bash
cd ..    # go to the projects folder which is above the incidents app
mkdir s4-bupa-integration
cd s4-bupa-integration
npm init -y
```

Then copy the contents of the `srv/external` folder (from the incidents app) to a `bupa` folder here:

```bash
cp -r ../incident-management-<xxx>/srv/external/ bupa
```

Use `npm pack` to preview the content of the package:

```bash
npm pack
```
Which outputs:

```
npm notice 
npm notice 📦  s4-bupa-integration@1.0.0
npm notice === Tarball Contents === 
npm notice 152.2kB bupa/BusinessPartnerA2X.cds                       
npm notice 327B    bupa/BusinessPartnerA2X.js                        
npm notice 634.4kB bupa/BusinessPartnerA2X.xml                       
npm notice 107B    bupa/data/BusinessPartnerA2X-A_BusinessPartner.csv
npm notice 748B    bupa/index.cds                                    
npm notice 237B    package.json                                      
npm notice === Tarball Details === 
npm notice name:          s4-bupa-integration                 
npm notice version:       1.0.0                                   
npm notice filename:      s4-bupa-integration-1.0.0.tgz       
npm notice package size:  58.0 kB                                 
npm notice unpacked size: 788.0 kB                                
npm notice shasum:        b47fc7c0dc49ed39b417aadabb55ef6fe8ec86d6
npm notice integrity:     sha512-cHiWiQVLWRLyZ[...]umfYPVVIo4QSg==
npm notice total files:   6                                       
npm notice 
s4-bupa-integration-1.0.0.tgz
```

You see that NPM has nicely packaged all your content.

> You can influence what gets packaged with the [files field in package.json](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#files) or an `.npmignore` file.

## Publish

There are different options to make the package available for usage in applications:

- Via [npmjs.com](https://www.npmjs.com/): this is the preferred way for free usage by anyone. It requires an NPM account. See the [NPM docs](https://docs.npmjs.com/cli/v8/commands/npm-publish) for more.
- Via GitHub: just push the package sources to a repository on github.com, and you can refer to the package with a `git+https://github.com/...` URL during `npm install`. You can even refer to a specific branch of the repository.
- Via a `tgz` file like the one you built above. This doesn't need to be stored locally, but can also be served by a remote host.
- Via a local folder

> See the [NPM docs](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#urls-as-dependencies) for more details.

For this tutorial, we use the _local folder_ approach, as it's the most convenient for fast development roundtrips. Also, it doesn't require you to use a GitHub or an NPM account.

> Note though, that for basic cloud deployments local folders won't work. There, you need to have publicly accessible hosts for your packages, like npmjs.com or github.com, so that NPM can download the packages during deployment.
    This restriction can in turn be mitigated by vendoring, i.e. including your packages in deployment archives (like SAP's multi-target archive format MTA). This is beyond the scope of this tutorial, though.

## Install

Go back to the incidents application and install the folder like any other NPM dependency:

```bash
cd ../incident-management-<xxx>
npm add ../s4-bupa-integration
```

The package was added as a `file:` dependency in `package.json`.

> If there is a _red squiggly_ versioning error on the `s4-bupa-integration` dependency in the `package.json`, you can safely ignore it.

Let's see what got installed by expanding the folder `node_modules/s4-bupa-integration` (in the file explorer or in the terminal):

```bash
node_modules/s4-bupa-integration
├── bupa
│   ├── BusinessPartnerA2X.cds
│   ├── BusinessPartnerA2X.edmx
│   ├── BusinessPartnerA2X.js
│   ├── data
│   │   └── BusinessPartnerA2X-A_BusinessPartner.csv
│   └── index.cds
└── package.json
```

As expected, all files are available. Note though that `node_modules/s4-bupa-integration` is a symlink to the actual package directory `../s4-bupa-integration`. This means that any change there will be immediately visible in the application, which is great for development roundtrips!

## Use

Replace the `using ... from './external'` line in `srv/mashup.cds` (incidents app) with:

```js
using { s4 } from 's4-bupa-integration/bupa';
```

> Note the path difference in the from 's4-bupa-integration/bupa' clause. For NPM packages – and this is what we have here – it starts with the package name right away, i.e. without a leading ./
    Also, the /bupa path is actually /bupa/index.cds, but index.cds can always be omitted.

Now delete folder `srv/external`.

Start the application with `cds watch` again, and you can see in the log that the model files from the `../s4-bupa-integration/` package are used, as well as the mock implementation `../s4-bupa-integration/bupa/BusinessPartnerA2X.js`:

```bash
[cds] - loaded model from 7 file(s):

  db/schema.cds
  ...
  ../s4-bupa-integration/bupa/index.cds
  ../s4-bupa-integration/bupa/BusinessPartnerA2X.cds
...
[cds] - mocking BusinessPartnerA2X { path: '/api-business-partner', impl: '../s4-bupa-integration/bupa/BusinessPartnerA2X.js' }
```

The application works as before!

## Summary

You've now learned how to add an integration package. You've also seen that quite some application code became obsolete and could be removed:

- The imported edmx file and the resulting csn file
- The js mock implementation and sample data

And that additional features can be added in such packages, like

- Event definitions
- Event emitters for local testing
- CDS projections for model parts that are often used, like the Customers definition.
- Additional annotations, like for SAP Fiori Elements

CAP also has a [plugin](https://cap.cloud.sap/docs/node.js/cds-plugins) concept. Plugins can be distributed via npm as we've done in this exercise and provide a powerful way to create your own resuable CAP capabilities, such as new annotations for example.

The SAP community already provides a number of great plugins with some examples shown below:

- __[telemetry](https://github.com/cap-js/telemetry)__
    > CDS plugin providing observability features, incl. automatic OpenTelemetry instrumentation.

- __[change-tracking](https://github.com/cap-js/change-tracking)__
    > CDS plugin providing out-of-the box support for automatic capturing, storing, and viewing of the change records of modeled entities.

- __[notifications (Work Zone notifications)](https://github.com/cap-js/notifications)__
    > About CDS plugin providing integration to the SAP Alert Notification Service to publish Business Notifications.

- __[audit-logging](https://github.com/cap-js/audit-logging)__
    > CDS plugin providing integration to the SAP Audit Log service as well as out-of-the-box personal data-related audit logging based on annotations.

- __[event-queue](https://github.com/cap-js-community/event-queue)__
    > An event queue that enables secure multi-tenant enabled transactional processing of asynchronous events, featuring instant event processing with Redis Pub/Sub and load distribution across all application instances.

- __CAP Field Validations__
    > https://github.com/MertSAP/CAPVAL


With CAP you can bring in the whole power of the Node.js or Java ecosystems into your projects.

For example here is a handy node.js library (a java one also exists):

- __Alert Notification Service node.js library__
    > https://github.com/SAP/alert-notification-node-client


Continue to - [Further Reading & Tutorials](../Further%20Reading/README.md)
