VarexJ
======

Highly-configurable systems allow users to achieve their specific needs. Such software systems are flexible, but come with difficulties for program analyses, as it is usually not possible to test all combinations of options separately due to the configuration space explosion.  Variability-aware approaches exploit redundancies among configurations to share analysis efforts. Variability-aware execution aggressively shares computations and data in program execution across multiple configurations, for example, when executing a test over all configurations. By maximizing sharing, the approach can outperform traditional approaches by orders of magnitude on many highly-configurable systems, without falling back to incomplete sampling strategies.  We investigate and evaluate the impact of interactions on sharing and scalability to current testing approaches using several small benchmark programs. We show that sharing reduces the number of executed instructions significantly, while the effort to execute them usually stays low. We applied VarexJ to several larger real-world applications to  illustrate typical sharing potential in real-world applications. Finally, we found that options high interact on data in these systems, but only local, orthogonal and rare.

VarexJ is based on Java Pathfinder v7.0 (rev 1155+) see: http://javapathfinder.sourceforge.net/.

JDK 7 is required.


Build
-----

Import the project into eclipse.

If it does not build automatically, right-click on the build.xml \ run as \ Ant BUild
The build process has to be run with JDK 7, JRE will not work.


JPF options
-----------

Variability-Aware options:

* set feature expression [SAT, BDD]
	`factory=BDD`
* set choice type [TreeChoice, MapChoice]
	`choice=TreeChoice`
* define constraints of the application with a dimacs file can be created with FeatureIDE (http://fosd.net/fide):
	`featuremodel="path"\model.dimacs`
* set method frame [StackHandler] (currently only one type supported)

Specify conditional boolean fields
----------------------------------

	import gov.nasa.jpf.annotation.Conditional;

	@Conditional
	static FEATURE = true;

FEATURE is used as if it has both values true and false. 

Run VarexJ
----------

a) as test: see test package "cmu.*", it contains several examples for variability-aware execution

b) as JVM via command line:

`java -jar ..\RunJPF.jar +native_classpath=.."path to VarexJ"\lib\* +search.class=.search.RandomSearch +featuremodel="path to the feature model"\model.dimacs +choice=TreeChoice +factory=BDD +classpath="path to the application"\bin\ A.B.Main args `

