---
layout: post
title:      "Ruby and Iteration "
date:       2019-06-10 14:06:57 +0000
permalink:  ruby_and_iteration
---


I started learning Ruby about probably 9 months ago, after making the decison to look into a career in programming again.  I had studied some computer science in college even though that was not my final major. and even did a little bit of work programming during summers in college.   I eventually ended up working in IT support for 4 years, played with web pages in grad school but never really programmed or developed, though I had many friends who were software developers.  I had never done object-oriented coding, for example.

So when I encountered Ruby, I found it to be kind of interesting compared to other languages (C, Pascal) that I had used.  The biggest thing when learning Ruby is that the language seems very well designed for iterating through arrays of variables or hashes of variables, or arrays of hashes of variables.   One can go through an array, say a[0]...a[10] by just using an .each statement  

a.each {|a_el| puts "#{a_el}"}  

instead of having to do something like 

for (i=0; i < 10, i++)
     printf("%s\n", a[i])

That is how one would do that in C, for example.  Note that in Ruby, one does not have specify the length or size of the array, though one can obtain the size/length of the array by calling a method a.length.  So one doesn't have to know in advance how long an array is.  Note, also that one can iterate without ever to use an index variable--though there are ways to get one if needed.

Ruby also has functionality that allows arrays to be created from other arrays (.map, .select), searched (.find).  One can find the first element of an array (.first) (ok, that's not that hard in other languages), the last element (.last, one doesn't  need to know the length of an array to find its last element).    All of this lowers the number of characters of code that needs to be written in Ruby for iterating through arrays.  There are also many methods/functions in Ruby for performing tasks (e.g. sorting, removing duplicate elements) on those arrays.  Because strings also have some of the same properties as arrays--in some languages, strings ARE arrays of single characters-- there are also a number of functions for manipulating and getting information from strings.

The idea of a "hash" takes on a new meaning in Ruby.  The idea that a non-numeric character or a symbol can map to another data element  and using keys, of course, is not new, and cryptography is based on using such hashes.  In Ruby, though, one can create hashes that sort of act like arrays in other languages, but allow symbols to be "index" -- these are keys--to a value.   In a way, these hashes (set of key-value pairs) are sort of variable pairs within a larger data structure.   This allows more flexibility because one can just pass a hash in as argument to a method...and the argument variable can have different number of key-value pairs.  

In older languages there were ways around too, but generally if one specified 3 arguments for a function or a procedure, one had to pass in 3 arguments, including perhaps a "none" for a variable.   

Ruby also is a tad different than non-object oriented languages like C or Pascal in that the main variables appear to be objects and the code that operate on them are methods.   The methods also access data from the object that is calling them...so methods can get data from other their calling object and any parameters/arguments passed in.   When looking at and writing Ruby code -- especially in methods -- one has to remember that, as opposed to always looking for a local or a global variable (which Ruby does have)

In summary, I can defiintely understand why Ruby can be used for applications where there is a lot of iteration, because it allows for abstraction that is easier to understand.  Ruby allows for cleaner code in performing these iterative tasks, rather than having to declare fixed size arrays or specify fixed-length loops and index variables.  I only have started learning Ruby and hope to learn more how to use the language in building and developing apps.



