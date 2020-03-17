---
title: "Speeding up your loops with HashTables/Dict"
categories:
  - Programming
header:
  teaser: "assets/images/loop_vs_hash.png"
tags:
  - python
  - hashtable
---

Today I want to show you a way to speed up your code. If you are like me and are a self taught programmer/coder/data scientist... you are probably pretty comfortable with loops. We all know that loops are "horribly slow" and that you "should never use" them... blah blah blah.... However, for many of us, they are our default approach for a quick and dirt "first draft." What I want to talk about in this post are hashtables.

## Hash tables

So what are hash tables? They are an unorderd collection of key-value pairs. Each key is unique. In python, think of a dictionary, or you could think of a one-dimensional array where your key is the index, but you are not constrained to an integer based index.

If have done any programming in python, you probably know about the dictionary. But have you considered using it like an array? Lets look at an example. I'll code it up the "quick and dirty loop-de-loop" way and then compare it to using a hash table.

## Example

Here's the example. Write up a function that takes as input two arguments. Arg1 is a list (or 1D array) of integers. Arg2 is a single integer. If any two separate values in your list add up to equal the Arg2 integer, return True. Otherwise return False.

first we'll look at the quick and dirty approach.

```python
def compare_int_long(intList, testInt):
    """
    compare a list of integers to a single integer.

    return true if any 2 integers (i1 + i2) == testInt
    false otherwise
    """
    for idx1 in range(len(intList)):        # loop through the list
        int1 = intList[idx1]                # grab current integer
        for idx2 in range(len(intList)):    # loop through the list again
            if idx2 != idx1:
                int2 = intList[idx2]        # compare to every other integer
                if int1 + int2 == testInt:
                    return True             # passed test, so return true
    return False                            # failed so return false
```

This approach works, but is very brute force. For every element in your list, you compare it to every other element in your list to see if it passes the test. The problem with this approach? It scales pretty bad. This, I believe, is an *O(N<sup>2</sup>)* complex code. This means the performance of this function increases proportionally to the square of the size of the input list.

Now lets look at an example where we use the hash table (or a dictionary in python). first off though, there are a few things to note. If you create a standard dictionary in python and you call it with an undefined key... you'll raise an error. For example

```python
temp_dict = {'a': 1, 'b':2}
temp_dict['c']  # raises an error
```

Defaultdict, however has an interesting property. If you pass it a key with no value, it will assign a default value to that key. So with the above example we can modify it:

```python
temp_dict = defaultdict({'a': 1, 'b':2}, bool)
temp_dict['c']  # returns False
```

defaultdict makes the above problem much easier to tackle. You could set up a try block to catch any raised errors... or use default dict as shown here.

The other thing to note, is that we need to rethink how we structure the problem. Instead of comparing each integer to every other integer (which is an *O(N<sup>2</sup>)* performance problem), we consider a different approach. Our first test was `int1 + int2 == testInt`. However, we can rearrange the problem to `int2 == testInt - int1`. This is important because this allows us to do two separate loops through the list instead of a nested loop. Let's look at the example.

```python
def compare_int_hash(intList, testInt):
    """
    compare a list of integers to a single integer.

    return true if any 2 integers (i1 + i2) == testInt
    false otherwise
    """
    intHash = defaultdict(bool)             # default value will be False
    intCount = defaultdict(int)             # default value will be 0 which is usefull for counting
    listLength = len(intList)

    for idx in range(listLength):           # 1st loop creating a hash table with the key being testInt - int1 and the value being True
        val = testInt - intList[idx]
        intHash[val] = True
        intCount[val] += 1                  # count how many times
    for idx in range(listLength):           # 2nd loop seeing if int2 is found in the hashtable
        if intHash[intList[idx]]:
            if intCount[intList[idx]] > 1:  # do a quick check against the count so we know if we there are 2 values or if we just happen to have a single value that's half the testInt
                return True
    return False
```

The above example is probably more like a *O(2N)* scale problem. So, now lets take a quick look at the performance of these two functions.

![Loopy-De-Loop vs Hashing]({{ site.url }}{{ site.baseurl }}/assets/images/loop_vs_hash.png)

As you can see, the loopy-de-loop version very very quickly scales out of control. With just a list of 10,000 elements, worst case scenario, it'll take you roughly 53 seconds to test. However by using the hash table with the value you are wanting as the index key, you can test that same 10,000 element list in under a second (~0.01 s). Now just because it's dramatically different doesn't mean it's not scaling. There is an issue of scale here.

![Hash scale]({{ site.url }}{{ site.baseurl }}/assets/images/hash_scale.png)

You can see that the hash table approach is still scaling. It's just more more of a linear increase instead of the exponential scaling of the nested loop.

