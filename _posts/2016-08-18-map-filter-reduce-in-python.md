---
layout:     post
title:      map, filter, reduce in Python
date:       2016-08-18
summary:    Understanding map, fiter, reduce in Python
categories: Python, Functional Programming
---

I am playing around with some basics of functional programming and to start with I was trying to understand the behavior of these simple functions in Python and with this post I would like to share my understanding about these functions.

## map()
If we look at the map() signature, it takes two arguments:

```python
r =  map(function, sequence)
```

So an example to understand what a map would be:

```python
def square(x):
	return x*x
	
r =  map(square, [1,2,3,4])
```

Output of this simple function would [1,4,9,16]

Looking at the output, we can now comprehend what does a map() function do? It takes the <i>function</i> which is provided as an argument and apply it to all the elements of the <i>sequence</i>. Till this point everything seems so easy and simple so to make things interesting what we could do is, pass multiple sequences as an argument to this function. Let's see how does it behave in that scenario:

```python
def sum(x,y):
	return x+y
	
r =  map(sum, [1,2,3,4], [5,6,7,8])
```

Output would be : [6,8,10,12]

This looks interesting, so what map() did was it took elements of both the list one by one and applied sum over them. This concept could be generalized over <i>n sequences</i>.

## filter()
filter() is another function which is very simple but a very useful one. Function signature of filter() is very similar to map(), it also take two arguments: function and sequence

```python
r =  filter(function, sequence)
```

We will again take a simple example to comprehend the functioning of filter(). Suppose we want to filter even number from a list we can use filter() to do so.

```python
def even(x):
	return x%2 == 0
r =  filter(even, [1,2,3,4])
```

Output of this would be list of even number: [2,4].

filter() works in the similar manner like map(), it applies function to all the elements of the list. The interesting part to note is, the function which is supplied as a argument, will return a boolean value True or False and that's the deciding factor which govern whether the element should be included or not in the new list.

## reduce()
This is another function in the same leauge whose function signature match with map() and filter():

```python
r =  reduce(function, sequence)
```

But it is the most interesting function to understand so let us take an example to understand this function. Consider a scenario you want to find sum of all the elements of list how would you proceed in normal scenario, you would iterate over the list and add up all the elements and if a say, you could do it with one line in python. Lets see how we can do this (Assuming everyone is familiar with lambda functions in python):

```python
r = reduce(lambda x,y: x+y, [1,2,3,4])
```

Output would be: 10

Now if we want to formally define the functioning of reduce(function, sequence). It continually applies function() to the elements of sequence.

If sequence = [s1, s2, s3 ..... , sn], calling reduce reduce(function, sequence) works like this:

- At first the first two elements of seq will be applied to function, i.e. function(s1,s2) The list on which reduce() works looks now like this: [ func(s1, s2), s3, ... , sn ] 
- In the next step func will be applied on the previous result and the third element of the list, i.e. function(function(s1, s2),s3). The list looks like this now: [ function(function(s1, s2),s3), ... , sn ] 
- Continue like this until just one element is left and return this element as the result of reduce()


I would like to conclude the post with this. Hope you like this post.

&lt;/Happy Coding/&gt;