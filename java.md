# About static block statement
Basically, the static block is a block of code called before class created

    static {}

The {} block is a block of code that will instill into constructor. Everytimes we call the constructor, that piece of code will be called once.

Detailed explaination:
http://www.jusfortechies.com/java/core-java/static-blocks.php

# JNI
Java Native Interface
http://www.ntu.edu.sg/home/ehchua/programming/java/JavaNativeInterface.html
## Don't forget to call ReleaseXXX() with a mode of 0 (copy back and free the memory) for each GetXXX() call.

# Commandline parser

	private static Options createCommandLineOptions() {
		final Options options = new Options();
		options.addOption("action", true, "Build index or Query");
		options.addOption("querytype", true, "Exact search or Fuzzy search");
		options.addOption("help", false, "Show help information.");
		options.addOption("geo", false, "using geo file");

		options.addOption(
				"verbose",
				true,
				"verbose level, \n\t\t0\tperformance\n\t\t1\tprint result\n\t\t2\t print detail");
		options.addOption("topk", true, "topk result required by each query");
		options.addOption("limit", true,
				"limit number of queries, the left query will not executed");
		options.addOption("ed", true,
				"edit distance for fuzzy search, default 1");
		options.addOption("radius", true,
				"radius number fo geo search, default 0.25");
		return options;
	}

	private static void outputCommandLineHelp(final Options options) {
		final HelpFormatter formater = new HelpFormatter();
		formater.printHelp("The SampleCLI demonstrates the use of CLI.",
				options);
	}

	private static void processCommandline(final CommandLine cl)
			throws IllegalArgumentException {
		if ((null != cl) && cl.hasOption("port")) {
			// do something with port
		}
		if ((null != cl) && cl.hasOption("id")) {
			// do something with id
		}
		if ((null != cl) && cl.hasOption("filter")) {
			// do something with filter
		}
		if ((null != cl) && cl.hasOption("details")) {
			// do something with details
		}
		if ((null != cl) && cl.hasOption("jar_files")) {
			// do something with jar_files
		}
	}

	public static void main(final String[] args) {
		// Parse command line
		final Parser commandlineparser = new PosixParser();
		final Options options = createCommandLineOptions();
		CommandLine cl = null;
		try {
			cl = commandlineparser.parse(options, args, true);
		} catch (final ParseException exp) {
			Logger.error("Unexpected exception:" + exp.getMessage());
		}
		// Process command line and store parameter in attributes
		try {
			if (null != cl) {
				processCommandline(cl);
			}
		} catch (final IllegalArgumentException e) {
			outputCommandLineHelp(options);
			Logger.error("Illegal arguments on command line: " + e.getMessage());
			return;
		}
		if ((null != cl) && cl.hasOption("help") || args.length < 1) {
			outputCommandLineHelp(options);
			return;
		}
	}

# Date format
    
    new SimpleDateFormat("HH:mm").format(new Date())

## Good JNI tutorials:

http://www.ibm.com/developerworks/library/j-jni/

http://www.ibm.com/developerworks/java/tutorials/j-jni/

http://www.ibm.com/developerworks/training/kp/j-kp-jni/

http://publib.boulder.ibm.com/infocenter/javasdk/v5r0/index.jsp?topic=%2Fcom.ibm.java.doc.diagnostics.50%2Fdiag%2Funderstanding%2Fjni_refs.html


# Java regex
Good reference: http://www.vogella.com/articles/JavaRegularExpressions/article.html

Pattern and Matcher can find each match part like this:
```Java
public static void main(String[] args) {
    Pattern pattern = Pattern.compile("\\w+");
    // In case you would like to ignore case sensitivity you could use this
    // statement
    // Pattern pattern = Pattern.compile("\\s+", Pattern.CASE_INSENSITIVE);
    Matcher matcher = pattern.matcher(EXAMPLE_TEST);
    // Check all occurance
    while (matcher.find()) {
        System.out.print("Start index: " + matcher.start());
        System.out.print(" End index: " + matcher.end() + " ");
        System.out.println(matcher.group());
    }
    // Now create a new pattern and matcher to replace whitespace with tabs
    Pattern replace = Pattern.compile("\\s+");
    Matcher matcher2 = replace.matcher(EXAMPLE_TEST);
    System.out.println(matcher2.replaceAll("\t"));
}
```

# JNI exception:
##JNI WARNING: expected return type 'L'
e.g. the return type is "boolean", we are using "CallObjectMethod" then it will give you a warning.
Change to "CallBooleanMethod" will solve the problem. 

# Generate JNI function declarations
reference: http://thebreakfastpost.com/2012/01/23/wrapping-a-c-library-with-jni-part-1/
```
$ javac org/vamp_plugins/*.java
$ javah -jni org.vamp_plugins.Plugin org.vamp_plugins.PluginLoader
```

# JNI return local reference:
follow this :http://android-developers.blogspot.com/2011/11/jni-local-reference-changes-in-ics.html
```
static jobjectArray MyClass_returnArray(JNIEnv* env, jclass) {
    env->PushLocalFrame(256);
    jobjectArray array = env->NewObjectArray(128, gMyClass, NULL);
    for (int i = 0; i < 128; ++i) {
        env->SetObjectArrayElement(array, i, newMyClass(i));
    }
    env->PopLocalFrame(NULL); // Error: should pass 'array'.
    return array; // Error: array is no longer valid.
}
```


# JNI cache the jclass and jmethod by static call and static variables
reference :http://stackoverflow.com/questions/10617735/in-jni-how-do-i-cache-the-class-methodid-and-fieldids-per-ibms-performance-r

# Create Jar file:
```
jar cf jar-file input-file(s)
```

# About the InnerClass
An instance of InnerClass can exist only within an instance of OuterClass and has direct access to the methods and fields of its enclosing instance. The next figure illustrates this idea.

and:

A nested class is a member of its enclosing class. Non-static nested classes (inner classes) have access to other members of the enclosing class, even if they are declared private. Static nested classes do not have access to other members of the enclosing class. As a member of the OuterClass, a nested class can be declared private, public, protected, or package private. (Recall that outer classes can only be declared public or package private.)

# HashMap loop:
Loop keys:
```
Map<String, Object> map = ...;

for (String key : map.keySet()) {
        // ...
}

//If you only need the values, use values():
for (Object value : map.values()) {
        // ...
}

//Finally, if you want both the key and value, use entrySet():

for (Map.Entry<String, Object> entry : map.entrySet()) {
        String key = entry.getKey();
        Object value = entry.getValue();
        // ...
}
```

# Eclipse sidebar setting in ubuntu:

```bash
sudo ln -s ~/Downloads/eclipse /usr/lib/
sudo ln -s /usr/lib/eclipse/eclipse /usr/bin/eclipse
sudo vi  /usr/share/applications/eclipse.desktop
```
Copy these lines to that eclipse.desktop file
```
[Desktop Entry]
Version=4.3
Name=Eclipse
GenericName=Text Editor

Exec=eclipse
Terminal=false
Icon=/usr/lib/eclipse/icon.xpm
Type=Application
Categories=IDE;Development
X-Ayatana-Desktop-Shortcuts=NewWindow

[NewWindow Shortcut Group]
Name=New Window
Exec=eclipse -n
TargetEnvironment=Unity
```

