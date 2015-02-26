# [Learning Scala](http://techbus.safaribooksonline.com/book/programming/scala/9781449368814)

## [Chapter 1. Getting Started with the Scalable Language](http://techbus.safaribooksonline.com/book/programming/scala/9781449368814/idot-core-scala/ch01_html)

### Notes

1. Installing Java 1.8 (Failed attempt)

    1. Install Homebrew "java" Cask (Take 1)
    
            $ brew cask install java
            ==> We need to make Caskroom for the first time at /opt/homebrew-cask/Caskroom
            ==> We'll set permissions properly so we won't need sudo in the future
    
        Doh!  That won't work.  Don't have the root password on my Mac!
        
    1. Use writable "caskroom" directory, and try again (Take 2)

            $ export HOMEBREW_CASK_OPTS="--caskroom=~/homebrew/Caskroom"
            $ brew cask install java
            Error: undefined method `cask' for main:Object
            Please report this bug:
                https://github.com/caskroom/homebrew-cask/issues
            /Users/keelerh/homebrew/Library/Taps/caskroom/homebrew-cask/Casks/java.rb:1
            /System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/lib/ruby/1.8/rubygems/custom_require.rb:31:in `gem_original_require'
            /System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/lib/ruby/1.8/rubygems/custom_require.rb:31:in `require'
            ...
            
        Hmmm.  Looks like a Homebrew issue.
        
    1. Update `brew-cask` and try again (Take 3) 
    
            $ brew update && brew upgrade brew-cask && brew cleanup && brew cask cleanup
            $ brew cask install java
            ==> Caveats
            This Cask makes minor modifications to the JRE to prevent issues with
            packaged applications, as discussed here:

                https://bugs.eclipse.org/bugs/show_bug.cgi?id=411361

            If your Java application still asks for JRE installation, you might need
            to reboot or logout/login.

            Installing this Cask means you have AGREED to the Oracle Binary Code
            License Agreement for Java SE at

                http://www.oracle.com/technetwork/java/javase/terms/license/index.html

            ==> Downloading http://download.oracle.com/otn-pub/java/jdk/8u31-b13/jdk-8u31-macosx-x64.dmg
            ######################################################################## 100.0%
            ==> Running installer for java; your password may be necessary.
            ==> Package installers may write to any location; options such as --appdir are ignored.
            Password:
            
        Dammit!  Blocked again, and no way around this without help from the Helpdesk.
        
        I'll come back to this.  For now, Scala seems to run fine under the Java 1.6.x install on my Mac.
            
        **Note:** Upgrade instructions from [Updating/Upgrading the Homebrew-cask Tool](https://github.com/caskroom/homebrew-cask/blob/master/USAGE.md#updatingupgrading-the-homebrew-cask-tool)
    
    
1. Installing Scala

        $ brew install scala
        $ scala -version
        Scala code runner version 2.11.4 -- Copyright 2002-2013, LAMP/EPFL
        
        Well, at least the `scala` install works without issue over Homebrew.

### Exercises

1. Although println() is a good way to print a string, can you find a way to print a string without println? Also, what kinds of numbers, strings, and other data does the REPL support?

2. In the Scala REPL, convert the temperature value of 22.5 Centigrade to Fahrenheit. The conversion formula is cToF(x) = (x * 9/5) + 32.

    **Answer:** Complete
    ```scala
    scala> val f = (22.8 * (9.0/5.0)) + 32
    f: Double = 73.03999999999999
    ```

3. Take the result from exercise 2, halve it, and convert it back to Centigrade. You can use the generated constant variable (e.g., “res0”) instead of copying and pasting the value yourself.
 

    **Answer:** Complete
    ```scala
    scala> val halfedC = ((f/2) - 32) * (5.0/9.0)
    halfedC: Double = 2.511111111111109
    ```

4. The REPL can load and interpret Scala code from an external file with the :load <file> command. Create a new file named Hello.scala and add a command that will print a greeting, then execute it from the REPL.
 
    **Answer:** Complete
    ```
    cd scala/books/learning-scala/exercises/
    echo 'println("Hello!")' > ch1e4.scala
    scala
    
    scala> :load ch1e4.scala
    Loading ch1e4.scala...
    Hello!
    ```

5. Another way to load external Scala code is to paste it into the REPL in “raw” mode, where the code is compiled as if it were actually in a proper source file. To do this, type :paste -raw, hit Return, and then paste the contents of your source file from exercise 4. After exiting “paste” mode you should see the greeting.

    **Answer:** Incomplete
    
    1. Try to just paste is "as-is", but it failed.  Apparently REPL code ain't good enough.
        ```scala
        scala> :paste -raw
        // Entering paste mode (ctrl-D to finish)

        println("Hello!")

        // Exiting paste mode, now interpreting.

        <pastie>:1: error: expected class or object definition
        println("Hello!")
        ^
        There were compilation errors!
        ```
    
    1. Poked around SO and found http://stackoverflow.com/questions/15791856/how-do-i-compile-my-code-so-that-it-becomes-an-executable-jar-and-can-be-opened.  So...
        ```scala
        scala> :paste -raw
        // Entering paste mode (ctrl-D to finish)

        object HelloWorld {
            def main(args: Array[String]) {
              println("Hello!")
            }
        }

        // Exiting paste mode, now interpreting.
        ```
    ...OK, so it didn't barf, but the code was not executed.  Not going to spend any more time on this for now.



## [Chapter 2. Working with Data: Literals, Values, Variables, and Types](http://techbus.safaribooksonline.com/book/programming/scala/9781449368814/idot-core-scala/ch02_html)

### Excercises


## [Chapter 4. Functions](http://techbus.safaribooksonline.com/book/programming/scala/9781449368814/idot-core-scala/ch04_html)

### Terms

* **functions** - named, reusable _expressions_.
* **pure functions:** 
    * Has one or more input parameters
    * Performs calculations using only the input parameters
    * Returns a value
    * Always returns the same value for the same input
    * Does not use or affect any data outside the function
    * Is not affected by any data outside the function
* **procedure** - _function_ that doesn’t have a return value
* **recursive function** - _function_ that may invoke itself, preferably with some type of parameter or external condition that will be checked to avoid an infinite loop of function invocation.
* **tail-recursion** - recursive invocation doesn’t create new stack space but instead uses the current function’s stack space.
    * Only functions whose last statement is the recursive invocation can be optimized for tail-recursion by the Scala compiler.
    * `@annotation.tailrec` - Scala compiler will attempt to optimized for tail-recursion, failing with compile error if it cannot.

### Excercises

1. Write a function that computes the area of a circle given its radius.

    **Answer:** Complete
    ```scala
