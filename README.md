## Nettosphere: A Java WebSocket and HTTP server powered by the [Atmosphere Framework](http://github.com/Atmosphere/atmosphere) and the [Netty Framework](http://netty.io/)

The easiest way to get started with NettoSphere is to download a sample and start it. [Or look at the Javadoc](http://atmosphere.github.com/nettosphere/apidocs/). You can download one of our [sample](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.atmosphere.nettosphere.samples%22) distribution.

```bash
   % unzip nettosphere-<name>-distribution.jar
   % chmod a+x ./bin/nettosphere.sh
   % ./bin/nettosphere.sh
```

[Samples](https://github.com/Atmosphere/atmosphere-samples/tree/master/nettosphere-samples) are the same as then one available in Atmosphere. Bootstrap classes looks like [AtmosphereHandler](https://github.com/Atmosphere/atmosphere-samples/blob/master/nettosphere-samples/chat/src/main/java/org/nettosphere/samples/chat/NettosphereChat.java#L27) or [Jersey](https://github.com/Atmosphere/atmosphere-samples/blob/master/nettosphere-samples/jersey-chat/src/main/java/org/nettosphere/samples/chat/NettosphereJerseyChat.java#L31)

Download Nettosphere [here](http://search.maven.org/#search%7Cga%7C1%7Cnettosphere) or use Maven

```xml
     <dependency>
         <groupId>org.atmosphere</groupId>
         <artifactId>nettosphere</artifactId>
         <version>2.4.2 | 3.0.0-RC1</version>
     </dependency>
```

### Super Simple Web Application

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource(MyClass.class)
                    .build())
                 .build();
    server.start();
```

or

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource(new Handler() {
                        public void handle(AtmosphereResource r) {
                            try {
                                r.getResponse().write("Hello World").write(" from Nettosphere").flushBuffer();
                            } catch (IOException e) {
                                e.printStackTrace();
                            }
                        }
                    })
                    .build())
                 .build();
    server.start();
```

All [Atmosphere](http://jfarcand.wordpress.com/2011/11/07/hitchiker-guide-to-the-atmosphere-framework-using-websocket-long-polling-and-http-streaming/) API supported. As simple as:

[Top](#Top)

### Server static and dynamic resources, use atmosphere.xml to configure NettoSphere

```java
        Config.Builder b = new Config.Builder();
        b.resource("./webapps")
            .port(8080)
            .host("127.0.0.1")
            .configFile("../conf/atmosphere.xml")
            .build();
        Nettosphere s = new Nettosphere.Builder().config(b.build()).build();
```
[Top](#Top)

### Deploy a Resource (annotated using Jersey), access it using HTTP or WebSocket

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource(MyResource.class)
                    .build())
                 .build();
    server.start();
```
[Top](#Top)

### Deploy an AtmosphereHandler, access it using HTTP or WebSocket

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource("/*", MyAtmosphereHandler.class)
                    .build())
                 .build();
    server.start();
```

### Deploy an AtmosphereHandler, define a WebSocket protocol

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .webSocketProtocol(JMSOverWebSocketProtocol.class)
                    .resource("/*", MyAtmosphereHandler.class)
                    .build())
                 .build();
    server.start();
```
[Top](#Top)

### Deploy a Servlet which use Meteor

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource("/*", MyServlet.class)
                    .build())
                 .build();
    server.start();
```
[Top](#Top)

### The Server can also be started using java

```java
    java -cp nettosphere-all.jar
          org.atmosphere.nettosphere.Nettosphere
                [/path/to/an/exploded/war/file] [host] [port]
```
[Top](#Top)

### Using Maven and the Git repo

    mvn exec:java -Dexec.arguments='path to your exploded war file'

#### Build Status
[![Build Status](https://buildhive.cloudbees.com/job/Atmosphere/job/nettosphere/badge/icon)](https://buildhive.cloudbees.com/job/Atmosphere/job/nettosphere/)

#### [Change Log](./CHANGELOG.md)

2.4 release: [2.4.0]()
2.3 release: [2.3.3](https://github.com/Atmosphere/nettosphere/issues?q=label%3A2.3.3+is%3Aclosed) [2.3.2](https://goo.gl/gaTKLZ ) [2.3.1](https://github.com/Atmosphere/nettosphere/issues?q=label%3A2.3.1+is%3Aclosed) [2.3.0](https://github.com/Atmosphere/nettosphere/issues?q=label%3A2.3.0+is%3Aclosed)

2.1 release: [2.1.1](https://github.com/Atmosphere/nettosphere/issues?labels=2.1.1&page=1&sort=updated&state=closed)

2.0 release: [2.0.2](https://github.com/Atmosphere/nettosphere/issues?labels=2.0.2&page=1&sort=updated&state=closed) [2.0.1](https://github.com/Atmosphere/nettosphere/issues?labels=2.0.1&milestone=&page=1&sort=updated&state=closed)

We are on irc.freenode.net under #atmosphere-comet and [Twitter](http://twitter.com/jfarcand)

[![Analytics](https://ga-beacon.appspot.com/UA-31990725-2/Atmosphere/nettosphere)]
