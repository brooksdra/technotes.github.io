#SVN

From directory C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\PatientInventoryInterface\src\main\java\com\pro......\patientInventory

### shows entire file
`svn annotate -v PatientInventorySystem.java`
```
     2        gbs 2017-04-10 18:04:34 -0400 (Mon, 10 Apr 2017)
  4381        drb 2020-07-30 18:41:17 -0400 (Thu, 30 Jul 2020)         if (iEnv.isConfigurationOPI()) {
  4380        drb 2020-07-30 18:14:17 -0400 (Thu, 30 Jul 2020)             simulationSupporter = new SimulationSupportOpi();
  6415        drb 2021-01-04 19:49:53 -0500 (Mon, 04 Jan 2021)             getApplicationContext().getAutowireCapableBeanFactory().autowireBean(simulationSupporter);
  4380        drb 2020-07-30 18:14:17 -0400 (Thu, 30 Jul 2020)         }
  4381        drb 2020-07-30 18:41:17 -0400 (Thu, 30 Jul 2020)         else if (iEnv.isConfigurationPPA()) {
  4381        drb 2020-07-30 18:41:17 -0400 (Thu, 30 Jul 2020)             simulationSupporter = new SimulationSupportPPA();
  4380        drb 2020-07-30 18:14:17 -0400 (Thu, 30 Jul 2020)         }
  4380        drb 2020-07-30 18:14:17 -0400 (Thu, 30 Jul 2020)         else {
  4380        drb 2020-07-30 18:14:17 -0400 (Thu, 30 Jul 2020)             simulationSupporter = new SimulationSupport();
  4380        drb 2020-07-30 18:14:17 -0400 (Thu, 30 Jul 2020)         }
  4380        drb 2020-07-30 18:14:17 -0400 (Thu, 30 Jul 2020)
     2        gbs 2017-04-10 18:04:34 -0400 (Mon, 10 Apr 2017)         ObjectName name = new ObjectName("com.pro......." + getSystemName() + ":type=Simulation");
...
```
    
### Show a specific revision:
```
svn log -c 6415 PatientInventorySystem.java    
------------------------------------------------------------------------
 r6415 | drb | 2021-01-04 19:49:53 -0500 (Mon, 04 Jan 2021) | 1 line

[daveb] I-43038 Reinstate default purge settings, Update getTubesInPuck* routines to include WB and Storage pucks, Bring simulator inline with new simulatorId logic with new OPI queries, Update verbose simulator counts, Fix simulator empty generation, Correct session and puck handling.
------------------------------------------------------------------------
```

### Show a specific revision with all involved files:
`svn log -c 6415 -v PatientInventorySystem.java`
```
------------------------------------------------------------------------
r6415 | drb | 2021-01-04 19:49:53 -0500 (Mon, 04 Jan 2021) | 1 line
Changed paths:
   M /branches/propel-4.x-dev/CilaSpaceCommons/src/main/java/com/pro....../commons/patientinventory/PurgeTriggerGenerator.java
   M /branches/propel-4.x-dev/CilaSpaceCommons/src/main/java/com/pro....../commons/puck/PuckService.java
   M /branches/propel-4.x-dev/CilaSpaceCommons/src/main/java/com/pro....../commons/simulatorrecord/SimulatorRecordService.java
   M /branches/propel-4.x-dev/CilaSpaceCommons/src/main/java/com/pro....../commons/tubes/specimen/SpecimenTubeService.java
   M /branches/propel-4.x-dev/CilaSpaceCommons/src/main/resources/hibernate/config/spacedb/SpecimenTube.xml
   M /branches/propel-4.x-dev/PatientInventoryInterface/launchers/PatientInventory OPI.launch
   M /branches/propel-4.x-dev/PatientInventoryInterface/src/main/java/com/pro....../patientInventory/PatientInventorySystem.java
   M /branches/propel-4.x-dev/PatientInventoryInterface/src/main/java/com/pro....../patientInventory/model/SimulationSupport.java
   M /branches/propel-4.x-dev/PatientInventoryInterface/src/main/java/com/pro....../patientInventory/model/SimulationSupportOpi.java
   M /branches/propel-4.x-dev/PatientInventoryInterface/src/main/java/com/pro....../patientInventory/natives/AddSimulationToSpace.java
   M /branches/propel-4.x-dev/PatientInventoryInterface/src/main/java/com/pro....../patientInventory/simulator/PuckSimulatorOpi.java
   M /branches/propel-4.x-dev/PatientInventoryInterface/src/main/java/com/pro....../patientInventory/simulator/PuckSimulatorOpiStorage.java

[daveb] I-43038 Reinstate default purge settings, Update getTubesInPuck* routines to include WB and Storage pucks, Bring simulator inline with new simulatorId logic with new OPI queries, Update verbose simulator counts, Fix simulator empty generation, Correct session and puck handling.
------------------------------------------------------------------------
```