If you want to play around with the above code, here is a link to an example notebook on mybinder
[![badge](https://img.shields.io/badge/Launch-ex_hashtables-579ACA.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFkAAABZCAMAAABi1XidAAAB8lBMVEX///9XmsrmZYH1olJXmsr1olJXmsrmZYH1olJXmsr1olJXmsrmZYH1olL1olJXmsr1olJXmsrmZYH1olL1olJXmsrmZYH1olJXmsr1olL1olJXmsrmZYH1olL1olJXmsrmZYH1olL1olL0nFf1olJXmsrmZYH1olJXmsq8dZb1olJXmsrmZYH1olJXmspXmspXmsr1olL1olJXmsrmZYH1olJXmsr1olL1olJXmsrmZYH1olL1olLeaIVXmsrmZYH1olL1olL1olJXmsrmZYH1olLna31Xmsr1olJXmsr1olJXmsrmZYH1olLqoVr1olJXmsr1olJXmsrmZYH1olL1olKkfaPobXvviGabgadXmsqThKuofKHmZ4Dobnr1olJXmsr1olJXmspXmsr1olJXmsrfZ4TuhWn1olL1olJXmsqBi7X1olJXmspZmslbmMhbmsdemsVfl8ZgmsNim8Jpk8F0m7R4m7F5nLB6jbh7jbiDirOEibOGnKaMhq+PnaCVg6qWg6qegKaff6WhnpKofKGtnomxeZy3noG6dZi+n3vCcpPDcpPGn3bLb4/Mb47UbIrVa4rYoGjdaIbeaIXhoWHmZYHobXvpcHjqdHXreHLroVrsfG/uhGnuh2bwj2Hxk17yl1vzmljzm1j0nlX1olL3AJXWAAAAbXRSTlMAEBAQHx8gICAuLjAwMDw9PUBAQEpQUFBXV1hgYGBkcHBwcXl8gICAgoiIkJCQlJicnJ2goKCmqK+wsLC4usDAwMjP0NDQ1NbW3Nzg4ODi5+3v8PDw8/T09PX29vb39/f5+fr7+/z8/Pz9/v7+zczCxgAABC5JREFUeAHN1ul3k0UUBvCb1CTVpmpaitAGSLSpSuKCLWpbTKNJFGlcSMAFF63iUmRccNG6gLbuxkXU66JAUef/9LSpmXnyLr3T5AO/rzl5zj137p136BISy44fKJXuGN/d19PUfYeO67Znqtf2KH33Id1psXoFdW30sPZ1sMvs2D060AHqws4FHeJojLZqnw53cmfvg+XR8mC0OEjuxrXEkX5ydeVJLVIlV0e10PXk5k7dYeHu7Cj1j+49uKg7uLU61tGLw1lq27ugQYlclHC4bgv7VQ+TAyj5Zc/UjsPvs1sd5cWryWObtvWT2EPa4rtnWW3JkpjggEpbOsPr7F7EyNewtpBIslA7p43HCsnwooXTEc3UmPmCNn5lrqTJxy6nRmcavGZVt/3Da2pD5NHvsOHJCrdc1G2r3DITpU7yic7w/7Rxnjc0kt5GC4djiv2Sz3Fb2iEZg41/ddsFDoyuYrIkmFehz0HR2thPgQqMyQYb2OtB0WxsZ3BeG3+wpRb1vzl2UYBog8FfGhttFKjtAclnZYrRo9ryG9uG/FZQU4AEg8ZE9LjGMzTmqKXPLnlWVnIlQQTvxJf8ip7VgjZjyVPrjw1te5otM7RmP7xm+sK2Gv9I8Gi++BRbEkR9EBw8zRUcKxwp73xkaLiqQb+kGduJTNHG72zcW9LoJgqQxpP3/Tj//c3yB0tqzaml05/+orHLksVO+95kX7/7qgJvnjlrfr2Ggsyx0eoy9uPzN5SPd86aXggOsEKW2Prz7du3VID3/tzs/sSRs2w7ovVHKtjrX2pd7ZMlTxAYfBAL9jiDwfLkq55Tm7ifhMlTGPyCAs7RFRhn47JnlcB9RM5T97ASuZXIcVNuUDIndpDbdsfrqsOppeXl5Y+XVKdjFCTh+zGaVuj0d9zy05PPK3QzBamxdwtTCrzyg/2Rvf2EstUjordGwa/kx9mSJLr8mLLtCW8HHGJc2R5hS219IiF6PnTusOqcMl57gm0Z8kanKMAQg0qSyuZfn7zItsbGyO9QlnxY0eCuD1XL2ys/MsrQhltE7Ug0uFOzufJFE2PxBo/YAx8XPPdDwWN0MrDRYIZF0mSMKCNHgaIVFoBbNoLJ7tEQDKxGF0kcLQimojCZopv0OkNOyWCCg9XMVAi7ARJzQdM2QUh0gmBozjc3Skg6dSBRqDGYSUOu66Zg+I2fNZs/M3/f/Grl/XnyF1Gw3VKCez0PN5IUfFLqvgUN4C0qNqYs5YhPL+aVZYDE4IpUk57oSFnJm4FyCqqOE0jhY2SMyLFoo56zyo6becOS5UVDdj7Vih0zp+tcMhwRpBeLyqtIjlJKAIZSbI8SGSF3k0pA3mR5tHuwPFoa7N7reoq2bqCsAk1HqCu5uvI1n6JuRXI+S1Mco54YmYTwcn6Aeic+kssXi8XpXC4V3t7/ADuTNKaQJdScAAAAAElFTkSuQmCC)](https://mybinder.org/v2/gh/tyleracorn/lessons/master?filepath=Ex_hashtables.ipynb)

Hope you enjoyed this quick example!
