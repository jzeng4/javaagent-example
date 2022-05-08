# javaagent-example
Example of how to instrument the java class files on class loading.
AOPTransformer will transform target class to print "before invoke" when invoke methods.
You can change(instrument) the byte code without changing the java source file and recompiling. 
# Usage
Package the agent jar file.
```
mvn clean package
```

Find the packaged jar file in target directory and add it to the java command line options.
For example.
```$xslt
java -javaagent:./target/javaagent-1.0-SNAPSHOT-jar-with-dependencies.jar com.lzy.javaagent.Test
```

or run in idea and add vm options.

Have Fun!


Call stack for class transformer:

```
javassist.CannotCompileException: no method body
	at javassist.CtBehavior.insertBefore(CtBehavior.java:744)
	at javassist.CtBehavior.insertBefore(CtBehavior.java:734)
	at com.lzy.javaagent.AOPTransformer.transform(AOPTransformer.java:51)
	at java.instrument/java.lang.instrument.ClassFileTransformer.transform(ClassFileTransformer.java:246)
	at java.instrument/sun.instrument.TransformerManager.transform(TransformerManager.java:188)
	at java.instrument/sun.instrument.InstrumentationImpl.transform(InstrumentationImpl.java:563)
	at java.base/java.lang.ClassLoader.findBootstrapClass(Native Method)
	at java.base/java.lang.ClassLoader.findBootstrapClassOrNull(ClassLoader.java:1258)
	at java.base/java.lang.System$2.findBootstrapClassOrNull(System.java:2134)
	at java.base/jdk.internal.loader.ClassLoaders$BootClassLoader.loadClassOrNull(ClassLoaders.java:118)
	at java.base/jdk.internal.loader.BootLoader.loadClassOrNull(BootLoader.java:116)
	at java.base/jdk.internal.loader.BootLoader.loadClass(BootLoader.java:124)
	at java.base/java.lang.Class.forName(Class.java:476)
	at java.base/java.util.ResourceBundle$ResourceBundleProviderHelper.lambda$loadResourceBundle$1(ResourceBundle.java:3601)
	at java.base/java.security.AccessController.doPrivileged(Native Method)
	at java.base/java.security.AccessController.doPrivileged(AccessController.java:430)
	at java.base/java.util.ResourceBundle$ResourceBundleProviderHelper.loadResourceBundle(ResourceBundle.java:3602)
	at java.base/java.util.ResourceBundle.loadBundle(ResourceBundle.java:1844)
	at java.base/java.util.ResourceBundle.findBundle(ResourceBundle.java:1774)
	at java.base/java.util.ResourceBundle.findBundle(ResourceBundle.java:1728)
	at java.base/java.util.ResourceBundle.findBundle(ResourceBundle.java:1728)
	at java.base/java.util.ResourceBundle.getBundleImpl(ResourceBundle.java:1662)
	at java.base/java.util.ResourceBundle.getBundleImpl(ResourceBundle.java:1582)
	at java.base/java.util.ResourceBundle.getBundleImpl(ResourceBundle.java:1556)
	at java.base/java.util.ResourceBundle.getBundle(ResourceBundle.java:857)
	at java.base/sun.launcher.LauncherHelper$ResourceBundleHolder.<clinit>(LauncherHelper.java:124)
	at java.base/sun.launcher.LauncherHelper.getLocalizedMessage(LauncherHelper.java:452)
	at java.base/sun.launcher.LauncherHelper.abort(LauncherHelper.java:616)
	at java.base/sun.launcher.LauncherHelper.loadMainClass(LauncherHelper.java:776)
	at java.base/sun.launcher.LauncherHelper.checkAndLoadMain(LauncherHelper.java:655)
```
