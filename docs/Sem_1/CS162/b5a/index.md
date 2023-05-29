---
layout: post
title: CS162 - 5A
parent: Introduction to Computer Science II
grand_parent: Semester I
--- 

*Proofread by Huỳnh Hà Phương Linh*

{% include toc.md %}

## Introduction - Circular Linked List

``Circular Linked List`` is similar to ``SLL`` but the ``pNext`` of the last node points to the first node. Thus, if the ``CLL`` has only one node, that single node's ``pNext`` will point to itself.

### Problem statements

1. Find ``x``
```cpp
Node* findX(Node* pFirst, int x);
```

2. Remove the $1^{st}$ ``x``
```cpp
void remove1stX(Node* &pFirst, int x);
```

3. Remove all ``x`` s
```cpp
void removeAllXs(Node* &pFirst, int x);
```

### Problem 1
#### Student's code

{% capture code %}
{% highlight cpp linenos %}
Node* findX(Node* pFirst, int x) {
    Node* cur=pFirst;
    if(pFirst == nullptr)
        return nullptr;
    while(cur->data != x && cur->pNext != pFirst) {
        cur = cur->pNext;
    }
    if(cur->data == x)
        return cur;
    return nullptr;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Discussion

THE FIRST ACCEPTED CODE WRITEN BY **Ô HỚN SÂM**.

### Problem 2
#### Student's code

{% capture code %}
{% highlight cpp linenos %}
void remove1stX(Node* &pFirst, int x) {
    if(pFirst == nullptr) return;
    if(pFirst->pNext == pFirst) {
        if(pFirst->data == x) {
            delete pFirst;
            pFirst = nullptr;
        }
        return;
    }
    
    Node* cur = pFirst;
    while(cur->pNext->data != x &&
         cur->pNext->pNext != pFirst) {
        cur = cur->pNext;
    }
    if(cur->pNext->data == x) {
        Node* tmp = cur->pNext;
        cur->pNext = cur->pNext->pNext;
        if(tmp == pFirst) pFirst = tmp->pNext;
        delete tmp;
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Discussion

- The code doesn't delete the first node (``if statement`` at ``line 12-13``).
- If there are multiple nodes with value ``x`` and ``pFirst`` is the first one, the second node will be deleted instead.

#### Fixed code

{% capture code %}
{% highlight cpp linenos %}
void remove1stX(Node* &pFirst, int x) {
    if(pFirst == nullptr) return;
    if(pFirst->data == x) {
        Node* pLast = pFirst;
        while(pLast->pNext != pFirst) 
            pLast = pLast->pNext;
        
        if(pLast == pFirst) {
            delete pFirst;
            pFirst = nullptr;
            return;
        }
        
        pLast->pNext = pFirst->pNext;
        delete pFirst;
        pFirst = pLast->pNext;
        return;
    }
    
    Node* cur = pFirst;
    while(cur->pNext->data != x &&
         cur->pNext->pNext != pFirst->pNext) {
        cur = cur->pNext;
    }
    if(cur->pNext->data == x) {
        Node* tmp = cur->pNext;
        cur->pNext = cur->pNext->pNext;
        delete tmp;
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Problem 3
#### Student's code (Fixed)
{% capture code %}
{% highlight cpp linenos %}
void removeAllXs(Node* &pFirst, int x) {
    if(!pFirst) return;
    Node* cur = pFirst;
    while(cur->pNext != pFirst) {
        if(cur->pNext->data == x) {
            Node* tmp = cur->pNext->pNext;
            delete cur->pNext;
            cur->pNext = tmp;
        }
        else cur = cur->pNext;
    }
    if(cur->pNext->data == x) {
        Node* tmp = cur->pNext->pNext;
        if(cur->pNext == pFirst) pFirst = tmp;
        if(pFirst->pNext == pFirst)
            pFirst = nullptr;
        delete cur->pNext;
        cur->pNext = tmp;
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Discussion
- Time is running out so we couldn't discuss much. The code works just fine.