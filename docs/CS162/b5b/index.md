---
layout: post
title: CS162 - 5B
parent: Introduction to Computer Science II
--- 

*Proofread by Huỳnh Hà Phương Linh*

{% include toc.md %}

## Introduction - Circular Linked List (cont.)

Problem 1 appeared in the midterm exam 2 years ago.

## Problem statements

1. Given a circular linked list, delete the k-th element in the list. Delete the next k-th element counting from the previous one. Repeating the operation until the list is deleted.
```cpp
void removeBasedOnK(Node* &pHead, int k);
```

## Problem 1


### Student's code

{% capture code %}
{% highlight cpp linenos %}
void deleteLL(Node* &pFirst) {
    Node* cur = pFirst;
    while(cur->pNext != cur) {
        Node* tmp = cur;
        cur = cur->pNext;
        delete tmp;
    }
    delete cur;
    pFirst = nullptr;
}

void removeBasedOnK(Node* &pFirst, int k)
{
    int t = k;
    if (t == 1) {
        deleteLL(pFirst);
        return;
    }
    t--;
    Node* cur = pFirst->pNext;
    while(cur != nullptr) {
        if(t==1) {
            t = k;
            Node* tmp = cur->pNext;
            cur->pNext = cur->pNext->pNext;
            delete tmp;
        } else {
            t--;
            if(cur->pNext == cur) {
                delete cur;
                pFirst = nullptr;
            } 
            else cur = cur->pNext;
        }
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Discussion

- In the case of `k==1` (`deleteLL(pFirst)` invoked), when `cur == pLast`, if `CLL` has 2 or more nodes, the condition at `line 3` would never be satisfied. 
- They forgot to print out the deleted nodes. 
- When `sizeof(CLL) == 1` and `k==2`, the condition at`line 29` will be satisfied and the program will try to access `pNext` of the deleted node.
- At `line 20`, it should have been `Node* cur = pFirst`.


### Fixed code (they... then wrote a whole new code 🥲)

{% capture code %}
{% highlight cpp linenos %}
void removeBasedOnK(Node* &pFirst, int k) {
    if (k == 1) {
        deleteLL(pFirst);
        return;
    }
    Node* cur = pFirst;
    for(int i=1; i < k-1; i++) {
        cur = cur->pNext;
    }
    cout << cur->pNext->data << " ";
    Node* tmp = cur->pNext;
    cur->pNext = tmp->pNext;
    delete tmp;
    while(cur != nullptr) {
        Node* cur = pFirst;
        for(int i=1; i < k-1; i++) {
            cur = cur->pNext;
        }
        cout << cur->pNext->data << " ";
        if(cur->pNext->pNext != cur) {
            Node* tmp = cur->pNext;
            cur->pNext = tmp->pNext;
            delete tmp;
        }
        else if(cur->pNext == cur) {
            Node* tmp = cur;
            cur = nullptr;
            delete tmp;
            pFirst = nullptr;
        }
        else {
            Node* tmp = cur->pNext;
            cur->pNext = cur;
            delete tmp;
        }
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Discussion

The code is almost okay due to some mistakes. Students are assigned to improve this code at home.

### Fixed code (...yes, new code)

{% capture code %}
{% highlight cpp linenos %}
void deleteNext(Node* cur) {
    Node* tmp = cur->pNext;
    cur->pNext = tmp->pNext;
    cout << tmp->data << " ";
    delete tmp;
}

void removeBasedOnK(Node* &pFirst, int k) {
    if(pFirst == nullptr) return;
    int n = 1;
    for(Node* p = pFirst; pFirst->pNext != p; pFirst = pFirst->pNext)
        n++;
    for(;n;n--) {
        for(int t = (k+n-1)%n; t--; pFirst = pFirst->pNext);
        deleteNext(pFirst);
    }
    pFirst = nullptr;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

Ehm... This code is a bit... meh, so I'll write down an alternative one.

### "Prettier" one

{% capture code %}
{% highlight cpp linenos %}
void deleteNext(Node* cur) {
    Node* tmp = cur->pNext;
    cur->pNext = tmp->pNext;
    cout << tmp->data << " ";
    delete tmp;
}

void removeBasedOnK(Node* &pFirst, int k) {
    if(pFirst == nullptr) return;
    int n = 1;
    Node* mFirst = pFirst;
    while(pFirst->pNext != mFirst)
    {
        pFirst = pFirst->pNext;
        n++;
    }
    while(n > 0) {
        for(int t = 1; t <= (k+n-1) % n; t++)
            pFirst = pFirst->pNext;
        deleteNext(pFirst);
        n--;
    }
    pFirst = nullptr;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

And a commented one.

### "Commented" version

The key idea is to get right before the meant-to-be-deleted node and delete it.

{% capture code %}
{% highlight cpp linenos %}
void deleteNext(Node* cur) {
    Node* tmp = cur->pNext;
    cur->pNext = tmp->pNext;
    cout << tmp->data << " ";
    delete tmp;
}

void removeBasedOnK(Node* &pFirst, int k) {
    if(pFirst == nullptr) return;
    
    //This first block of code will compute the size of the CLL 
    //(stored in n) and set pFirst point to the last element
    int n = 1;
    Node* tmp = pFirst;
    while(pFirst->pNext != tmp)
    {
        pFirst = pFirst->pNext;
        n++;
    }
    
    //This while loop will handle the deletion
    while(n > 0) {
        //Loop through k-1 node to get right before the 
        //meant-to-be-deleted node and delete it
        for(int t = 1; t <= (k+n-1) % n; t++)
            pFirst = pFirst->pNext;
        deleteNext(pFirst);
        n--; //Reduce the CLL size
    }
    pFirst = nullptr; //Self-explained
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}