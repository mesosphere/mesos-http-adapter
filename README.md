# Mesos HTTP API Adapter

## Goal
The goal of this project is to enable existing Mesos frameworks to try out the Mesos `V1` [HTTP API](http://mesos.apache.org/documentation/latest/scheduler-http-api/) using the existing `SchedulerDriver` interface.

## Intent
This project's intent is to help migrate existing Mesos frameworks to the HTTP API, and not become the de-facto way of using HTTP API.

## Usage

### Maven

To add `mesos-http-adapter` as a dependency on your project add following to your `pom.xml`:
```xml
<dependency>
  <groupId>com.mesosphere</groupId>
  <artifactId>mesos-http-adapter</artifactId>
  <version>0.3.0</version>
</dependency>
```

### Gradle

To add `mesos-http-adapter` as a dependency on your project add following to your `build.gradle`:

```
compile "com.mesosphere:mesos-http-adaptor:0.3.0"
```

### Source code

Using `MesosToSchedulerDriverAdapter` is really simple, as it's a drop-in replacement of `MesosSchedulerDriver`. In your framework code, you need to just update the code which instantiates `MesosSchedulerDriver`. For ex:

Before:

```java
MesosSchedulerDriver driver = new MesosSchedulerDriver(scheduler, frameworkInfo, masterUrl);
```

After:

```java
MesosSchedulerDriver driver = new MesosToSchedulerDriverAdapter(scheduler, frameworkInfo, masterUrl);
```

If you are using `Credential`, then also it's as simple as:

Before:

```java
MesosSchedulerDriver driver = new MesosSchedulerDriver(scheduler, frameworkInfo, masterUrl, credential);
```

After:

```java
MesosSchedulerDriver driver = new MesosToSchedulerDriverAdapter(scheduler, frameworkInfo, masterUrl, credential);
```

## Switching between `V0` and `V1` API

By default, `MesosToSchedulerDriverAdapter` uses `V0` version of API (non-HTTP). 

To use `V1` version of API, you just need to start your framework with `MESOS_API_VERSION` environment variable set to `V1`. For ex:

```
export MESOS_API_VERSION=V1
```

If for some reason you ever want to go back to `V0` version while already running framework with version `V1` of API, you just need to restart your framework with either `MESOS_API_VERSION` environment variable set to `V0` OR by unsetting `MESOS_API_VERSION` (which automatically default to `V0`). For ex:

```
export MESOS_API_VERSION=V0
``` 

OR 

```
unset MESOS_API_VERSION
```
