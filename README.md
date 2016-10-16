# Serverless Plugin: External SNS Events

[![Build Status](https://travis-ci.org/silvermine/serverless-plugin-external-sns-events.png?branch=master)](https://travis-ci.org/silvermine/serverless-plugin-external-sns-events)
[![Coverage Status](https://coveralls.io/repos/github/silvermine/serverless-plugin-external-sns-events/badge.svg?branch=master)](https://coveralls.io/github/silvermine/serverless-plugin-external-sns-events?branch=master)
[![Dependency Status](https://david-dm.org/silvermine/serverless-plugin-external-sns-events.png)](https://david-dm.org/silvermine/serverless-plugin-external-sns-events)
[![Dev Dependency Status](https://david-dm.org/silvermine/serverless-plugin-external-sns-events/dev-status.png)](https://david-dm.org/silvermine/serverless-plugin-external-sns-events#info=devDependencies&view=table)


## What is it?

This is a plugin for the Serverless framework to allow you have a function that
uses an already existing, or external (to that service), SNS topic as an event
source.

By default, the Serverless [SNS event
source](https://serverless.com/framework/docs/providers/aws/events/sns/) will
create a new topic just for that function, but in many cases if you want a
function to subscribe to a topic, the topic will have already been create,
either in the same service or in a different service.


## How do I use it?

Rather than defining an `sns` event for your function, define an `externalSNS`
event, where the value is either a string, or an object that works with
CloudFormation to resolve to an ARN.

```
functions:
   doSomething:
      name: ${self:service}-${self:provider.stage}-doSomething
      handler: src/DoSomething.handler
      events:
         - externalSNS:
            'Fn::Join':
               - 'arn:aws:sns:${self:custom.region}:'
               - { Ref: 'AWS::AccountId' }
               - ':some-topic'
```

Or:

```
functions:
   doSomething:
      name: ${self:service}-${self:provider.stage}-doSomething
      handler: src/DoSomething.handler
      events:
         - externalSNS: 'arn:aws:sns:us-east-1:1234567890:some-topic'
```

## How do I contribute?

Easy! Pull requests are welcome! Just do the following:

   * Clone the code
   * Install the dependencies with `npm install`
   * Create a feature branch (e.g. `git checkout -b my_new_feature`)
   * Make your changes and commit them with a reasonable commit message
   * Make sure the code passes our standards with `grunt standards`
   * Make sure all unit tests pass with `npm test`

Our goal is 100% unit test coverage, with **good and effective** tests (it's
easy to hit 100% coverage with junk tests, so we differentiate). We **will not
accept pull requests for new features that do not include unit tests**. If you
are submitting a pull request to fix a bug, we may accept it without unit tests
(we will certainly write our own for that bug), but we *strongly encourage* you
to write a unit test exhibiting the bug, commit that, and then commit a fix in
a separate commit. This *greatly increases* the likelihood that we will accept
your pull request and the speed with which we can process it.


## License

This software is released under the MIT license. See [the license file](LICENSE) for more details.