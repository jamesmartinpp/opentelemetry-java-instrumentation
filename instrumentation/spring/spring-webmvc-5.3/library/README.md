# Library Instrumentation for Spring Web MVC

Provides OpenTelemetry instrumentation for Spring WebMVC controllers.

## Quickstart

### Add these dependencies to your project.

Replace `SPRING_VERSION` with the version of spring you're using.
 - `Minimum version: 5.3`

Replace `OPENTELEMETRY_VERSION` with the latest stable [release](https://mvnrepository.com/artifact/io.opentelemetry).
 - `Minimum version: 1.17.0`

For Maven add the following to your `pom.xml`:

```xml
<dependencies>
  <!-- OpenTelemetry instrumentation -->
  <dependency>
    <groupId>io.opentelemetry.instrumentation</groupId>
    <artifactId>opentelemetry-spring-webmvc-5.3</artifactId>
    <version>OPENTELEMETRY_VERSION</version>
  </dependency>

   <!-- OpenTelemetry exporter -->
   <!-- replace this default exporter with your OpenTelemetry exporter (ex. otlp/zipkin/jaeger/..) -->
   <dependency>
    <groupId>io.opentelemetry</groupId>
    <artifactId>opentelemetry-exporter-logging</artifactId>
    <version>OPENTELEMETRY_VERSION</version>
  </dependency>

  <!-- required to instrument Spring WebMVC -->
  <!-- this artifact should already be present in your application -->
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>SPRING_VERSION</version>
  </dependency>

</dependencies>
```

For Gradle add the following to your dependencies:

```groovy

// OpenTelemetry instrumentation
implementation("io.opentelemetry.instrumentation:opentelemetry-spring-webmvc-5.3:OPENTELEMETRY_VERSION")

// OpenTelemetry exporter
// replace this default exporter with your OpenTelemetry exporter (ex. otlp/zipkin/jaeger/..)
implementation("io.opentelemetry:opentelemetry-exporter-logging:OPENTELEMETRY_VERSION")

// required to instrument Spring WebMVC
// this artifact should already be present in your application
implementation("org.springframework:spring-webmvc:SPRING_VERSION")
```

### Features

#### `SpringWebMvcTelemetry`

`SpringWebMvcTelemetry` enables creating OpenTelemetry server spans around HTTP requests processed
by the Spring servlet container.

##### Usage in Spring Boot

Spring Boot allows servlet `Filter`s to be registered as beans:

```java
import io.opentelemetry.api.OpenTelemetry;
import io.opentelemetry.instrumentation.spring.webmvc.v5_3.SpringWebMvcTelemetry;
import javax.servlet.Filter;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SpringWebMvcTelemetryConfiguration {

   @Bean
   public Filter telemetryFilter(OpenTelemetry openTelemetry) {
      return SpringWebMvcTelemetry.create(openTelemetry).createServletFilter();
   }
}
```

### Starter Guide

Check
out [OpenTelemetry Manual Instrumentation](https://opentelemetry.io/docs/instrumentation/java/manual/)
to learn more about using the OpenTelemetry API to instrument your code.
