---
layout: post
title: List Comprehension with Conditional Expressions
---

In my attempt o write "Pythonic" code, I googled "Pythonic code".  How can code be considered "Pythonic"?

Quoting from this wonderful [blog post](http://blog.startifact.com/posts/older/what-is-pythonic.html)

> To be Pythonic is to use the Python constructs and data structures with clean, readable idioms. It is Pythonic is to
  exploit dynamic typing for instance, and it's definitely not Pythonic to introduce static-type style verbosity into the
  picture where not needed. To be Pythonic is to avoid surprising experienced Python programmers with unfamiliar ways to  
  accomplish a task.

My goal was to create a function to generate a random word generator given a list of letter positions that must remain unchanged.

For my input:

```
in = "creed is a great movie"
index = [1,3,5]
```

This function must generate random letters corresponding to the letters in the input string except if the letter is in the index position in the constant_index list.  For this example, we will not change 'r' in index 1, 'e' in index 3 and ' ' in index 5.

 ```
    import random
  
    def selective_generate_1(in, index):
        alphabet = 'abcdefghijklmnopqrstuvwxyz '
        i = 0
        result = ''
        strlen = len(in)
        while i < strlen:
            ch = ''
            if i not in index:
                ch = alphabet[random.randrange(strlen)]
            else:
                ch = in[i]
            result += ch
            i = i+1
        return result

    def selective_generate_2(in, index):
        strlen = len(in)
        alphabet= 'abcdefghijklmnopqrstuvwxyz '
        return "".join(in[i] if i in index else alphabet[random.randrange(strlen)] for i in range(strlen))
 ```
  
In this informative [blog post] (http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html), it encourages the use of list comprehensions while keeping it simple.  This means limiting conditions inside list comprehensions to two or three.

Looking at `selective_generate_2`, we have reduced static  style verbosity, used ternary operators with a list comprehension, used range,  and used join for string concatenation.  The downside is that we might be sacrificing a little readability with everything in one line. We should be mindful in the order we right one-liners like this.  

*We start with the individual element we want to process:* `for i in range(strlen)`

*Then we evaluate the ternary conditional operator:* `if i in constant_index else alphabet[random.randrange(strlen)]` 

*Then we get the result and the result for each individual element are placed in a list:* `input_str[i] or alphabet[random.randrange(strlen)]`

*Then we join the elements in a list as a string:* `"".join(...)`
            



 
