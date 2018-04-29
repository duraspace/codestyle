# DuraSpace Code Style

The purpose of this repository is to provide resources for maintaining consistent coding style. The resources in this repository are available for use by DuraSpace projects as well as any other individuals or projects interested in maintaining a coding style consistent with well established open source projects.

[Checkstyle](#checkstyle) | [Code Style Guide](#code-style-guide) | [IDE Support](#ide-support) | [License](#license)

## Checkstyle

<p align="center">
  <a href="http://checkstyle.sourceforge.net"><img src="http://checkstyle.sourceforge.net/images/header-checkstyle-logo.png" alt="Checkstyle Logo"/></a>
</p>

[Checkstyle](https://github.com/checkstyle/checkstyle) is a development tool for Java, used to ensure that code standards are applied consistently.

Checkstyle can be enabled in Java projects with Maven using the [Maven Checkstyle Plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin). Add the following into the <build><plugins> section of your Maven POM.xml file:

```xml
<!-- Used to validate all code style rules in source code using Checkstyle -->
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-checkstyle-plugin</artifactId>
    <version>3.0.0</version>
    <executions>
        <execution>
            <id>verify-style</id>
            <!-- Bind to verify so it runs after package & unit tests, but before install -->
            <phase>verify</phase>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <configLocation>duraspace-checkstyle/checkstyle.xml</configLocation>
        <suppressionsLocation>*your-checkstyle-suppression.xml*</suppressionsLocation>
        <encoding>UTF-8</encoding>
        <consoleOutput>true</consoleOutput>
        <logViolationsToConsole>true</logViolationsToConsole>
        <failOnViolation>true</failOnViolation>
        <includeTestSourceDirectory>true</includeTestSourceDirectory>
    </configuration>
    <dependencies>
        <dependency>
            <groupId>org.duraspace</groupId>
            <artifactId>codestyle</artifactId>
            <version>${duraspace-codestyle.version}</version>
        </dependency>
        <dependency>
            <groupId>*your-suppression-group*</groupId>
            <artifactId>*your-suppression-artifact*</artifactId>
            <version>*your-suppression-version*</version>
        </dependency>

        <!-- Override dependencies to use latest version of checkstyle -->
        <dependency>
            <groupId>com.puppycrawl.tools</groupId>
            <artifactId>checkstyle</artifactId>
            <version>8.8</version>
        </dependency>
    </dependencies>
</plugin>
```

Once this configuration is in place, executing a build on the project  (`mvn clean install` ) will trigger checkstyle checks which will cause the build to fail if a style violation is encountered.

## Code Style Guide

The following code guidelines are enforced by the checkstyle rules:

1. 4-space indents for Java, and 2-space indents for XML. NO TABS ALLOWED.
2. K&R style braces required. Braces are required on all blocks, e.g.
    ```java
    if (code) {
      // code
    } else {
      // code
    }
    ```
3. Maximum length of lines is 120 characters (except for long URLs, packages or imports)
4. No trailing spaces allowed
5. Do not use wildcard imports (e.g. `import java.util.*`). Duplicated or unused imports are not allowed.
6. Write Javadocs for public methods and classes. Keep it short and to the point.
   1. Javadoc `@author` tags are optional, but should refer to an individual's name or handle (e.g. GitHub username) when included
7. Tokens should be surrounded by whitespace ([details here](http://checkstyle.sourceforge.net/config_whitespace.html#WhitespaceAround))
8. Each line of code can only include one statement.  This also means each variable declaration must be on its own line, e.g.
    ```java
    // This is NOT valid. Three variables are declared on one line
    String first = "", second = "", third = "";

    // This is valid. Each statement is on its own line
    String first = "";
    String second = "";
    String third = "";
    ```
9. No empty "catch" blocks in try/catch.  A "catch" block must minimally include a comment as to why the catch is empty, e.g.
    ```java
    try {
      // some code ..
    } catch (Exception e) {
      // ignore, this exception is not important
    }
    ```   
10. All "switch" statements must include a "default" clause.  Also, each clause in a switch must include a "break", "return", "throw", "continue", or a `// fall through` comment
    ```java
    // This is NOT valid. Switch doesn't include a "default" and is missing a "break" in first "case"
    switch (myVal) {
      case "one":
        // do something
      case "two":
        // do something else
        break;
    }

    // This is valid. Switch has all necessary breaks and includes a "default" clause
    switch (myVal) {
      case "one":
        // do something
        break;
      case "two":
        // do something else
        break;
      case "three":
        // do another thing
        // fall through
      default:
        // do nothing
        break;
    }
    ```
11. Any "utility" classes (a utility class is one that just includes static methods or variables) should have non-public (i.e. private or protected) constructors, e.g.
    ```java
    // This is an example class of static constants
    public class Constants {
       public static final String DEFAULT_ENCODING = "UTF-8";
       public static final String ANOTHER_CONSTANT = "Some value";

       // As this is a utility class, it MUST have a constructor that is non-public.
       private Constants() {
       }
    }
    ```
12. Import statements must be ordered alphabetically and grouped by matching packages. The groupings must be in the order:
    1. Static imports
    2. Standard java packages (java.* and javax.*)
    3. Third party packages
13. No more than one consecutive blank line
14. A blank line must follow each major code section (imports, class definitions, interface definitions, enum definitions, static initialization blocks, method definitions, constructor definitions)

## IDE Support

Most major IDEs include plugins that support Checkstyle configurations. The plugin usually lets you import an existing [checkstyle.xml configuration](https://raw.githubusercontent.com/duraspace/resources/master/checkstyle/duraspace-checkstyle.xml) to configure your IDE to use and/or validate against that style.

Select an IDE from the list for more details on how to configure your IDE to use Checkstyle:

* [IntelliJ IDEA](ide-support/intellij.md)
* [Eclipse](ide-support/eclipse.md)
* [NetBeans](ide-support/netbeans.md)

## License

All resources in this repository are made available under the [Apache 2 license](https://www.apache.org/licenses/LICENSE-2.0).
