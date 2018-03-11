# Instructions

Importing the `random-uid-kafka-openshift-template.yml` template should configure everything automatically. The only additional required parameter is `${NAMESPACE}`, which should be set to the project's namespace in order to configure service DNS entries correctly.

One common gotcha with the cp-kafka image is that the startup scripts contain many checks for environment variables with the prefix KAFKA. If you name your service "kafka", OpenShift will inject KAFKA_TCP_PORT etc., environment variables automatically and the container will fail to start.

## Spring Boot Test App

A simple test spring boot app is included in this repository to test connectivity. You can build it using S2I using the following command, filling in the necessary environment variables:

```
oc new-app codecentric/springboot-maven3-centos~https://github.com/jmcelwain/random-uid-kafka-openshift \
  -e NAMESPACE=... \
  -e KAFKA_BROKER_PORT=...
```

