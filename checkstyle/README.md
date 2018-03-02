[Checkstyle](https://github.com/checkstyle/checkstyle) is a development tool for Java, used to ensure that code standards are applied consistently.

Checkstyle can be enabled in Java projects using Maven using the [Maven Checkstyle Plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin)

```xml
<!-- Used to validate all code style rules in source code using Checkstyle -->
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-checkstyle-plugin</artifactId>
    <version>3.0.0</version>
    <executions>
        <execution>
            <id>verify-style</id>
            <!-- Bind to process-classes so it runs after compile, but before package -->
            <phase>process-classes</phase>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <configLocation>https://raw.githubusercontent.com/duraspace/resources/master/checkstyle/duraspace-checkstyle.xml</configLocation>
        <suppressionsLocation>https://raw.githubusercontent.com/duraspace/resources/master/checkstyle/duraspace-checkstyle-suppressions.xml</suppressionsLocation>
        <encoding>UTF-8</encoding>
        <consoleOutput>true</consoleOutput>
        <logViolationsToConsole>true</logViolationsToConsole>
        <failOnViolation>true</failOnViolation>
        <includeTestSourceDirectory>true</includeTestSourceDirectory>
    </configuration>
    <dependencies>
        <!-- Override dependencies to use latest version of checkstyle -->
        <dependency>
            <groupId>com.puppycrawl.tools</groupId>
            <artifactId>checkstyle</artifactId>
            <version>8.8</version>
        </dependency>
    </dependencies>
</plugin>
```
