# Mesos HTTP API Adapter

## Goal
The goal of this project is to enable existing Mesos frameworks to try out the Mesos `V1` HTTP API using the existing `SchedulerDriver` interface.

## Intent
This project's intent is to help migrate existing Mesos frameworks to the HTTP API, and not become the de-facto way of using HTTP API.

## Usage

### Maven

To add `mesos-http-adapter` as a dependency on your project add following to your `pom.xml`:
```xml
<dependency>
  <groupId>com.mesosphere</groupId>
  <artifactId>mesos-http-adapter</artifactId>
  <version>0.1.0</version>
</dependency>
```

### Gradle

To add `mesos-http-adapter` as a dependency on your project add following to your `build.gradle`:

```
compile "com.mesosphere:mesos-http-adaptor:0.1.0"
```

### Switching between `V0` and `V1`

By default, `MesosToSchedulerDriverAdapter` uses `V0` version of API (non-HTTP). 

To use V1 version of API, start your framework scheduler with following environment variable:

`MESOS_API_VERSION=V1`
