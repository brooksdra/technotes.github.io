# IntelliJ

## Keymaps
![IntelliJ-keymap-macOS.png](images%2FIntelliJ-keymap-macOS.png)

![IntelliJ-keymap-windows-linux.png](images%2FIntelliJ-keymap-windows-linux.png)

![IntelliJ-keymap-windows-linux2.png](images%2FIntelliJ-keymap-windows-linux2.png)

## Things to look into:
Shift + Shift Actions
Logging Non-Suspending Breakpoints
Update all usages to 2022.1
Is there a commit tab for SVN, see Git on personal M1
Check on Tomcat IntelliJ integration for debugging web application
Look into Chrome debugging? With WebStorm
Look into sharing settings between all environments. This will be good for work!
Look into the Tasks bar at the top, it seems to understand files etc.??
Remote debugging.
Checking out from SVN into project with multiple modules.
Check for Maven dependency tracking
 I need to prepare a way to make sure all of the IDEs are configured correctly.

IntelliJ has an embedded tutorial which is pretty nice and covers a lot of stuff
Take a look at this https://www.jetbrains.com/help/idea/migrating-from-eclipse-to-intellij-idea.html

## Shelf Info
The Shelf is workspace specific
Use settings > Version Control > Shelf to set the directory.
I prefer a centralized place /ProtedyneSuite/idea-resources/shelf

## Editor Settings
**Allow Mouse font change** 
To enable/disable the feature, Settings > Editor > General: Change Font size with Ctrl+Mouse Wheel

**Open files with single click** This is called a preview tab and shows italics file names.
Preview tabs do not stay open, are reused until explicitly kept open (eg. via double clicked or editing).
To enable/disable the feature, Settings > Editor > General > Editor Tabs > Enable preview tab checkbox

**Ignoring or changing error checking**
File -> Settings -> search for inspection -> then error message
Unresolved Query brings up JPA, I turned that off
Unresolved Symbol in Java Doc, I turned that down to warning level

**Organize Imports**
File -> Settings -> Editor -> Code Style -> Java -> imports tab
Check Use single class import
Class count to use import with '*' = 999
Names count to use static import with '*' = 999
Import layout should be:
Import static all other imports
<blank line>
java.*
<blank line>
javax.*
<blank line>
org.*
<blank line>
com.*
<blank line>
All other imports

## Subversion
see https://www.jetbrains.com/help/idea/2021.2/enabling-version-control.html  
Right click on a project to see Subversion context menu

Also, there is a Subversion view is where everything winds up.  
To see history, right click on the project select Subversion | Show History. If there are more than 1 repo, the tab will have a dropdown.

New files aren't automatically add to SVN:  
Go to File -> Settings -> Version control -> Confirmation -> When files are created You're probably looking for "Add silently".
Note: In IntelliJ 6 or earlier versions this is done with File -> Settings -> Version control -> General Settings -> Add silently
From <https://stackoverflow.com/questions/2817452/add-a-new-file-in-intellij-doesnt-add-to-subversion> 

Go to File -> Settings -> Version control -> Commit   
Force non-empty commit comments  
Uncheck Analyze code, and Check Todo (Show All)  

**Adding (SVN checkout) a new module to an existing project**  
This is a two step process…

	1) Check project out of SVN
		a. SVN -> Browse VSC Repository -> Browse Subversion Repository
		b. Find exact project or repo in tool view, right click and select Checkout…
		c. In Destination window, select project directory and click OK
		d. In Options window, select project directory/Project Name, typically the second option, and click OK
		e. Keep the 1.8 option and click OK
		f. You will see an option to open project, click [Cancel]
			i. If you click [New Window] open a new workspace only looking at the newly checked out project
			ii. Close that new workspace.
		g. Open project in windows explorer and delete .idea and .iml
	2) Include the new module into the current workspace
		a. In the Projects View of your existing workspace, you should see the new module in your current workspace, but it is not highlighted.
		b. If  .idea and .iml exist, delete them.
		c. File -> New -> Module from existing sources…
		d. Select the pom.xml from the new module and click OK.
		e. Wait for Maven to do its thing.
		

**SVN not mapped to a directory**    
This may happen over time, but if it doesn't   
Preferences | Version Control | Directory Mappings  

**Merging**  
Find the target "eg. upgrade-qa" repo using Subversion Working Copies Information of the Subversion view.  
Press cleanup, then press Merge From…   
Select the appropriate source repo "eg. upgrade-dev"  NOTE: Use Configure Branches for better choices…  
Use Quick Manual Select to find all revisions for that merge.  
Select With Pre-Filter finds all candidates and selects them, not sure how to update the Pre-Filter  
The merge is completed and the commit message auto generated, reformat to our standards.  
From here you can commit or cancel to review the merge.  
If canceled, use the Commit tab of Subversion view to commit Merged from upgrade-dev changes.  
!!! Make sure to select the root of your changes or the commit will be partial !!!  

