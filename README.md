# Parent-pom to compile and package FirstSpirit-modules

The firstspirit-module-parent-pom will be used to generate FirstSpirit modules.

The build process contains several steps to produce a proper FirstSpirit module:

* generate-resources - 
  Generates the content for the module.xml which will be injected into the variables defined in it. More to this in the next section.
* process-resources -
  filters the module.xml and optional the module-isolated.xml inject the dependencies
* package 
  * add all content to the JAR file
  * copy all dependencies to a special folder
  * create a ZIP file as an assembly for the FirstSpirit module structure
    * module.xml
    * optional: module-isolated.xml
    * dependencies
    * generated fsm
  * rename the ZIP file to a FSM
* install -
  attaches the generated FSM file to the local repository
* deploy
* attaches the generated FSM file to the remote repository

### Resource Filtering and module.xml
The parent pom analyse all dependencies and add them to several lists reagrding to the scope of the dependencies.

The general layout of a module(-isolated).xml looks like this:

```xml
<module>
  <name>${project.name}</name>
  <displayName>${project.name}</displayName>
  <version>${project.version}</version>
  <description>${project.description}</description>
  <vendor>${project.organization.name}</vendor>
  <components>
 
  </components>
  <resources>
  ${module.resources.global.legacy}	
  </resources>
 </module>
 ```
 
 ### Usage
 Please use one of the Archetypes to create your module project and add your depenencies and your code.
 
 After you finished your implementation you can use the clean package goals to build your FSM. You can find the result in the target directory
 
 ####Attention
 You need to activate the profile firstspirit-module-create otherwise you will only create JARs instead of FSMs.
 
 #Deprecation Notes:
 
 The profiles firstspirit-module-install and firstspirit-module-uninstall 
 will be replaced by the usage of the FSDevTools and should migrated. They will be removed with the next release.