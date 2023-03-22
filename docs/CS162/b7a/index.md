---
layout: post
title: CS162 - 7A
parent: Introduction to Computer Science II
--- 

{% include toc.md %}

## Recursion

Is another way to do the same thing again and again by self-referencing.

```cpp
void A(int a, int b) {
    //do something something
    A(b, a);
    //do something something
}
```

![](E9KSOdx.gif)

- The action of getting back to the previous function call in recursion is called **backtracking**. 
- Using recursion can make a repetition but sometimes loops are better than recursion.
- Recursion looks simpler but hard to debug. 
- All the problems solved by recursion can be solved by loops (by rebuild the stack).

Look at the code below, can you tell what it does?

{% capture code %}
{% highlight cpp linenos %}
void strange() {
    int t;
    cin >> t;
    if (t!=0) {
        strange();
        cout << t << " ";
    }
}

int main {
    cout << "Pls input numbers (0 to stop)" << endl;
    strange();
    cout << endl;
    return 0;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

**Answer:** It will input a list of numbers (until 0) then print that list in *reversed* order.

## Problem statement(s)

1. Given a positive integer $N$, you are asked to implement a program to print out all permutations of $1$ to $N$.

## Problem 1

### Student's code

{% capture code %}
{% highlight cpp linenos %}
#include <iostream>
using namespace std;

void Permutation(int i, int n, int* &arr, bool* &avail);

int main() {
    int n;
    cout << "Pls input an integer number: ";
    cin >> n;
    int* arr = new int[n];
    bool* avail = new bool[n];
    for(int i = 0; i < n; i++)
        avail[i] = 1;
    
    Permutation(0, n, arr, avail);
    
    delete[] arr;
    delete[] avail;
    return 0;
}

void Permutation(int i, int n, int* &arr, bool* &avail) {
    if(i==n) {
        for(int j=0; j<n; j++) cout<<arr[j]<<" ";
        cout<<"\n";
        return;
    }
    
    for(int x=0; x<n; x++) {
        if(avail[x]) {
            arr[i] = x+1;
            avail[x] = 0;
            Permutation(i+1, n, arr, avail);
            avail[x] = 1;
        }
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}