# Serverless image processing

The example repository will contain a basic image processing service. It will do
nothing complex but will be deployed on serverless infrastructure. Perhaps a
basic example to start with is image resize.

## Design goals

Given the popularity of AWS services this will likely be deployed using AWS
infrastructure. While planning the technical approach the following design goals
will be followed.

1. Be accessible over a simple REST API.
2. Use the highest level of abstractions available.
3. Be infinitely vertically scalable.

## Process overview

Regardless of the image processing required there are some basic steps which
need to be completed.

1. Upload the image.
2. Perform the image processing.
3. Download result data.

In the above process (2) could take some time to complete.

## Architecture patterns

Given the time the image processing might take to complete, we should avoid
having a single long running request for all the processing. Instead we might
want to create a resource which can be used to manage the whole process.

Making use of a resource to manage the process would provide the client with a
unique reference to manage the running process. With this reference the client
can check the processing, each single request would complete in a short amount
of time.
