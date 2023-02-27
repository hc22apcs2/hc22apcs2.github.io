---
layout: post
title: CS162 - 1B
parent: Introduction to Computer Science II
---

{% include toc.md %}

## What are pointers?

{% capture code %}
{% highlight cpp linenos %}
//Declare 2 int variables
int t = 5;
int x = 7;
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

We declare 2 variables of ``int`` in the program, the data will be stored in **RAM**.  
When the program is run, **RAM** has 2 parts:

- **Stack**: is small, belongs to the program, contain the data of variables declared in the program.
- **Heap**: is big, belongs to the system.

Thus, the data of 2 variables ``x`` and ``t`` will be stored in **Stack**.

![dxxxd](https://i.imgur.com/qxbms85.png)

{% capture code %}
{% highlight cpp linenos %}
//Declare a pointer of int
int* p; //p is a pointer of int
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

**A pointer** is (somewhat) a variables that contains the *address* of an other variables. It may be 32-bit or 64-bit depends on the operating system. Because ``p`` can be treated like a varible and was declared in the program, data of ``p`` will belong to Stack.

![](https://i.imgur.com/LFIf7XX.png)

{% capture code %}
{% highlight cpp linenos %}
//Assign address value for p
p = &t; //&t is the address of t
p = &x; //&x is the address of x
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

![](https://i.imgur.com/eDB2Ciz.png)

## Dereference

With ``p``, we know where the data of ``x`` is in our RAM. With this idea, via ``p`` we can access to the value of ``x`` and do anything with it.

{% capture code %}
{% highlight cpp linenos %}
x  = 10;
*p = 15; //dereference
cout << x; //Output 15
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

## Allocation and De-allocation

### Allocation (Dynamic allocation)

We can actually allocate data in Heap and use it for our program. 

{% capture code %}
{% highlight cpp linenos %}
p = new int; //allocation
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

This line of code mean the system will assign some slot for the variable of your program and give you the address of it.

![](https://i.imgur.com/8kQ9HBA.png)

### ⚠️Caution:

The data in Stack will be refreshed (deleted) when the program is started / ended. But the allocated data in Heap won't. In C/C++, we will have to return the allocated data so it can be free for other program to use. This is called de-allocation.

### De-allocation

{% capture code %}
{% highlight cpp linenos %}
delete p; //de-allocation
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

This line of code implies that we will return the variable allocated at that address. Note that ``p`` will not vanish after the ``delete`` function, we can re-use ``p`` in future.

{% capture code %}
{% highlight cpp linenos %}
p = new int;
*p = 10;
...
...
cout << *p << endl;
delete p;

p = new int;
...
...
delete p;

p = &t;
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Memory leaking

What will happen when we forget to return the allocated data to system? 

{% capture code %}
{% highlight cpp linenos %}
int* p;
p = new int; //Address: 01234567
*p = 5; //Use the variable at 01234567

p = new int; //Address: 76543210
*p = 7; //Use the variable at 76543210
delete p;
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

In this code, ``p`` leave the variable at ``01234567`` to control at ``76543210``.

After ``line 5`` of the code, we will forget the address of the previous variable we allocated. Although we returned the data in ``line 7`` but this only returned the variable at ``76543210``.

So how the system get back the data it allocated to our program at ``012345467``? We can only restart the computer to refresh our RAM. However nowaday with modern operating system, they can somehow get the data back.

The phenomenon of the system giving the data here and there but can't get it back is very common so they have a name for it: Memory leaking.

To avoid this, you should write ``delete`` function right after you allocate. In future, we may have some other ways to deal with it more efficiently.

## Why dynamic allocation?

Sometimes we may try to do this:

{% capture code %}
{% highlight cpp linenos %}
int main()
{
    int n;
    cin>>n;
    int a[n];
    ... //Do something
    return 0;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

This code will not run due to a compiler error. The syntax ``int a[n]`` is a declaration of a static array and it has to know the size of the array in advance. To declare an array with size is not known before, we can use dynamic allocation to achieve that:

### Array allocation

{% capture code %}
{% highlight cpp linenos %}
int main()
{
    int n;
    cin>>n;
    int *a = new int[n];
    ... //Do something
    return 0;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

``line 5`` of code mean the system will assign ``n`` *blocks* of ``int`` for the array of your program and give you the address of the first element in the array.

![](https://i.imgur.com/PsX0QwO.png)

To dereference the ``i-th`` element of the array, you can use the syntax ``*(a+i)`` with ``i`` is an integer value. The syntax above is equivalent to ``a[i]`` so you can use it like normal.

### "Fun" fact:

Due to the commutative property of addition operator:

``a[i] == *(a+i) == *(i+a) == i[a]``

In fact, the notation ``i[a]`` works in C/C++ code!  
You can check some reference [here](https://stackoverflow.com/questions/3612554/commutative-property-ai-ia).

### Array de-allocation

Note that with the dynamic array allocation, when you say ``a`` it means the pointer of the first element of the array. so when you use ``delete a;``, it will only return the first element of the array to the system, ``n-1`` other elements remain in control.

To return all the element, we use operator ``delete[]``.

{% capture code %}
{% highlight cpp linenos %}
delete a; // just delete the first block
delete[] a; // delete full block (delete all)
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

# Teacher's note

- Try to use dynamic array
- Don’t forget to deallocate the pointers

# In-class discussions

## What is the address of an uninitialized pointer?

Depends. More specifically, if you run that code on debug mode, it may have the address value of 0 (or null). But for optimization when you release your program, it will have some random 32-bit/64-bit value that maybe an address to some byte on Heap.

{% capture code %}
{% highlight cpp linenos %}
int *p; // a pointer , random address value
int t; // random value
int x; // random value
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

## What if we dereference a pointer after delete or an uninitialized pointer?

It most likely will be crashed because of the conflict. If the block of data at the address that the "unauthorized" pointer's pointing at and some other program is using that block of data, it will cause a conflict. But if you lucky enough (noone is using that block of data), the code will be run smoothly.

{% capture code %}
{% highlight cpp linenos %}
p = new int;
*p = 15;
delete p;

*p = 10; //dereference the "unauthorized" pointer
cout << *p; //sometimes if you lucky, this code will run perfectly
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

## What if we let a pointer point to other memory types

Let ``Book`` be a data type needs 200 bytes and as we know, ``int`` needs 4 bytes. Consider a scenario like this:

{% capture code %}
{% highlight cpp linenos %}
int* p; //int requires 4 bytes
p = new int; // 4 bytes (32-bit)

Book* q; //Book requires 200 bytes
q = new Book; // 4 bytes (32-bit)

//Somehow copy the address value of q to p, 
//this won't work but there're some ways to make it works.
//Note that all the pointer need the same amount of bytes.
q = p; 

//Dereference of pointer q
(*q).title = "...";
(*q).price = ...;

//"Dereference" of pointer p
//This line won't works because p is a int-typed pointer
//so it doesn't have the attribute "title".
(*p).title = "...";

//This dereference here actually valid, it will translate first 4 bytes 
//in 200 bytes of struct Book into an interger value and print it out.
cout << (*p) << endl; 
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

This code won't actually works because there're some false statements that can't be compiled.