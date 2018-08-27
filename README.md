
# Break and Continue Statements

## Introduction
In this lesson, we are going to talk about the `break` and `continue` statements in Python. Sometimes we will want to perform operations using a for loop on **almost** every element in a collection, or only certain elements, or only one element. Whatever the case may be, we can see that we'll need to be able to add some *flow control* to our iteration process with for loops. `break` and `continue` can help us do just that. We'll look at exactly how these statements work and when is a good opportunity to employ these.

## Objectives
* Understand what `break` and `continue` statements can do
* Identify opportunities to use `break` and `continue`

## What Are `break` and `continue` Statements?

In this case, it is almost best to not overthink it too much. `break` and `continue` essentially do what they sound like. They are used in tandem with conditional statements (`if`, `elif`) inside loops, and they *break* out of a loop if a condition is met or *continue* a loop if a different condition is met. Before we dive too deep into how these statements function, let's look at an example.


```python
numbers = list(range(0,30))
new_list = []
for num in numbers:
    if len(new_list) > 4:
        print(f"We have enough even numbers in new_list ({len(new_list)}). break will stop the for loop now")
        break
    elif num % 2 == 0:
        new_list.append(num)
    elif num % 2 != 0:
        continue
        print("i never get executed")
    print(num, "is even.")
    print("this does not print for odd numbers\nbecause the continue statement skips\nthe code that follows in the for loop\nand goes straight back to the next element in the for loop")
    
```

Okay, so, let's unpack what's happening here. 

First, we have a for loop that is iterating over our list, `numbers`, which has 30 numbers in it. Then we see that we have an if statement that only executes it's code when our `new_list` has more than 4 numbers in it. Once this condition is met, we **break** out of our loop. We then have an `elif` statement that adds any even number to the `new_list`, and a final `elif` statement that tests to see if the number is odd, and if it is odd, then it **continue**s to the next element in our for loop's iteration process. 

So, first let's dig into the `continue` statement. `continue` is telling our loop to **skip** any code that comes after it and go straight to the next element in our loop. So, if we are dealing with number `1` in our list of numbers, we will hit our `continue` statement and immediately go to the next element in our for loop (i.e. `2`). Any code that comes after the `continue` will **not** be executed, **but** our for loop does **not** end execution. This contrasts with the `break` statement. Our break statement is only executed when we have met our condition that the `new_list` has reached the number of elements we want it to have. Once the `break` statement is executed, it will end the execution of the for loop altogether. All code after the `break` statement will be ignored, similar to our `continue`, but there will be no next step to the iteration. It stops the loop and that's the end.

So, essentially, we can use `continue` to *skip* operation on elements and code below the continue. We can then use `break` when we have a condition that tells us we want to stop the process altogether.

We can look at two examples to really reinforce this difference in execution.


```python
for i in list(range(0,5)):
    if True:
        print(i)
    print("Since we don't have a continue statement,\nI'll always get executed")
```


```python
for i in list(range(0,5)):
    if True:
        print(i)
        continue
    print("I'll never get executed")
```


```python
for i in list(range(0,5)):
    if True:
        print(i)
        break
    print("I'll never get executed either")
```

These examples are a bit contrived but they very clearly show how `continue` and `break` work inside loops and conditional statements as well as the difference between their execution.

## Identify Opportunities to Use Break and Continue

Let's say you have a collection of things that you want to filter out elements and create a new list with the elements you want. But you also want to perform a complex operation on each of the elements you **do** want. Well, you don't want to perform that operation on the elements that you don't want and you don't want to have to perform multiple for loops on the collection. So, a `continue` statement would allow you to optimize your performance and avoid needing to perform those operations. And a `break` statement can be used when we want to put a limit on the number of iterations we perform, the number of elements we append to a new list, or even just stop our iteration when we have found the first element we want. Let's take a look:


```python
names = ["aNNE", "JaNe", "willIAM", "WanDA", "WeSt", "HELEN", "tHoMaS", "HENrY", "John", "Marshall", "May"]
formatted_names = []
check_count = 0

for name in names:
    if name.startswith('w') or name.startswith("W"):
        check_count += 1
        continue
    elif len(formatted_names) >= 4:
        check_count += 1
        break
    else:
        formatted_names.append(name.title())

print("before", names)
print("after", formatted_names)
print(check_count)
```

    before ['aNNE', 'JaNe', 'willIAM', 'WanDA', 'WeSt', 'HELEN', 'tHoMaS', 'HENrY', 'John', 'Marshall', 'May']
    after ['Anne', 'Jane', 'Helen', 'Thomas']
    4


Okay, so, as we can tell from our code. We wanted to create a list of 4 names that are properly formatted and that **don't** start with the letter `w`. To optimize our code, we first check to see if the name starts with `w`. If it does, we skip all other operations that we need to do and go to the next name. Next we check to see if we have hit our quota of 4 names. If we have, then stop the iteration altogether. Lastly, if neither condition is met, format the given name and append it to our new list of formatted names.
This way, we are optimizing our code by making sure that we eliminate performing any operations that aren't absolutely necessary at each step. You may have noticed the variable, `check_count`. If you are feeling unconvinced that the break and continue are not cutting down on the amount of times our code is executing, run the cell below and compare the `check_count`s, which increment after **each** check of a conditional statement.


```python
names = ["aNNE", "JaNe", "willIAM", "WanDA", "WeSt", "HELEN", "tHoMaS", "HENrY", "John", "Marshall", "May"]
formatted_names = []
check_count = 0

for name in names:
    formatted_name = ""
    if len(formatted_names) < 4:
        check_count += 1
        if not name.startswith('w') or not name.startswith("W"):
            check_count += 1
            formatted_names.append(name.title())
            

print("before", names)
print("after", formatted_names)        
print(check_count)
```

    before ['aNNE', 'JaNe', 'willIAM', 'WanDA', 'WeSt', 'HELEN', 'tHoMaS', 'HENrY', 'John', 'Marshall', 'May']
    after ['Anne', 'Jane', 'William', 'Wanda']
    8


See that?! We have cut down on the different checks we perform by one half (50%)! And on top of that, to get the same result we have to have a **nested** if statement, which is, technically put, ***gross***. All joking aside, nested if statements should be avoided if they can be since they make our code less readable and therefore harder to maintain ontop of being half as efficient as our previous code.

It's imperative to note that these excess checks could represent much more expensive operations in our code. So, it is important to try and use `break` and `continue` when it makes sense.

## Summary

In this lesson, we introduced some *control flow* statements, `break` and `continue`, which allow us to make our conditional statements and the rest of our code more efficient and more readable. We call these statements flow control statements because they allow us to *control* the *flow* of our code's execution. 
