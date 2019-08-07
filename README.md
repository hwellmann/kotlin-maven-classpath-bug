# https://youtrack.jetbrains.com/issue/KE-344

A test class in a project cannot be run from Eclipse when the test class depends on a class of the main source folder of the same project.

This is a standard scenario when working with Maven (same issue with Gradle), which makes the Kotlin Eclipse plugin unusable for any serious work.

Reproducer: https://github.com/hwellmann/kotlin-maven-classpath-bug

Reproduction steps:

* Clone the project and import it into Eclipse.
* Try to run the JUnit test class demo.BrokenTest: the menu entry Run As | Kotlin JUnit Test is missing.
* Comment the Foo() statement in the test class and try again. The menu entry is present, and the test class can be run.
* Uncomment Foo() and clean the project (via menu Project | Clean)
* Run the test again. The run fails with `java.lang.ClassNotFoundException: demo.BrokenTest`
* The console view org.jetbrains.kotlin.ui.console has a message `ERROR: Unresolved reference: Foo (9, 9)`

I suspect that https://youtrack.jetbrains.com/issue/KE-268 is the root cause for this issue.
