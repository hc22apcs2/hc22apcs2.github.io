---
layout: post
title: CS162 - 4A
parent: Introduction to Computer Science II
grand_parent: Semester I
--- 

{% include toc.md %}

# Introduction - Singly Ordered Linked List

Last time, we learn about ``Singly Linked List`` and how to implement it. In this lecture, we will extend that to ``Singly Ordered Linked List``.

A ``Singly Ordered Linked List`` is a ``Singly Linked List`` with it's value sorted in ascending order. Given a singly ordered linked list, named ``listA``, you're asked to implement the following functions:

## Problem statements

1. Insert a new Node ``x`` into the ordered list and still keep the list in order.
```cpp
void insertOrderedList(Node* &pHead, int x);
```

2. Given anoter orderd linked list, named ``listB``, merge the 2 lists into a new ``listC`` in whick its values are also sorted in order.
```cpp
void mergeOderedLists(Node* &pHA, Node* &pHB, Node* &pHC);
```
_<u>E.g.</u>_

$$
pHA \to 40 \to 65 \to 94 \to 127 \to 315 \\
pHB \to 15 \to 28 \to 77 \to 89 \to 90
$$

$$
\Rightarrow 
\begin{cases}
    pHC \to 15 \to 28 \to 40 \to 65 \to 77 \to 89 \to 90 \to 94 \to 127 \to 315 \\
    pHA \to \texttt{nullptr} \\
    pHB \to \texttt{nullptr}
\end{cases}
$$

## Problem 1

### Student's code

{% capture code %}
{% highlight cpp linenos %}
void insertOrderedList(Node* &pHead, int x) {
    Node* cur = pHead;
    while(cur!=nullptr && cur->pNext!=nullptr) {
        if(pHead->pNext->data > x) {
            Node* tmp = new Node;
            tmp->data = x;
            tmp->pNext = cur->pNext;
            cur->pNext = tmp;
            return;
        }
        cur = cur->pNext;
    }

    Node* tmp = new Node;
    tmp->data = x;
    tmp->pNext = cur->pNext;
    cur->pNext = tmp;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### What's wrong?

- In ``line 4`` he misused ``pHead`` with ``cur``.
- What if we have to insert a node into the first position?

### Fixed code

```cpp
void insertOrderedList(Node* &pHead, int x) {
    if(pHead == nullptr || pHead->data > x) {
        Node* tmp = new Node;
        tmp->data = x;
        tmp->pNext = pHead;
        pHead = tmp;
        return;
    }

    Node* cur = pHead;
    while(cur->pNext!=nullptr) {
        if(cur->pNext->data > x) {
            Node* tmp = new Node;
            tmp->data = x;
            tmp->pNext = cur->pNext;
            cur->pNext = tmp;
            return;
        }
        cur = cur->pNext;
    }

    Node* tmp = new Node;
    tmp->data = x;
    tmp->pNext = cur->pNext;
    cur->pNext = tmp;
}
```

## Problem 2

### Student's code

{% capture code %}
{% highlight cpp linenos %}
void mergeOderedLists(Node* &pHA, Node* &pHB, Node* &pHC) {
    pHC = new Node;
    Node *cur = pHC;

    while(pHA && pHB) {
        if(pHA->data < pHB->data) {
            cur->pNext = pHA;
            pHA = pHA->pNext;
        } else {
            cur->pNext = pHB;
            pHB = pHB->pNext;
        }
        cur = cur->pNext;
    }

    if(pHA) {
        cur->pNext = pHA;
    } else {
        cur->pNext = pHB;
    }

    pHC = pHC->pNext;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Discussion

- Didn't ensure the nullity of ``pHA`` or ``pHB`` in the if statement at ``line 16``.
- Forgot to delete the dummy node.

### Fixed code

```cpp
void mergeOderedLists(Node* &pHA, Node* &pHB, Node* &pHC) {
    pHC = new Node; //create a dummy node
    Node *cur = pHC;

    while(pHA && pHB) {
        if(pHA->data < pHB->data) {
            cur->pNext = pHA;
            pHA = pHA->pNext;
        } else {
            cur->pNext = pHB;
            pHB = pHB->pNext;
        }
        cur = cur->pNext;
    }

    if(pHA) {
        cur->pNext = pHA;
        pHA = nullptr;
    } else {
        cur->pNext = pHB;
        pHB = nullptr;
    }
    
    Node *tmp = pHC;
    pHC = pHC->pNext;
    delete tmp; //delete the dummy
}
```

My comment: `"Very eleganto!"`

---

# Double linked list

```cpp
struct DNode {
    int data;
    DNode* pPrev, *pNext;
};
```

With the new member - pointer ``DNode``, the list created base on these nodes are called ``Doubly Linked List``. Its name explained a lots about how it'll be used, it point to the previous node in the list.

## Problem statements

1. Insert ``x`` at the beginning of a DLL.
```cpp
void insertAtBeginning(DNode* &pHead, int x);
```

2. Insert ``x`` before ``k`` in a DLL.
```cpp
void insertBeforeK(DNode* &pHead, int x, int k);
```

## Problem 1

### Teacher's code
```cpp
void insertAtBeginning(DNode* &pHead, int x) {
    DNode* tmp = new DNode;
    tmp->data = x;
    tmp->pNext = pHead;
    tmp->pPrev = nullptr;
    if(pHead) pHead->pPrev = tmp;
    pHead = tmp;
}
```