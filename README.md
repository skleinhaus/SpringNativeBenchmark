# Spring Native Benchmark

The purpose of this project is to determine the advantages of using GraalVM native AOT compilation in combination with Spring Boot. Specifically in cloud environments like Google Cloud 

## Creating an image

### Native with GraalVM
Create the native executable at target/springnativebenchmark

```
./mvn -Pnative native:compile
```

Create a native image

```
docker build -f src/main/docker/Dockerfile.native -t springnativebenchmark .
```

### JVM

Create a JAR file


```
./mvn package
```

Extract the JAR contents

```
java -Djarmode=layertools -jar target/*.jar extract --destination target/extracted
```

Create the JVM image

```
docker build -f src/main/docker/Dockerfile.jvm -t springnativebenchmarkjvm .
```

