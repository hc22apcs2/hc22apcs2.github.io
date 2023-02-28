---
layout: post
title: CS162 - 3B
parent: Introduction to Computer Science II
--- 

{% include toc.md %}

## Problem

7. Delete the first Node with value ``k`` from the list

{% capture code %}
{% highlight cpp linenos %}
void deleteANode(Node*& pHead, int k);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

8. Delete all nodes ``k`` from the list

{% capture code %}
{% highlight cpp linenos %}
void deleteAllNode(Node*& pHead, int k);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

## Solution

{% capture code %}
{% highlight cpp linenos %}
void deleteAt(Node* &pHead)
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
