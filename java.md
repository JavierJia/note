# About static block statement
Basically, the static block is a block of code called before class created

    static {}

The {} block is a block of code that will instill into constructor. Everytimes we call the constructor, that piece of code will be called once.

Detailed explaination:
http://www.jusfortechies.com/java/core-java/static-blocks.php

# JNI
Java Native Interface
http://www.ntu.edu.sg/home/ehchua/programming/java/JavaNativeInterface.html

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

