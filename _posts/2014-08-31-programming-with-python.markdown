# Programming with Python

## Python?

So here we are. In the past, my education has given me a wide variety of challenges to overcome, but mostly with the big players. C++ and Java have been commonplace in many educational programs the past decade or so. However, lately there's been a bit of a trend toward scripting languages for beginners and intermediate students alike. Now, it's now become a standard in many Minnesota colleges, for some reason.

So there it is, my education requires that I learn Python. I'm not mad, this is probably a good deal for me. So far it's been pretty fun!

### My Impressions thus far

*Normally* I don't code in any sort of scripting language,(though I've been actively pursuing ruby, and to a lesser extent Javascript) and so I periodically get lost on the little things someone a bit more experienced than I would probably not have too much trouble with.

I've been spending a lot of time in Objective-C lately, and I *want* to be typing all these extra characters. My mind wants to put `int`, `bool`, and `float`, before the variable name. You simply don't really need to do this all that often in Python, I've been lead to understand from the first couple attempts I've made. This is true for many of the scripting languages, but you don't need to explicitly define your variables like you do in C/C++, Java, etc. It's enough to say `x = 4`, or `myString = "This is my String, yo."`

Syntactically, it makes sense to read. Maybe not at first, as I've had my nose deep down in the Obj-C/C++ trenches for awhile and it's weird to change like this, but after a few minutes it's simple.

#### Slow and Steady wins the race - A (really) Basic Example

Let's show an example, and lets start basic.

Say we want to write a program that asks a user to enter two integers and print them to the screen, to begin with.

So, in Java, that would mean something like this:

```java
import java.util.Scanner

public class twoIntegers {

  public static void main(String[] args){
    Scanner s = new Scanner(System.in);
    System.out.println("Please enter your favorite Integer:")
    int x = s.nextInt();
    System.out.println("Now, why not enter your least favorite Integer:")
    int y = s.nextInt();  
    System.out.println("You entered " + x + " " + y + ",");
  }
}
```
**Great!**
We had to import a Scanner, set it up in the main, and use it to set our ints. Not too bad!

So now let's look at what I've cooked up for a Python(3.x) implementation:

```python
x = int(input("Enter most favorite integer:"))
y = int(input("Enter least favorite integer:"))
print("You entered " + str(x) + " " + str(y) + ".")
```
**Did I miss something...?**
Nope! But I lied. We *did* have to cast the user input as an int to get this to work properly (and then recast as a string to print all at once), but there it is - in all it's glory.

So, 12 lines of code for Java (which you could cut down by 2 or 3 lines, I suppose...) and *3* for Python. Yay, scripting!

I'll be working with these code snippets more later on, but they'll do for now.

### So There We Have It
I'm just getting started with Python - but like other scripting languages, it's kind of convenient how much you can get done in so few lines. I'm excited to dive in and see what else we can accomplish with Python.
