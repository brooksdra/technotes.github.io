# Spring Boot

### Typically we launch our SpringBoot jars as follows:
```
java-DSvc="%SVC%-%VERSION%" %JVM_OPTIONS% -jar %~dp0..\lib\%SVC%-%VERSION%.jar
```
<strong>Where:</strong>  
java : Launches the JVM.  
-DSvc="%SVC%-%VERSION%" : A VM option to set an obscure Svc property as a command-line marker making it easy to identify in Window's task manager.  
%JVM_OPTIONS% : Any and all JVM options.  
-jar : -Jar token instructing the JVM to launch according to the META-INF\MANIFEST.MF.  
%~dp0..\lib\%SVC%-%VERSION%.jar : The target jar.  

### If you want to run a different class (that has its own main), the command changes slightly:
```
java -cp %~dp0..\lib\%SVC%-%VERSION%.jar -Dloader.main=com.pro...e.metricsconsumer.apps.RerunErrorMessages org.springframework.boot.loader.PropertiesLauncher
```
<strong>Where:</strong>  
java : Launches the JVM.  
-cp %~dp0..\lib\%SVC%-%VERSION%.jar : The target jar in this case is put on the classpath.  
-DSvc="%SVC%-%VERSION%" : A VM option to set an obscure Svc property as a command-line marker making it easy to identify in Window's task manager.  
%JVM_OPTIONS% : Any and all JVM options.  
-Dloader.main=com.pro...e.metricsconsumer.apps.RerunErrorMessages : A VM option to set system property loader.main to the class targeted to run.  
org.springframework.boot.loader.PropertiesLauncher : The absolute class actually launched that knows how to then launch the loader.main class.  
