# serverless AWS Rust HTTP template

A sample template for bootstraping [Rustlang AWS Lambda](https://github.com/awslabs/aws-lambda-rust-runtime/) HTTP applications with ⚡ serverless framework ⚡.

## ✨ features

- 🦀 Build Rustlang applications targeting AWS Lambda with ease
- 🛵 Continuous integration testing with GitHub Actions
- 🚀 Continuous deployment with GitHub Actions
- 🧪 Getting started tests

## 📦 install

Install the [serverless framework](https://www.serverless.com/framework/docs/getting-started/) cli.

Then then run the following in your terminal

```bash
$ npx serverless install \
  --url https://github.com/softprops/serverless-aws-rust-http \
  --name my-new-api
```

This will download the source of a sample Rustlang application and unpack it as a new service named
"my-new-api" in a directory called "my-new-api"

## 🧙 how to be a wizard

Assumming you have [aws credentials with appropriate deployment permissions configured](https://serverless.com/framework/docs/providers/aws/guide/credentials/)
(if you already use any existing AWS tooling installed you likely already have this configured), you can impress your friends by creating a project
that is _born_ in a production environment.

```bash
$ npx serverless install \
  --url https://github.com/softprops/serverless-aws-rust-http \
  --name my-new-api \
  && cd my-new-api \
  && npm i \
  && npx serverless deploy
```

`npm i` will make sure npm dependencies are installed. This only needs run once.
The first time you run `npx serverless deploy` it will pull down and compile the base set
of dependencies and your application. Unless the dependencies change afterwards,
this should only happen once, resulting in an out of the box rapid deployment
cycle.

## 🛵 continuous integration and deployment

This template includes an example [GitHub actions](https://travis-ci.org/) [configuration file](.github/workflows/main.yml) which can unlock a virtuous cycle of continuous integration and deployment
( i.e all tests are run on prs and every push to master results in a deployment ).

GitHub actions is managed simply by the presence of a file checked into your repository. To set up GitHub Actions to deploy to AWS you'll need to do a few things

Firstly, version control your source. [Github](https://github.com/) is free for opensource.

```bash
$ git init
$ git remote add origin git@github.com:{username}/{my-new-service}.git
```

Store a `AWS_ACCESS_KEY_ID` `AWS_SECRET_ACCESS_KEY` used for aws deployment in your repositories secrets https://github.com/{username}/{my-new-service}/settings/secrets

Add your changes to git and push them to GitHub.

Finally, open https://github.com/{username}/{my-new-service}/actions in your browser and grab a bucket of popcorn 🍿

## 🔫 function triggering

With your function deployed you can now start triggering it using `serverless` framework directly or
the AWS integration you've configured to trigger it on your behalf

Copy this sample apigateway request into a file called payload.json

```json
{
  "path": "/test/hello",
  "headers": {
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
    "Accept-Encoding": "gzip, deflate, lzma, sdch, br",
    "Accept-Language": "en-US,en;q=0.8",
    "CloudFront-Forwarded-Proto": "https",
    "CloudFront-Is-Desktop-Viewer": "true",
    "CloudFront-Is-Mobile-Viewer": "false",
    "CloudFront-Is-SmartTV-Viewer": "false",
    "CloudFront-Is-Tablet-Viewer": "false",
    "CloudFront-Viewer-Country": "US",
    "Host": "wt6mne2s9k.execute-api.us-west-2.amazonaws.com",
    "Upgrade-Insecure-Requests": "1",
    "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.82 Safari/537.36 OPR/39.0.2256.48",
    "Via": "1.1 fb7cca60f0ecd82ce07790c9c5eef16c.cloudfront.net (CloudFront)",
    "X-Amz-Cf-Id": "nBsWBOrSHMgnaROZJK1wGCZ9PcRcSpq_oSXZNQwQ10OTZL4cimZo3g==",
    "X-Forwarded-For": "192.168.100.1, 192.168.1.1",
    "X-Forwarded-Port": "443",
    "X-Forwarded-Proto": "https"
  },
  "pathParameters": {
    "proxy": "hello"
  },
  "requestContext": {
    "accountId": "123456789012",
    "resourceId": "us4z18",
    "stage": "test",
    "requestId": "41b45ea3-70b5-11e6-b7bd-69b5aaebc7d9",
    "identity": {
      "cognitoIdentityPoolId": "",
      "accountId": "",
      "cognitoIdentityId": "",
      "caller": "",
      "apiKey": "",
      "sourceIp": "192.168.100.1",
      "cognitoAuthenticationType": "",
      "cognitoAuthenticationProvider": "",
      "userArn": "",
      "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.82 Safari/537.36 OPR/39.0.2256.48",
      "user": ""
    },
    "resourcePath": "/{proxy+}",
    "httpMethod": "GET",
    "apiId": "wt6mne2s9k"
  },
  "resource": "/{proxy+}",
  "httpMethod": "GET",
  "queryStringParameters": {
    "name": "me"
  },
  "stageVariables": {
    "stageVarName": "stageVarValue"
  }
}
```

Then invoke your function with a synthetic request

```sh
$ npx serverless invoke -f hello -d "$(cat payload.json)"
```

## 🔬 logs

With your function deployed you can now tail it's logs right from your project

```sh
$ npx serverless logs -f hello
```

## 👴 retiring

Good code should be easily replaceable. Good code is should also be easily disposable. Retiring applications should be as easy as creating and deploying them. The dual of `serverless deploy` is `serverless remove`. Use this for retiring services and cleaning up resources.

```bash
$ npx serverless remove
```

## ℹ️ additional information

- See the [serverless-rust plugin's documentation](https://github.com/softprops/serverless-rust) for more information on plugin usage.

- See the [aws rust runtime's documentation](https://github.com/awslabs/aws-lambda-rust-runtime) for more information on writing Rustlang lambda functions

## 👯 contributing

This template's intent is to set a minimal baseline for getting engineers up an running with a set of repeatable best practices. See something you'd like in this template that would help others? Feel free to [open a new github issue](https://github.com/softprops/serverless-aws-rust-http/issues/new). Pull requests are also welcome.
