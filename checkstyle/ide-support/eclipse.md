# Eclipse

*These instructions were created using Eclipse Neon.  Note: Eclipse Che (Codenvy) does not seem to support checkstyle.*

* Install the Eclipse Checkstyle plugin:  http://eclipse-cs.sourceforge.net/
  * Note that you can drag the plugin into your Eclipse installation
* Right click your project; select Properties → Checkstyle
* Go to `Checkstyle` → `Local check configurations` and click `New`
  * Create a `Project Relative Configuration`
  * Name: DuraSpace Checkstyle
  * Location: duraspace-checkstyle.xml
* An "Unresolved Properties Error" box will appear; click `Edit Properties`
  * Add a new property
    * Name: checkstyle.suppressions.file
    * Value: duraspace-checkstyle-suppressions.xml
  * Click OK
* Go to `Checkstyle` → `Main`
  * Select "DuraSpace Checkstyle" from the drop down
  * Check `Checkstyle active for this project`
  * Click OK
* Code will be rebuilt
* Edit a java file.  Place a curly brace on a line by itself.
  * The line of code should get highlighted in red.

Tested and works to validate code. To format you must generate a formatter style following the [steps here](https://stackoverflow.com/questions/984778/how-to-generate-an-eclipse-formatter-configuration-from-a-checkstyle-configurati). It seems impossible to force eclipse to use braces on sinle-line if statement

(*Please help us enhance these instructions to provide a step-by-step configuration for Eclipse*)
