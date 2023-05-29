---
layout: post
title: CS162 - 5B (Bonus)
parent: Introduction to Computer Science II
grand_parent: Semester I
--- 

*Proofread by Huỳnh Hà Phương Linh*

{% include toc.md %}

## Introduction - Circular Linked List (cont.)

This problem was introduced to class 22APCS1. I was lucky enough to attend the lecture and share with y'all 🥰.

The problem is about cycle detection, you can go to <a href="#references">references</a> section to see more.

## Problem statement

You are given a linked list with the last node (`pLast`) either pointing to `nullptr` or a node inside the linked list. When `pLast` points to `nullptr`, there are no loops inside the linked list. Otherwise there is **exactly one** loop.

Giving you too much information of the list would be too easy so only the address of the first node of the list is given.

Your job is to find if there is any loop.

```cpp
bool isLooped(Node* pFirst);
```

The problem seems easy at first, isn't it? I'll provide you with multiple solutions but first try to solve the problem yourself and see how good your solution(s) is/are.

## Trivial solution

The simplest solution to this problem is to add an attribute to show if a node has been visited.

{% capture code %}
{% highlight cpp linenos %}
struct Node {
    int data;
    Node* pNext;
    bool isVisited;
};
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

The code may look like this:

{% capture code %}
{% highlight cpp linenos %}
bool isLooped(Node* pFirst) {
    while(pFirst != nullptr && pFirst->isVisited == false) {
        pFirst->isVisited = true;
        pFirst = pFirst->pNext;
    }
    return pFirst != nullptr;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

After iterating through the list, if there's a node pointing to `nullptr`, the linked list has no loops and vice versa.

The code is simple and it works, but we have modified the structure of the node and increase the memory cost. Is there any solution that requires less memory?

## Memory-friendly solution

Notice that as we iterate through the list, the distance between the first node and the iterating node grows before crossing the LL's tail. Hence, if a loop exists, at some point the distance will stop growing. With that observation, we came up with the following code:

{% capture code %}
{% highlight cpp linenos %}
bool isLooped(Node* pFirst) {
    if(pFirst == nullptr) return false;
    
    int savedDistance = 0;
    Node* cur = pFirst->pNext;
    
    while(cur != nullptr) {
        int distance = 0;
        for(Node* tmp=pFirst; tmp != cur; tmp = tmp->pNext)
            distance++;
        
        if(distance > savedDistance) {
            savedDistance = distance;
        } else {
            return true;
        }
        
        cur = cur->pNext;
    }
    
    return false;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

It is easy to see that the code will iterate approximately $n^2$ times ($n$ is the number of node in the list). But the code does not cost memory for every single node like the previous solution. Can we do better?

## Tortoise and Hare solution

Assuming we have 2 iterators: `tortoise` and `hare`, both starting at the first node. The `tortoise` and `hare` will move 1 and 2 steps ahead respectively. If there's a loop, the`tortoise` and `hare` will intersect (proof below). The code might look like this:

{% capture code %}
{% highlight cpp linenos %}
bool isLooped(Node* pFirst) {
    Node *tortoise = pFirst;
    Node *hare     = pFirst;

    while (   tortoise    != nullptr
           && hare        != nullptr
           && hare->pNext != nullptr) {
        tortoise = tortoise->pNext;
        hare = hare->pNext->pNext;
        if (tortoise == hare)
            return true;
    }

    return false;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

The code looks clean but is it alright? Let's have a look!

If there are no loops, the function returns the expected answer - false, so we just have to focus on the case with a loop.

If there's a loop, the `tortoise` and `hare` will both enter the loop after approximately $2n$ iterations. In the loop, they chase around in circle. Notice that every time the `tortoise` and `hare` move, the distance between them decrease by $1$ so the max number of iterations is $2n$. So the max number of iterations is $4n$ for those two to meet. (Actually it's $\approx2n$).

There we have it, a memory-friendly and fast solution! This algorithm is known as ***Floyd’s Cycle Finding Algorithm***.

## SOLUTION

This solution is proposed by **Lê Hữu Nghĩa**. The number of iterations is almost similar to ***Floyd’s Cycle Finding Algorithm***. You can calculate the number of iterations yourself as an exercise😉.

{% capture code %}
{% highlight cpp linenos %}
bool isLooped(Node* pFirst) {
    if(pFirst == nullptr) return false;
    if(pFirst->pNext == nullptr) return false;
    int steps = 1;
    Node* cur1 = pFirst
    Node* cur2 = pFirst->pNext;
    while(true) {
        for(int i=1; i<=steps; i++) {
            cur2 = cur2->pNext;
            if(cur2 == nullptr) return false;
            if(cur2 == cur1) return true;
        }
        for(int i=1; i<=steps; i++) {
            cur1 = cur1->pNext;
            if(cur1 == nullptr) return false;
            if(cur1 == cur2) return true;
        }
        steps *= 2;
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

## References
- [Wiki (Circle detection)](https://en.wikipedia.org/wiki/Cycle_detection)
- [Funny video about Floyd’s Cycle Finding Algorithm](https://www.youtube.com/watch?v=pKO9UjSeLew)