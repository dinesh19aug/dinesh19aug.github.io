---
title: 'Scala: Tail Recursion'
author: Dinesh
type: post
date: 2017-03-20T02:37:02+00:00
url: /2017/03/20/scala-tail-recursion/
dsq_thread_id:
  - 5647609754
  - 5647609754
categories:
  - Tech Notes

---
Tail-344recursion is a basic but important concept in Functional programming. Recursive functions has always been a pain point for me. I would be eliminated out of several interview rounds if interviewers places emphasis on recursion. In Java world thankfully, most people I know hate recursion because when nesting goes too deep, it impacts the performance if the nested recursion is more than 100 levels deep.

Unfortunately(Fortunately), functional programming languages like Scala and Haskell have solved this concept with the term Tail Recursion. We will look into the concept of Tail recursion using a sample code below by implementing a function that calculates &#8220;factorial&#8221;.

Regular Recursion code: Calculate factorial

<pre>def factorial(n:Int) :Int={
   if(n&gt;0) n * factorial(n-1)
   else 1
}

</pre>

So the problem with above code is that if I pass a value **factorial(5) ,** then the code will create a series of wait to get the result back ex &#8211;

Call 1: 5 * factorial(4)

Call 2: 4*  factorial(3)

Call 3: 3* factorial(2)

Call 4: 2* factorial(1)

Call 5: 1*1

Now the call retraces the nested flow to jump back to Step 4 to provide the value as 2\*1, which traces back to Step 3 &#8211; 3\*(2*1) and so on.

Imagine what will happen if you pass a **factorial(100)??**

Now let&#8217;s take a look at how it is done properly in Functional progaramming using [scala][1].

<pre>def factorial(n:Int) :Int={
  def calculateFactorial(n: Int, acc:Int){
    if(n&lt;=0) acc
    else calculateFactorial(n-1, n* acc)
  }

  calculateFactorial(n,1)
}</pre>

Do you see the difference in code? No?. Let me explain what we just did. In Scala, you can define a local method inside another method. So I created a new method called &#8220;**calcuateFactorial&#8221;** that takes two parameter, **n:Int** and **acc:Int, **where acc is accumalor of the result. Now when I call the function **factorial(5), **the recursion code is not doing any processing or calculation on the method. It just returns the accumalator **acc** as a result. Ex &#8211;

call 1 &#8211; Intput 5,1

call 2 &#8211; Input 4, 5*1

call 3 &#8211; Input 3, 4\*(5\*1)

call 4 &#8211; Input 2, 3\*(4\*(5*1))

call 6 &#8211; Input 1, 2\*(3\*(4\*(5\*1)))

call 7 &#8211; Input 0, 1\*(2\*(3\*(4\*(5*1)))) &#8211;  **RETURN RESULT as 1\*2\*3\*4\*5 which is the second input param

**

That is when a recursion becomes tail recursion. The final call when nesting stops, just returns the result and the previous nested call is not waiting for a result to complete the call/result.

Hope the concept will stay with me and with those of you who hated recursion earlier. It just got real so learn and deal with it 🙂

~ Ciao

 [1]: https://www.scala-lang.org/