scala> def area(radius:Double): Double = 3.14 * radius * radius
area: (radius: Double)Double

scala> area(4.556)
res40: Double = 65.17740704
    ```
2. Provide an alternate form of the function in exercise 1 that takes the radius as a String. What happens if your function is invoked with an empty String ?

    **Answer:** Complete
    ```scala
scala> def area(radius:String): Double = 3.14 * radius.toDouble * radius.toDouble
area: (radius: String)Double

scala> area("4.556")
res38: Double = 65.17740704

scala> area("")
java.lang.NumberFormatException: empty String
  at sun.misc.FloatingDecimal.readJavaFormatString(FloatingDecimal.java:992)
  at java.lang.Double.parseDouble(Double.java:510)
  at scala.collection.immutable.StringLike$class.toDouble(StringLike.scala:259)
  at scala.collection.immutable.StringOps.toDouble(StringOps.scala:30)
  at .area(<console>:7)
  ... 33 elided
    ```
    
1. Write a recursive function that prints the values from 5 to 50 by fives, without using for or while loops. Can you make it tail-recursive?
 
    **Answer:** Complete

    ```scala
scala> @annotation.tailrec
     | def increment(by:Int, max:Int, idx:Int = 0): Int = {
     |   val inc = idx + by
     |   println(inc)
     |   if (inc == max) inc
     |   else increment(by, max, inc)
     | }
increment: (by: Int, max: Int, idx: Int)Int

scala> increment(5, 50)
5
10
15
20
25
30
35
40
45
50
res3: Int = 50    
    ```

1. Write a function that takes a milliseconds value and returns a string describing the value in days, hours, minutes, and seconds. What’s the optimal type for the input value? 

    **Answer:** Complete (but pretty sure this could be done more cleanly)
    
    ```scala
scala> def millisToDateParts(millis:Long): String = {
     |   val perSecond = 1000
     |   val perMinute = perSecond * 60
     |   val perHour = perMinute * 60
     |   val perDay = perHour * 24
     |
     |   // Returns tuple of whole and remainder of division
     |   def timePart(millis:Long, divideBy:Int): (Long, Long) = {
     |     (millis / divideBy, millis % divideBy)
     |   }
     |
     |   val days = timePart(millis, perDay)
     |   val hours = timePart(days._2, perHour)
     |   val minutes = timePart(hours._2, perMinute)
     |   val seconds = timePart(minutes._2, perSecond)
     |
     |   s"${days._1} days, ${hours._1} hours, ${minutes._1} minutes, ${seconds._1} seconds"
     | }
millisToDateParts: (millis: Long)String

scala> millisToDateParts(10)
res0: String = 0 days, 0 hours, 0 minutes, 0 seconds

scala> millisToDateParts(10000)
res1: String = 0 days, 0 hours, 0 minutes, 10 seconds

scala> millisToDateParts(100000)
res2: String = 0 days, 0 hours, 1 minutes, 40 seconds

scala> millisToDateParts(1000000)
res3: String = 0 days, 0 hours, 16 minutes, 40 seconds

scala> millisToDateParts(10000000)
res4: String = 0 days, 2 hours, 46 minutes, 40 seconds

scala> millisToDateParts(100000000)
res5: String = 1 days, 3 hours, 46 minutes, 40 seconds

scala> millisToDateParts(1000000000)
res6: String = 11 days, 13 hours, 46 minutes, 40 seconds

scala> millisToDateParts(1234567890)
res7: String = 14 days, 6 hours, 56 minutes, 7 seconds
    ```

1. Write a function that calculates the first value raised to the exponent of the second value. Try writing this first using math.pow, then with your own calculation. Did you implement it with variables? Is there a solution available that only uses immutable data? Did you choose a numeric type that is large enough for your uses?