### For the last 10 commits
`Svn log –limit 10`


`svn diff -c 6415 PatientInventorySystem.java`
```
Index: PatientInventorySystem.java
===================================================================
--- PatientInventorySystem.java (revision 6414)
+++ PatientInventorySystem.java (revision 6415)
@@ -179,6 +179,7 @@

         if (iEnv.isConfigurationOPI()) {
             simulationSupporter = new SimulationSupportOpi();
+            getApplicationContext().getAutowireCapableBeanFactory().autowireBean(simulationSupporter);
         }
         else if (iEnv.isConfigurationPPA()) {
             simulationSupporter = new SimulationSupportPPA();
```

### Get the status of a workspace project:
`svn status C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace`   
```            
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\AliquotCapperSystem\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\AliquotCapperSystem\.settings\org.eclipse.jdt.apt.core.prefs
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\BastinFeederSystem\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\CilaScriptEngine\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\CilaSpaceCommons\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\ConveyorSystem\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\InstallationControllerSystem\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\LaserEscapementSystem\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\LaserMarker\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\MasterSealerSystem\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\MasterWasterSystem\.factorypath
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\PatientInventoryInterface\.factorypath
M       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\PatientInventoryInterface\launchers\Launch-InstallationMonitor1.launch
?       C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\PipettorEscapementSystem\.factorypath
…
```

### Get the status of a workspace project with incoming updates:
`svn status --show-updates` 
`Status against revision: 2856`

### Update a workspace project:
`svn update C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace`
```
Updating 'C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace':
U    C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\InstallationControllerSystem\bin\HelpCopyToLocalFromDHCP.bat
U    C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\InstallationControllerSystem\bin\config\Raritan1\ConfiguredSystems.xml
U    C:\Pr.......Suite\vscode-propel-upgrade-dev\CilaSpace\PipettorEscapementSystem\src\main\java\com\pro......\pipettor\PipettorOutfeedEscapement.java
Updated to revision 7967.
```

### Compare the local (in this case QA) branch with a range of revisions from different (dev) branch:
`svn diff -r7972:7974 svn://svn.pro.......pro.......com/Propel/branches/upgrade-dev`
```
Index: CilaScriptEngine/src/test/resources/config/lilyConnectionManager.xml
===================================================================
--- CilaScriptEngine/src/test/resources/config/lilyConnectionManager.xml        (revision 7972)
+++ CilaScriptEngine/src/test/resources/config/lilyConnectionManager.xml        (revision 7974)
@@ -2,7 +2,7 @@
 <lilyConnectionManager>
        <lily api="capi5-0/xmlCall.capi" duration="2" ip="172.16.100.114" port="8080"/>
        <RTI refreshMinutes="2"/>
-       <jdbc context="lily5-0?autoReconnect=true" driver="org.mariadb.jdbc.Driver" maxActive="0" maxWait="1000" password="pro......" port="3306" protocol="jdbc:mysql" userName="root"/>
+       <jdbc context="lily5-0?autoReconnect=true" driver="org.mariadb.jdbc.Driver" maxActive="0" maxWait="1000" password="pro......" port="3306" protocol="jdbc:mariadb" userName="root"/>
        <otherIp ip="localhost:8080" name="TipFeeder"/>
        <otherIp ip="172.14.0.0" name="Decapper"/>
        <otherIp ip="172.14.0.0" name="Pouroff"/>
Index: CilaSpaceCommons/bin/config/properties/databaseConnection-local.properties
===================================================================
--- CilaSpaceCommons/bin/config/properties/databaseConnection-local.properties  (revision 7972)
+++ CilaSpaceCommons/bin/config/properties/databaseConnection-local.properties  (revision 7974)
@@ -6,7 +6,7 @@
 # SSDB schema
 #
 db.ssdb.driver=org.mariadb.jdbc.Driver
-db.ssdb.url=jdbc:mysql://127.0.0.1:3306/SSDB
+db.ssdb.url=jdbc:mariadb://127.0.0.1:3306/SSDB
 db.ssdb.user=engineer
 db.ssdb.pass=pro......
```

