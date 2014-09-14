---
layout: post
active: blog
title: Finance With Python
date: 2014-09-04
---


# Finance With Python, The Hard Way

## What's PMT?

Basically, PMT (as far as finances goes) usually stands for a function that calculates the payment for a loan based on constant payments and interest rate.

You can use a pmt() function in just about any language with the right libraries imported, and if you know your way around Microsoft's Excel program, it's built into there as well.

But for the sake of learning how things work, we aren't going to do it the easy way.

### The Hard Way

So. Like I was saying, normally if you want to do this easily in Python, you go ahead and download <a href="http://www.numpy.org/">NumPy</a> and import it into your Python file.

Then all you have left to do is `pmt(rate,nper,pv[,fv,when])`,
where rate is your calculated monthly interest rate, nper is total payment periods, pv is present value (how much you start with on the loan), fv is the future value (usually 0 for most people), and when triggers when payments are due for the function, either 1 for begin or 2 for end.

Sounds easy enough, once you get past the syntax. Well let's try this on our own.

#### Calculating...

So I've whipped up an easy to understand solution for Python.
You can read along here, and if you want you can pop the code into your IDLE or terminal from <a href"https://github.com/lydelln/python-projects">here.</a> Look for the PMT folder.

The first thing I'll be doing is defining a function with which to use to calculate the PMT.

There are a few things I did that probably don't *need* to be done, per se. But this worked for me, and I think it's easy enough to understand.

Here's the function I've put down, I'll break it up into chunks in just a second:

{% highlight python linenos %}
def loanAmort(initial, apr, time):

  totalInt = 0
  totalPaid = 0
  prinPayment = (initial / time)
  remaining = initial

  for x in range(1, (time + 1)):

    monthlyPayment = (initial * pir) / (1 - (1 + pir)**(-time))
    intThisMonth = (monthlyPayment - prinPayment)
    remaining += intThisMonth
    remaining -= monthlyPayment

    if(x < 10):
      print(str(x) + "      " + "%.2f" % intThisMonth + "            " + "%.2f" % prinPayment + "            " + "%.2f" % (remaining))
    else:
      print(str(x) + "     " + "%.2f" % intThisMonth + "            " + "%.2f" % prinPayment + "            " + "%.2f" % (remaining))


    totalPaid += monthlyPayment
    totalInt += (monthlyPayment - prinPayment)


  print(" ")
  print("Total Paid     |   Total Interest Paid")
  print("--------------------------------------")
  print("%.2f" % totalPaid + "             " + "%.2f" % totalInt)



  return
{% endhighlight %}

Okay! Not so bad. Take a look at:

{% highlight python linenos %}
def loanAmort(initial, apr, time):

  pir = (apr / time)
  totalInt = 0
  totalPaid = 0
  prinPayment = (initial / time)
  remaining = initial

  for x in range(1, (time + 1)):

    monthlyPayment = d
    intThisMonth = (monthlyPayment - prinPayment)
    remaining += intThisMonth
    remaining -= monthlyPayment
{% endhighlight %}

We've defined our function with the `def` tag, and asked for 3 variables.

The variables I asked for were the initial value of the loan (or PV), APR, which is the interest annually, and time, how many periods do we have to pay within.

`pir` is the APR divided by periods to pay. This is what we call "Periodic Interest Rate." It is necessary for the function.

Since we also have to calculate total interest paid and total amount paid for this exercise, I've taken the liberty of adding `totalInt` and `totalPaid` as variables outside our for loop.

The payment on our principle each month is what I have defined as `prinPayment`, which is the amount due per month before we add interest.

`remaining` is set to initial, because we need to know how much loan is remaining if we're going to print it out on the screen for the user!

Now the loop:
We are going to use the for loop with a range. This stops it from iterating at a certain point. We define x as 1, and it's max as time + 1 for accuracy on the printed sheet for the user. _(Note: there are a few ways to do this, and you might not agree with adding +1 onto the range in the loop definition, but that's how I've done it here.)_

The monthly payment is actually calculated with the formula:

**P = (Pv*R) / [1 - (1 + R)^(-n)]**

You can see the similarity to my own function:

`(initial * pir) / (1 - (1 + pir)**(-time))`

I'm not a financial expert, but basically we've got a formula to get monthly payment there.

Lastly, `intThisMonth` is just my way of calculating how much interest will be paid for the sake of printing to the user. The total monthly payment (the amount with the interest added on) minus the principal payment (which, is the amount without any interest) should give us the interest.

`remaining` is added to the interest this month, and then reduced by the monthly payment. I did this to keep the numbers straight while I was printing to the screen, I believe it has to work this way to keep remaining balance on par with the interest added, as the remaining variable is otherwise untouched.

So without further ado...

Onward, intrepid Pythoneers!

{% highlight python linenos %}
if(x < 10):
  print(str(x) + "      " + "%.2f" % intThisMonth + "            " + "%.2f" % prinPayment + "            " + "%.2f" % (remaining))
else:
  print(str(x) + "     " + "%.2f" % intThisMonth + "            " + "%.2f" % prinPayment + "            " + "%.2f" % (remaining))


  totalPaid += monthlyPayment
  totalInt += (monthlyPayment - prinPayment)


print(" ")
print("Total Paid     |   Total Interest Paid")
print("--------------------------------------")
print("%.2f" % totalPaid + "             " + "%.2f" % totalInt)
{% endhighlight %}

All of this is just printing to the screen in a pretty shady, but effective format. We iterate through our loop, printing out which month it is (or payment period) with str(x), just using the loop counter as the variable here.

The if(x < 10) is just to keep the lines straight when the month goes up to the tens spot.

Next, after some space, we print the interest due this period, up to 2 decimals, the principal payment due, and total remaining balance.

To keep track of total amounts paid, and interest, we simply add the monthly payment to `totalPaid` and use some basic math to find interest added that month, adding it to `totalInt`.

Easy!

Then, with a small table-type formatting, we print out the total paid and total interest after our loop has iterated completely.


**Lastly**, we need to actually get these variables from our user, and call our function.

{% highlight python linenos %}
initialPrinciple = float(input("Please enter your initial Principle: "))
apr = float(input("Enter your APR (in percentage. eg. 12.5) Do not use '%' symbol: "))
apr = (apr / 100)
time = int(input("Enter the length of your term (in months) : "))

print("Month | Interest Owed | Principle Owed |  Principle Remaining ")
print("-------------------------------------------------------------------------------")

loanAmort(initialPrinciple, apr, time)
{% endhighlight %}

Of course, for tutorial I haven't checked exceptions (What if they type some "asldhakshd" nonsense for principle, for example.) but this gets the job done!
Note: We get the APR as a float, and divide it into percentage for the formula.

Done!

### Financial Expertise with Python
Of course there are easier ways to do this, but it helps to walk through the formula if you really want to understand what's going on under the hood. The function we made was actually pretty short for what it was, again. Bored on the weekend? Curious about how to calculate your loans? You could whip it up in an hour or so during a breezy late summer afternoon. (I know I did!)
