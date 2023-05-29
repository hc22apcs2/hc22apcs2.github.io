---
layout: post
title: CS162 - 3B
parent: Introduction to Computer Science II
grand_parent: Semester I
--- 

{% include toc.md %}

## Problem

1. Delete the first Node
```cpp
void deleteAtBeginning(Node* &pHead);
```

2. Delete the first Node with value ``k`` from the list
```cpp
void deleteANode(Node*& pHead, int k);
```

3. Delete all nodes ``k`` from the list
```cpp
void deleteAllNode(Node*& pHead, int k);
```

## Solution

{% capture code %}
{% highlight cpp linenos %}
void deleteAtBeginning(Node* &pHead)
{
    Node* cur = pHead;
    if (pHead) pHead = pHead->pNext;
    delete cur;
}

void deleteANode(Node*& pHead, int k)
{
    if(pHead != nullptr && pHead->data == k) {
        deleteAt(pHead);
        return;
    }

    Node* tmp = nullptr;
    Node* cur = pHead;
    while(cur != nullptr && cur->data != k) {
        tmp = cur;
        cur = cur->pNext;
    }
    if (cur == nullptr) return;
    tmp->pNext = cur->pNext;
    delete cur;
}

void deleteAllNode(Node*& pHead, int k)
{
    while (pHead != nullptr && pHead->data == k) deleteAt(pHead);
    if (pHead == nullptr) return;
    for (Node *cur = pHead; cur->pNext != nullptr; ) {
        if(cur->pNext->data == k)
            deleteAt(cur->pNext);
        else
            cur = cur->pNext;
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
