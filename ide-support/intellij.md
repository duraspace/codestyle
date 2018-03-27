# IntelliJ IDEA

(*These instructions are based on IntelliJ 2017.3.4.  They should apply to other recent versions, but some menus or settings may have changed.*)

### Install the Checkstyle plugin

* Install the [IntelliJ IDEA checkstyle plugin](https://plugins.jetbrains.com/plugin/1065-checkstyle-idea), called `CheckStyle-IDEA`
  * File →  Settings →  Plugins
  * Restart IDE
* [Clone](https://help.github.com/articles/cloning-a-repository/) this [repository](https://github.com/duraspace/resources) (so that you have a local copy)
* Configure the plugin to use the DuraSpace `checkstyle.xml`
  * File →  Settings →  Checkstyle
    * In older versions of IntelliJ, this menu may be under File → Settings → Other Settings → Checkstyle
  * Add a "Configuration File" (press the `+` in the table). Select a local copy of the`duraspace-checkstyle.xml` 
  * Make it "Active" by checking the Active box
  * Click Apply

### Set Code Style

There are two ways to sync the IntelliJ Code Style settings with your Checkstyle settings. Importing a pre-configured code style scheme is the simplest and most likely to provide consistent results. If you would prefer more control over your settings, importing the Checkstyle configuration provides a starting point for further tweaking.

#### Option 1: Import Code Style XML

* The simplest way to match the IntelliJ Code Style settings with the Checkstyle configuration is to import the [DuraSpace Code Style settings](duraspace-intellij-java-code-style.xml)
  * File → Settings → Editor → Code Style
  * Select the small gear icon next to "Scheme", select `Import Scheme` → `IntelliJ IDEA code style XML`
  * Select the *duraspace-intellij-java-code-style.xml* (under checkstyle/ide-support in the DuraSpace resources repo directory)
  * Select OK, then Apply, then OK
  * Ensure the `DuraSpace Code Style` Scheme is selected

#### Option 2: Import Checkstyle Configuration 

* Importing Checkstyle configuration, as supported through the Checkstyle plugin, provides a starting point for Code Style configuration
  * File → Settings → Editor → Code Style
  * Select a starting point Scheme from the drop down box. `Default` is a good option if you want a clean start or if you have not yet configured any Code Style settings. Some settings in any Scheme you select will be overwritten when importing the Checkstyle configuration
  * Click the small gear icon next to "Scheme", Select `Import Scheme` → `CheckStyle Configuration`
  * Select the *duraspace-checkstyle.xml* (from the DuraSpace resource repo directory)
  * If prompted for a value for `checkstyle.suppressions.file`, enter the full path to the *duraspace-checkstyle-suppressions.xml* file, which is sitting next to the *duraspace-checkstyle.xml* file
  * Select OK, then Apply, then OK

#### Other Settings

If you want to dig further into configuration (primarily needed if you selected Option 2 above), consider the following settings

* After importing the Checkstyle settings, your "Copyright profiles" may get reset (if you had them previously configured).  If you want IntelliJ to automatically add a copyright statement / license at the top of every Java class, you should ensure this is (re)configured:
  * File → Settings → Editor → Copyright
  * Add a Copyright profile, using the `+` button
  * Set the notice which will appear at the top of all generated code files
  * Select the profile from the *Default project copyright* list
  * Select Formatting and uncheck the option "Add blank line after"
* Verify or set the following settings. These will allow the IDE to properly reformat code for you (when making bulk edits). This is especially important if you plan to do any bulk cleanup of existing code using IntelliJ tools
  * File → Settings → Editor → Code Style → Java → Tabs and Indents
    * Verify that the *Use tab character* is unchecked
    * Set *Tab size*, *Indent*, and *Continuation indent* to 4
  * File → Settings → Editor → Code Style → Java → Spaces
    * Under *Before Left Brace*, UNCHECK *Annotation array initializer left brace*
  * File → Settings → Editor → Code Style → Java → Wrapping and Braces
    * CHECK *Ensure right margin is not exceeded*
    * Set all of the following  to *Wrap if long*:
      * Extends/implements list (also check "align when multiline")
      * Extends/implements keyword
      * Throws list
      * Throws keyword
      * Method declaration parameters (also check "align when multiline")
      * Method call arguments (also check "align when multiline")
      * Chained method calls (also check "align when multiline")
      * "for()" statement (also check "align when multiline")
      * "try-with-resources" (also check "align when multiline")
  * File → Settings → Editor → Code Style → Java → JavaDoc
    * UNCHECK "Generate `<p>` on empty lines"
    * Make sure "Keep empty lines" is checked
  * File → Settings → Editor → Code Style → Java → Imports
    * In the "Import Layout" section, ensure  the settings are in this order
      * "import static all other imports"
      * `<blank line>`
      * "import java.*"
      * "import javax.*"
      * `<blank line>`
      * "import all other imports"

### Fixing existing code

* First, verify that you have either followed Option 1 or  used Option 2 with all Other Settings above
* Open up any Java source file in IntelliJ. You will see Checkstyle warnings appear (if any) in RED. This highlighting is enabled via the checkstyle plugin.
* IntelliJ IDEA [allows you to bulk reformat entire projects or code modules](https://www.jetbrains.com/help/idea/editor-basics.html#reformat_rearrange_code)
  * Right click on a single directory / module
  * Select "Reformat Code"
  * Check "Optimize imports"  (This will remove any import statements with an asterisk)
  * Leave "Rearrange entries" unchecked (This will rearrange methods/variables based on arrangement settings in IDEA. This is not necessary.)
  * Under *Filters* → Check *File Masks* and enter in "*.java, *.xml"  (to ensure bulk reformatting only applies to Java and XML files)
  * Click Run
  * Run Checkstyle against the module. There likely will still be a few failures to fix manually.
    ```shell
    # Either run checkstyle alone
    mvn -U checkstyle:check
    # Or execute the entire build
    mvn clean install 
    ```
  * Fix any errors that are reported before you commit!
