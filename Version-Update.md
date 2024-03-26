# <a href="https://github.com/mosip/registration">Registration</a>

## 1. <a href="https://github.com/mosip/registration/blob/master/registration-processor/pom.xml">Pom.xml (registration-processor\pom.xml)</a>


### 1. Maven
Older version:

```xml
<maven.compiler.source>11</maven.compiler.source>
<maven.compiler.target>11</maven.compiler.target>
<maven.compiler.version>3.8.0</maven.compiler.version>
<maven.jar.plugin.version>3.0.2</maven.jar.plugin.version>
<maven.war.plugin.version>3.1.0</maven.war.plugin.version>
<maven.surefire.plugin.version>2.22.0</maven.surefire.plugin.version>
<maven.jacoco.version>0.8.5</maven.jacoco.version>
<maven.sonar.plugin.version>3.7.0.1746</maven.sonar.plugin.version>
<maven.javadoc.version>3.2.0</maven.javadoc.version>
```

Updated version:

```xml
<maven.compiler.source>17</maven.compiler.source>
<maven.compiler.target>17</maven.compiler.target>
<maven.compiler.version>3.8.1</maven.compiler.version>
<maven.jar.plugin.version>3.3.0</maven.jar.plugin.version>
<maven.war.plugin.version>3.1.0</maven.war.plugin.version>
<maven.surefire.plugin.version>3.2.5</maven.surefire.plugin.version>
<maven.jacoco.version>0.8.8</maven.jacoco.version>
<maven.sonar.plugin.version>7.31.0.34839</maven.sonar.plugin.version>
<maven.javadoc.version>3.6.3</maven.javadoc.version>
<maven.assembly.version>3.3.0</maven.assembly.version>
```

### 2. Spring boot version and its related

older version:

```xml
<spring.boot.version>2.0.2.RELEASE</spring.boot.version>
<spring.data.version>2.0.9.RELEASE</spring.data.version>
<spring-cloud-config.version>2.0.0.RELEASE</spring-cloud-config.version>
```

updated version:

```xml
<spring.boot.version>2.7.18</spring.boot.version>
<spring.data.version>2.7.18</spring.data.version>
<spring-cloud-config.version>3.1.3</spring-cloud-config.version>
```

## 3. junit

Older:

```xml
<junit.version>4.12</junit.version>
```

Updated:

```xml
<junit.version>4.13.2</junit.version>
```

## 4. lombok

Older:

```xml
<lombok.version>1.18.8</lombok.version>
```

### 
```xml
<lombok.version>1.18.30</lombok.version>
```

### 5.  Added plugin to support lombok (needed for java 17):

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>${maven.compiler.version}</version>
    <configuration>
        <source>${maven.compiler.source}</source>
        <target>${maven.compiler.target}</target>
        <fork>true</fork>
        <compilerArgs>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.code=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.comp=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.file=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.main=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.model=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.parser=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.processing=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.tree=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.util=ALL-UNNAMED</arg>
            <arg>-J--add-opens=jdk.compiler/com.sun.tools.javac.jvm=ALL-UNNAMED</arg>
        </compilerArgs>
        <annotationProcessorPaths>
            <path>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <version>${lombok.version}</version>
            </path>
        </annotationProcessorPaths>
    </configuration>
</plugin>
```

## 2. WebClient using ssl:

Reference: https://stackoverflow.com/questions/45418523/spring-5-webclient-using-ssl

Path : <a href="https://github.com/mosip/registration/blob/master/registration-processor/pre-processor/registration-processor-packet-validator-stage/src/main/java/io/mosip/registration/processor/stages/helper/RestHelperImpl.java">registration-processor\pre-processor\registration-processor-packet-validator-stage\src\main\java\io\mosip\registration\processor\stages\helper\RestHelperImpl.java</a>


Older :

```java
org.springframework.web.reactive.function.client.WebClient.Builder webClientBuilder = WebClient.builder().clientConnector(new ReactorClientHttpConnector(builder -> builder.sslContext(sslContext)))
```

Updated:

```java
import reactor.netty.http.client.HttpClient;
```

```java
SslContext context = SslContextBuilder.forClient().trustManager(InsecureTrustManagerFactory.INSTANCE).build();
HttpClient httpClient = HttpClient.create().secure(t -> t.sslContext(context));

org.springframework.web.reactive.function.client.WebClient.Builder webClientBuilder = WebClient.builder().clientConnector(new ReactorClientHttpConnector(httpClient))
```

## 3. Simple Java toolkit for JSON (version):

#### Changes in the following file:
<a href="https://github.com/mosip/registration/tree/master/registration-processor/registration-processor-core/pom.xml">registration-processor\registration-processor-core\pom.xml </a>

<a href="https://github.com/mosip/registration/tree/master/registration-processor/registration-processor-info-storage-service/pom.xml">registration-processor\registration-processor-info-storage-service\pom.xml</a>



Older version:

```xml
<dependency>
	<groupId>com.googlecode.json-simple</groupId>
	<artifactId>json-simple</artifactId>
</dependency>
```

Updated version:

```xml
<dependency>
	<groupId>com.googlecode.json-simple</groupId>
	<artifactId>json-simple</artifactId>
	<version>1.1.1</version>
</dependency>
```
