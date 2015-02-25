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

3. Take the result from exercise 2, halve it, and convert it back to Centigrade. You can use the generated constant variable (e.g., “res0”) instead of copying and pasting the value yourself.

4. The REPL can load and interpret Scala code from an external file with the :load <file> command. Create a new file named Hello.scala and add a command that will print a greeting, then execute it from the REPL.

5. Another way to load external Scala code is to paste it into the REPL in “raw” mode, where the code is compiled as if it were actually in a proper source file. To do this, type :paste -raw, hit Return, and then paste the contents of your source file from exercise 4. After exiting “paste” mode you should see the greeting.


## [Chapter 2. Working with Data: Literals, Values, Variables, and Types](http://techbus.safaribooksonline.com/book/programming/scala/9781449368814/idot-core-scala/ch02_html)

### Notes

### Excercises


