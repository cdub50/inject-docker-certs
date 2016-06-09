# Inject Docker Certificates -- Docker Native for Mac

## Is this you?

```
╭─mathias.klippinge at SE-C02PPAD5G8WP in ~/src/mood-test on master✘✘✘ using ‹ruby-2.3.1› 16-06-09 - 11:03:08
╰─○ docker pull docker.staging.eu1.order-management.klarna.net/dynakafka-application:latest
Error response from daemon: Get https://docker.staging.eu1.order-management.klarna.net/v1/_ping: x509: certificate signed by unknown authority
```

![Feels bad man](![Alt text](/relative/path/to/img.jpg?raw=true "Optional Title") "Feels bad man")

## We got you covered!

You need to inject your ca into docker!

Visit [this repo](https://github.com/gesellix/inject-docker-certs) for a complete and easy guide.

This repo is the SHOW ME THE MONEY version, since "easy" is not easy enough, we all have stuff to do and business to go about.

So,

1. Make sure the certificate you want inside the Docker native VM is in the current directory.
1. For good measure, make sure the certificate is valid: `openssl x509 -in klarna_ca.crt -text -noout`
1. build the image: `docker build -t inject-docker-certs .`
1. run the patch: `docker run --rm -it -v `pwd`:/certs -v /etc:/vm-etc -e CERTIFICATE=klarna_ca.crt inject-docker-certs`

Make sure `klarna_ca.crt` is replaced with whatever filename you might have.