### Show eligible merge revisions between two branches (Thanks to Thomas)
`svn mergeinfo --show-revs=eligible --log -r1:HEAD svn://svn.pro.......pro.......com/CilaEnterprise/PropelDataServices/branches/{propeldataservices-dev,propeldataservices-qa} | grep '^r' | grep 'drb'`
```
r4339 | drb | 2022-06-20 13:24:28 -0400 (Mon, 20 Jun 2022) | 1 line
r4343 | drb | 2022-06-20 14:35:36 -0400 (Mon, 20 Jun 2022) | 1 line
```

### Merge those changes even if SVN things they were already merged. 
`svn merge -r7972:7974 svn://svn.pro.......pro.......com/Propel/branches/upgrade-dev`
```
In this case, the merge information was incorrect, so there was nothing to merge??? This was a problem with the branch, see next command to overcome.
--- Recording mergeinfo for merge of r7973 through r7974 into '.':
 U   .
```

### Try --ignore-ancestry if there is a nothing to merge.
`svn merge --ignore-ancestry -r7972:7974 svn://svn.pro.......pro.......com/Propel/branches/upgrade-dev`
```
--- Merging r7973 through r7974 into '.':
U    CilaScriptEngine\src\test\resources\config\lilyConnectionManager.xml
U    CilaSpaceCommons\bin\config\properties\databaseConnection-local.properties
U    CilaSpaceCommons\bin\config\properties\databaseConnection-opiqa.properties
U    CilaSpaceCommons\bin\config\properties\databaseConnection-opiqalocal.properties
U    CilaSpaceCommons\bin\config\properties\databaseConnection-production.properties
U    CilaSpaceCommons\bin\config\properties\dialogConnection-local.properties
U    CilaSpaceCommons\bin\config\properties\dialogConnection-opiqa.properties
U    CilaSpaceCommons\bin\config\properties\dialogConnection-production.properties
… 
```

### To revert all local changes (You can be as specific as the path provided to the command):
`svn revert -R .`
```
Reverted 'CilaSpaceCommons\bin\config\properties\dialogConnection-opiqa.properties'
Reverted 'CilaSpaceCommons\bin\config\properties\databaseConnection-opiqa.properties'
Reverted 'CilaSpaceCommons\bin\config\properties\dialogConnection-production.properties'
Reverted 'CilaSpaceCommons\bin\config\properties\databaseConnection-opiqalocal.properties'
Reverted 'CilaSpaceCommons\bin\config\properties\dialogConnection-local.properties'
Reverted 'CilaSpaceCommons\bin\config\properties\databaseConnection-production.properties'
Reverted 'CilaSpaceCommons\bin\config\properties\databaseConnection-local.properties'
Reverted 'CilaScriptEngine\src\test\resources\config\lilyConnectionManager.xml'
…
```

### Check out a revision
`svn checkout -r 3940 svn://svn.pro.......pro.......com/CilaEnterprise/CilaCommons/branches/cilacommons-dev`