## Database
The database interface seems okay.  
Can you run directly from code? Ctrl + Enter?  

The following are MariaDB and Mongo localhost database configurations:  
Copy all the way till the end then paste into the Database tab window.   
This will open the setting window and introduce the newest settings.  
Install the Driver and enter the password for each datasource, then push them up to Global.  

#DataSourceSettings#   
#LocalDataSource: MariaDB localhost  
#BEGIN#  
<data-source source="LOCAL" name="MariaDB localhost" uuid="fa8507be-46e5-45da-a0c3-ccaa0b9fa5d3"><database-info product="MariaDB" version="10.3.13-MariaDB-log" jdbc-version="4.2" driver-name="MariaDB Connector/J" driver-version="3.0.7" dbms="MARIADB" exact-version="10.3.13" exact-driver-version="3.0"><extra-name-characters>#@</extra-name-characters><identifier-quote-string>`</identifier-quote-string></database-info><case-sensitivity plain-identifiers="mixed" quoted-identifiers="mixed"/><driver-ref>mariadb</driver-ref><synchronize>true</synchronize><jdbc-driver>org.mariadb.jdbc.Driver</jdbc-driver><jdbc-url>jdbc:mariadb://localhost:3306</jdbc-url><secret-storage>master_key</secret-storage><user-name>engineer</user-name><schema-mapping><introspection-scope><node kind="schema" negative="1"/></introspection-scope></schema-mapping><working-dir>$ProjectFileDir$</working-dir></data-source>  
#END#
   
#LocalDataSource: Mongo localhost  
#BEGIN#  
<data-source source="LOCAL" name="Mongo localhost" uuid="b70069e3-ea4e-47f7-aa26-811cfdecb454"><database-info product="Mongo DB" version="4.2.21" jdbc-version="4.2" driver-name="MongoDB JDBC Driver" driver-version="1.18" dbms="MONGO" exact-version="4.2.21" exact-driver-version="1.18"/><case-sensitivity plain-identifiers="mixed" quoted-identifiers="mixed"/><driver-ref>mongo</driver-ref><synchronize>true</synchronize><jdbc-driver>com.dbschema.MongoJdbcDriver</jdbc-driver><jdbc-url>mongodb://localhost:27017</jdbc-url><secret-storage>master_key</secret-storage><user-name>engineer</user-name><schema-mapping><introspection-scope><node kind="schema" negative="1"/></introspection-scope></schema-mapping><working-dir>$ProjectFileDir$</working-dir></data-source>
#END#

## HTTP REST Interface

## Generate serialVersionUID  
First enable settings Editor>Inspection>JVM>Serializable class without serialVersionUID, this warning will provide a way to generate the serialVersionUID

## Maven
Make sure the settings are in line with all development to point to D:\.m2
MY_MAVEN_OPT AND MAVEN_OPT = -Xms512m -Xmx2048m -XX:MaxMetaspaceSize=512m -Dmaven.repo.local=D:\.m2\repository

## Program Launchers
IDEA has an "Eclipser" plugin to convert Eclipse launcher configuration into IDEA launchers! Locate launchers in project, open, right click and select Convert with Eclipser. This adds a new launch configuration that is ready to go.

## For Debugging 
If not, here is a testing vm args example
-Dspring.profiles.active=dev -Dlog4j.configurationFile=/pro......Suite/bin/config/Log4j2Configuration.xml -Dlogfilename=SystemTesting

## For Unit Testing
If not, here is a testing vm args example
-ea -Dpro.......test.debug=2 -Dpro.......test.test_number=0 -Dpro.......test.use_real_timers=no -Dspring.profiles.active=dev -Dlog4j.configurationFile=/Pro......Suite/bin/config/Log4j2Configuration.xml -Dlogfilename=SystemTesting

## According to Burt
it appears they've broken Java debugging again. The arguments appear to have changed.  
Old:  
    $JAVA_DEBUG_OPTIONS = "-Xdebug", "-Xnoagent", "-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=$DEBUG_PORT"  
That no longer works.  
New:  
    $JAVA_DEBUG_OPTIONS = "-Xdebug", "-Xnoagent", "-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=$DEBUG_PORT"
Until the launcher is changed yet again we will not be able to remote debug.  or you can temporarily hack LaunchSystemGroup.ps1 to get it working.
