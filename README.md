# MavenForMe
# Compile a Java Code
  Javac HelloWorld.java ---> HelloWorld.class  

# Run the java Code
Java HelloWorld  

# Create a jar file out of this 
Jar cf myjar.jar HelloWorld.class //cf stands for create file  

# Run the java class with jar file
Java -classpath myjar.jar HelloWorld  
Java -cp target/helloworld-1.0-SNAPSHOT.jar  com.intuit.ParallelTest  

# Group ID in Pom is the reverse of domain of a given org usually
# ArtifactId  is the project name
# 3.2.1-SNAPSHOT ..snapshot tells maven that this is a development version

# Fat Jar
Dependent jars will be included in the main jar.  

# Repositories
  Local -  <userhome>/.me    
  Central - maven central  
  Remote - Other public/private locations  
# Effective POM
  This is the super pom file that has other config related details.
 # Maven Build Lifecycles
  Clean  
  Goal : clean  
    Removes everything from the target directory  
  Default    
    Clean - cleans the target directory   
    Validate -verify project is correct   
    Compile - Compile the project source code  
    Test- Test the project source code  
    Package - Package compiled files to packaging type( jar, war, etc)  
    Verify - Run Integrated Tests   
    Install - Install to local maven Repository (At this step jar file will be available)  
    Deploy - Deploy to shared maven repository  
  Site  

# Maven Archetype
  Archetype is a project template  

# Plugin
## Compiler
	Goals  
		1. Compiler:compile  //for compiling files in src/main/java  
		2. Compiler:test-compile  //for compiling files in src/test/java  
## Resources
	Goals  
		1. Resources:resources  
		2. Resources:testresources  
		3. Resources:copy-resources  
## SureFire Plugin
	Goal  
		Surefire:test  
## Maven Jar Plugin
	Goal 
		Jar:jar  
# Transitive Dependencies
  Transitive Dependencies. Ctrl+click navigates you to pom file of a particular dependency that has its own internal dependencies  

# Scope
  Compile - is default scope  
  Test --jar is available only for test source code  
  Runtime -jar will be available only at runtime  
  <version>[4.1,4.5]</version> //to use a jar file between 4.1 and 4.5 versions both values inclusive
  <version>[4.1,4.5)</version> //to use a jar file between 4.1 and 4.5 4.5 is exclusive

# Effective Pom - is  a super pom
	1. Maven -->build --> help:effective-pom -Doutput=effective-pom.xml //here help is compiler and effective-pom is goal and output is parameter 
	2. Maven -->build --> help:effective-settings-Doutput=effective-settings.xml 


# Super pom - Effect pom is by default the super pom 
## Pom inheritance
	1. Dependency management  
		1. For maven to manage all the jars from parent pom, we have add <dependencyManagement> section in parent pom.  
		2. The child module should have <parent> tag and parents maven coordinates in it for this to work.  
		3. If no groupid and artifact id are declared in child pom, by default all jars from parent are available in child modules.  
		4. If child module needs a different version of jar than the parent pom, then the child pom should also declare the maven coordinates (groupid, artifactid & version) so that it can have its own version.  
# Settings.xml
	Windows--Preferences->userSettings  
 To do Project Aggregation, you must do the following:  
	1. Change the parent POMs packaging to the value "pom" .  
	2.  Specify in the parent POM the directories of its modules (children POMs)  
	3. Include a dependency management element  
	4. Add parent tag in the child modules  
	5. Simply adding dependency in parent pom under dependency management will not add dependencies to child module by default. We should provide the dependeny in child module as well without version if we want to inherit the version from parent or with version if we want separate versions   
Note :  
	1. If you have depedendencyManagement Tag in parent pom, then its mandatory to declare the dependencies (maven coordinates) in child pom as well, version can be optional. It is also mandatory to declare parent tag with parent maven coordinates in the child pom  
	2. If you don't have dependency management tag in parent pom, all the dependencies declared in parent pom will be auto inherited to child pom even if the dependencies are not declared in child poms.  
	

# Properties
We can include properties under properties tag.   
For Ex: 
    1 	<properties>  
    2 	<java.compiler.version>1.8</java.compiler.version>  
    3 	</properties>  
The property can be retrieved by ${java.compiler.version}  

# Add Modules
Click on pom.xml-->Overview-->Under modules click Add and select modules.   
This will create modules in pom.xml  

Parent tag helps in achieving inheritance between poms  
Module tag helps in aggregation implicit child module builds when parent pom is built  

And this is done by reactor.  

# Linking up External Repository
	1. Add a <distributionManagement<snapshotrepository><id><url> Section in the pom.xml  
	2. Add a <servers><server><id><username><password> for authenticating the above url in distributionmanagement- in settings.xml, id here should match with snapshot/release #    repository id  
	3. Right click and run with maven goal --> deploy  
	4. The artifacts (snapshots.jar) will be uploaded to external repository  
# Execute a main method from test source directory
test-compile is to compile classes in test source directory
-Dexec.classpathScope="test" is important to execute this method successfully
```
mvn test-compile exec:java -Dexec.mainClass="makemytrip.Main" -Dexec.classpathScope="test"
```
