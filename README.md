## Environment
- IntelliJ IDEA 13.1.1 Community Edition (build number: **135.480**)
- Scala Plugin version **0.33.415**
- JDK version **1.7.40**

## Problem Description
I updated the Scala plugin today, noticed that all of projects with the following characteristics can no longer run from IntelliJ directly.
In `build.sbt`, I set the Scala source to be the root instead of the normal `src/main/scala` path.
It compiles and runs just fine using SBT console
```shell
sbt run
# It should print 'hello world' to the screen
```

## Steps to reproduce
- Import this project as a `SBT Project`
- Open `HelloWorld` within IntelliJ
- Right click within the editor
- Select `Run 'HelloWorld'`
- We get the following exception in the `Run` tab
```
Exception in thread "main" java.lang.ClassNotFoundException: HelloWorld
	at java.net.URLClassLoader$1.run(URLClassLoader.java:366)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:355)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.net.URLClassLoader.findClass(URLClassLoader.java:354)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:425)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:308)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:358)
	at java.lang.Class.forName0(Native Method)
	at java.lang.Class.forName(Class.java:190)
	at com.intellij.rt.execution.application.AppMain.main(AppMain.java:113)

Process finished with exit code 1
```
- Right click on the module `intellij-scala-bug`
- Hover `New`
- There is no option of adding a Java or Scala class

## Notes
- These issues did not occur with the previous version of Scala plugin
- Under `Project Structure...`, the root directory is not marked automatically as `Source Folders`
- Once I manually mark the root directory as the `Source Folders`, the problem is resolved
