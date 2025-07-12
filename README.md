<!--
title: 'Serverless Framework Node Express API on AWS'
description: 'This application demonstrates how to develop and deploy a simple Node Express API running on AWS Lambda using the Serverless Framework.'
layout: Doc
framework: v4
platform: AWS
language: nodeJS
priority: 1
authorLink: 'https://github.com/serverless'
authorName: 'Serverless, Inc.'
authorAvatar: 'https://avatars1.githubusercontent.com/u/13742415?s=200&v=4'
-->

# Serverless Framework TypeScript Node Express API on AWS

This application demonstrates how to develop and deploy a simple TypeScript Node Express API service running on AWS Lambda using the Serverless Framework.

This application configures a lambda function for each endpoint specified in `serverless.yml`, which is responsible for handling incoming requests using the `httpApi` event. To learn more about `httpApi` event configuration options, please refer to [httpApi event docs](https://www.serverless.com/framework/docs/providers/aws/events/http-api/). As the event is configured in a way to accept all incoming requests, the Express.js framework is responsible for routing and handling requests internally. This implementation uses the `serverless-http` package to transform the incoming event request payloads to payloads compatible with Express.js. To learn more about `serverless-http`, please refer to the [serverless-http README](https://github.com/dougmoscrop/serverless-http).

## Usage

> [!IMPORTANT]
> Follow the [Getting Started](https://www.serverless.com/framework/docs/getting-started) guide for the Serverless Framework as a prerequisite to deploying this application.

### Deployment

Install dependencies with:

```
npm install
```

and then deploy with:

```
serverless deploy
```

After running deploy, you should see output similar to:

```
Deploying "test-project" to stage "dev" (eu-north-1)

✔ Service deployed to stack test-project-dev (45s)

endpoint: 
  GET - https://xxxxxxxxxx.execute-api.eu-north-1.amazonaws.com
  GET - https://xxxxxxxxxx.execute-api.eu-north-1.amazonaws.com/hello
functions:
  app: test-project-dev-app (856 kB)
  sayHello: test-project-dev-sayHello (856 kB)
```

### Invocation

After successful deployment, you can call the created application via HTTP:

```
curl https://xxxxxxx.execute-api.eu-north-1.amazonaws.com/
```

Which should result in the following response:

```json
{ "message": "Hello from root!" }
```

### Local development

The easiest way to develop and test your function is to use the `dev` command:

```
serverless dev
```

This will start a local emulator of AWS Lambda and tunnel your requests to and from AWS Lambda, allowing you to interact with your function as if it were running in the cloud.

Now you can invoke the function as before, but this time the function will be executed locally. Now you can develop your function locally, invoke it, and see the results immediately without having to re-deploy.

When you are done developing, don't forget to run `serverless deploy` to deploy the function to the cloud.

### Remove deployment

Remove the deployed service created under the [deployment step](#deployment) with:

```
serverless remove
```

After running remove, you should see output similar to:

```
Removing "test-project" from stage "dev" (eu-north-1)

✔ Service test-project has been successfully removed (34s)
```
