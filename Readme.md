## Apollo Federation Demo

This repository is a demo of using Apollo Federation to build a single schema on top of multiple services. The microservices are located under the [`./services`](./services/) folder and the gateway that composes the overall schema is in the [`gateway.js`](./gateway.js) file.

### Installation

To run this demo locally, pull down the repository then run the following commands:

```sh
npm install
```

This will install all of the dependencies for the gateway and each underlying service.

```sh
npm run start-services
```

This command will run all of the microservices at once. They can be found at http://localhost:4001, http://localhost:4002, http://localhost:4003, and http://localhost:4004.

In another terminal window, run the gateway by running this command:

```sh
npm run start-gateway
```

This will start up the gateway and serve it at http://localhost:4000

### What is this?

This demo showcases four partial schemas running as federated microservices. Each of these schemas can be accessed on their own and form a partial shape of an overall schema. The gateway fetches the service capabilities from the running services to create an overall composed schema which can be queried. 

To see the query plan when running queries against the gateway, click on the `Query Plan` tab in the bottom right hand corner of [GraphQL Playground](http://localhost:4000)

To learn more about Apollo Federation, check out the [docs](https://www.apollographql.com/docs/apollo-server/federation/introduction)


### Managed Federation
-To update the demo to be a managed federation follow the guide on the Apollo website

-To add a subgraph use the following (first address is running service to introspect and get schema details, second is the location of the service to direct to when called):
rover subgraph introspect \
  http://localhost:4004 | \
  APOLLO_KEY=service:Managed-Federation-Test-9ahmg7:yGJrCGg5613S6Qx56DAEEw \
  rover subgraph publish Managed-Federation-Test-9ahmg7@current \
  --name inventory --schema - \
  --routing-url http://localhost:4004

  -When adding a .env file don't forget to add the following to the top of the gateway file after installing dotenv:
  require('dotenv').config();