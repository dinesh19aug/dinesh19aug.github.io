---
title: 10 IntelliJ IDEA Keyboard Shortcuts That You Must Know
author: Dinesh
type: post
date: 2014-01-31T21:09:07+00:00
url: /2014/01/31/10-intellij-idea-keyboard-shortcuts-must-know/
bavotasan_home_page_alignment:
  - pull-left
  - pull-left
dsq_thread_id:
  - 5451639712
  - 5451639712
categories:
  - Tech Notes

---
Linux nerds/geeks happily flaunt their keyboard skills when they get a chance. I admit that I am not a shortcut junky but I too have some keyboard shortcuts under my sleeve that I use in day to day work. I have to say that not only have these shortcuts increased my productivity but they have also made my life a lot easier.

I am sharing my 10 most used shortcuts at work.

**1. Comment or Un-Comment: CTRL + L**

You will often run into situation where you need to add debug statement temporarily and remove or comment the line after the debug is complete. Instead of manually going to the beginning of the line and manually typing //, you can use the keyboard shortcut **CTRL + L**. A cool thing to know is that you can comment out multiple lines at once. <img class="alignnone" src="http://www.javahabit.com/wp-content/uploads/2014/01/156.png" alt="" width="553" height="89" />

&nbsp;

&nbsp;

**2. Documentation Comment Block : /** + Enter**

I may not follow other coding standard but I do follow this &#8211; &#8220;Leave the place cleaner before you leave&#8221;. One of my biggest pet peeves is developers not documenting about a method or sub routine. What are you conveying or trying to do in a particular method? I hate when I come across such code or even my code when I was beginner. So if commenting single line was not cool enough for you then you can use this to create documentation comments or comment out the code without ugly // marks showing at each line. ![][1]

To compare the difference, I have commented the same code using **CTRL+L **and **/** + Enter** ![][2]

**VS**

![][3]

&nbsp;

&nbsp;

**3. Delete Line : CTRL + Y**

This one is easy. If you have any vim experience or have used sublime text in the past then this would come easy. Simply place the cursor on the beginning of the line and hit **CTRL + Y.** Now it might not seem intuitive because the obvious choice of deleting should have been **CTRL** **+ D **(_It actually adds a new line if you wondered what it does_) but a cool way to remember is to think about confirmation dialog boxes in Unix. For example &#8211; Are you sure you want to delete this folder? (Y/N)

&nbsp;

&nbsp;

**4. Argument Documentation For Method Calls: CTRL + P**

This one is a true life saver. Imagine you are about to call method which accepts 10 parameters. You start by typing &#8211; MyClass.someMethodWith10Params(.., ..,) and you forget what was the third parameter that I need to pass. One ugly way of doing is use your mouse and place the cursor at the beginning of the open bracket and wait for a second until the highlight shows you that the third parameter that you need to pass is a String variable. However if you are like me who forgets the fourth and then next parameters, you would be pulling your hair out. Here comes your knight in the shining armor &#8211; **CTRL+P. **This will tell pull up a callout with the information you need.

![][4]

&nbsp;

&nbsp;

**5. Continuous Code Selection: CTRL + W**

Raise your hand if you never had to copy paste the code. Any one? This shortcut lets you select a word, block or comment without touching your mouse. When you press **CTRL+W **it will select the code next to the cursor and will continue to select intelligently. When I say intelligently I really mean it. Say you place your cursor in the middle of the code block and hit the key combination it will copy code from opening braces to closing braces and so on. Here&#8217;s a sample.

![][5]

&nbsp;

&nbsp;

**6. Paste from history: CTRL + V + Shift**

A lot of time I copy and paste code. Sometimes I open multiple projects and files and copy paste code from one project file to another project file. Occasionally I have to use a copy of code which I copied two steps behind and in that case I would think hard what file did I copy it from. Well I found this cool shortcut that saves me all the trouble to recall the file name and line numbers. Usually one uses CTRL + V to paste, but if you use CTRL + V + Shift then IDEA will show the last five copies that you can choose from to paste.

<img class="alignnone size-full wp-image-692" src="http://www.javahabit.com/wp-content/uploads/2014/02/img_52f1a6ac20ecb.png" alt="" />

&nbsp;

&nbsp;

**7. Last Changed files: CTRL + SHIFT + E**

I used [SVN][6] at work and [git][7] or [Bazaar][8] for my personal project. At times when I am not using either it can be hard to track and remember what files did I change in last 1-2 hours. Usually if you are using [SVN][6] then you can see uncommitted files to figure out the file changes. However how do you track the files that changed in the last one hour if you are not using SVN or git or mercurial tools. It turns out that [IntelliJ][9] keeps a track of your recent file changes. You can just use the shortcut CTRL + SHIFT + E to see the last edited files.

<img class="alignnone size-full wp-image-693" src="http://www.javahabit.com/wp-content/uploads/2014/02/img_52f1a968ebd4f.png" alt="" />

&nbsp;

&nbsp;

**8. File Structure popup: CTRL + F12**

This shortcut comes in handy if you are traversing through a huge file looking for a particular method name. You can either do CTRL + F to search for the method name. But at times you may not remember the name of the method or are not sure what methods or members are present in that file. In that case you use this shortcut.

<img class="alignnone size-full wp-image-694" src="http://www.javahabit.com/wp-content/uploads/2014/02/img_52f1aafa1a786.png" alt="" />

&nbsp;

&nbsp;

**9. Evaluate Expression : ALT + F8**

This is one feature that comes in handy in the debug mode. This features allows you to quickly test the output of an expression. For ex &#8211; Say I have a method that accepts a number from user and adds 2. When you are in debug mode and need to test a program that is already running need to figure out what would happen if I add 290.756 instead of adding 2, then you would normally have to make code a change or rerun the program. Some IDEs let you do hot deploy while some do not also in a large project this restart and change may take up long time to test one expression. This is when you can use this shortcut to quickly test different expressions without restarting or making a code change. <img class="alignnone size-full wp-image-695" src="http://www.javahabit.com/wp-content/uploads/2014/02/img_52f1bad77d359.png" alt="" />

&nbsp;

&nbsp;

**10. System.out.println() : sout + tab**

I kept the easiest and most used shortcut as the last piece. This is not really a shortcut but when I was looking for a way to avoid typing this verbose piece of code, I was surprised to see that many people did not know this fact. Unlike <a title="Netbeans" href="https://netbeans.org/" target="_blank">Netbeans</a> or <a title="Eclipse" href="https://www.eclipse.org/" target="_blank">Eclipse</a> where you can specify shortcut for commonly used text, I could not find this option in IntelliJ until I found the solution in <a title="Stackoverflow" href="http://stackoverflow.com/" target="_blank">SO</a>. Just type **sout **and hit TAB to print out the complete text. ~Ciao &#8230; Enjoy the shortcuts and more.

> P.S. &#8211; If you liked the post please click on one of the ads in the right hand column to help me maintain this site and do drop a me a line to suggest some topics that would like to see on this site.

 [1]: http://www.javahabit.com/wp-content/uploads/2014/01/646.png
 [2]: http://www.javahabit.com/wp-content/uploads/2014/01/996.png
 [3]: http://www.javahabit.com/wp-content/uploads/2014/01/674.png
 [4]: http://www.javahabit.com/wp-content/uploads/2014/01/478.png
 [5]: http://www.javahabit.com/wp-content/uploads/2014/01/636.png
 [6]: http://tortoisesvn.net/ "SVN"
 [7]: https://github.com/ "Github"
 [8]: http://bazaar.canonical.com/en/ "BAZAAR"
 [9]: http://www.jetbrains.com/idea/ "IntelliJ"