---
layout: post
title: CS162 - 4B
parent: Introduction to Computer Science II
--- 

{% include toc.md %}

## Continue with the last lecture

Last time with ``Singly Linked List`` we have inserted `x` before `k`. Now we will do the similar thing using  Doubly Linked List

With Singly Linked List we can't Insert `x` before `k` with our cur position right at `k` but can we do that with Doubly Linked List?

Let's give it a try!

### Problem statements

2. Insert ``x`` before ``k`` in a DLL.
```cpp
void insertB4K(DNode* &pHead, int x, int k);
```

3. Remove the first ``k`` from a DLL.
```cpp
void delete1K(DNode* &pHead, int k);
```

4. Remove all ``k``'s from a DLL.
```cpp
void deleteAllKs(DNode* &pHead, int k);
```

### Problem 1

#### Student's code

{% capture code %}
{% highlight cpp linenos %}
void insertB4K(DNode* &pHead, int x, int k) {
    if(pHead == nullptr)
        return;
    if(pHead->data == k){
        insertAtBeginning(pHead, x)
        return;
    }
    for(DNode* cur = pHead; cur != nullptr; cur = cur->pNext){
        if(cur->data == k){
            DNode* tmp = new DNode;
            tmp->data = x;
            tmp->pPrev = cur->pPrev;
            cur->pPrev->pNext = tmp;
            tmp->pNext = cur;
            cur->pPrev = tmp;
            break;
        }
    }
}

{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Discussion

The code is okay, though some modifications can be made.

- If we remove the ``if statement`` at ``line 4``, is it okay?
    - Yes, but we have to make some modifications at ``line 13`` because in case ``cur == pHead`` and ``cur`` is not pointing to any ``DNode`` (the DLL is empty).

- Can we remove the ``if statement`` at ``line 2``?
    - Yes, because if ``pHead == nullptr`` it will not run the ``for loop``.

- Does ``line 12`` safe?
    - Yes, it will handle the special case when ``cur->pPrev == nullptr`` which we are concerning.

#### Modified code

{% capture code %}
{% highlight cpp linenos %}
void insertBeforeK(DNode* &pHead, int x, int k) {
//    if(pHead == nullptr)
//        return;
//    if(pHead->data == k){
//        insertAtBeginning(pHead, x)
//        return;
//    }
    for(DNode* cur = pHead; cur != nullptr; cur = cur->pNext){
        if(cur->data == k){
            DNode* tmp = new DNode;
            tmp->data = x;
            tmp->pPrev = cur->pPrev;
            //-----------------------------------//
            if(cur->pPrev) cur->pPrev->pNext = tmp;
            else pHead = tmp;
            //-----------------------------------//
            tmp->pNext = cur;
            cur->pPrev = tmp;
            break;
        }
    }
}

{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Problem 2

#### Student's code

{% capture code %}
{% highlight cpp linenos %}
void delete1K(DNode* &pHead, int k)
{
    for(DNode *cur = pHead; cur; cur = cur->pNext) {
        if(cur->data == k) {
            cur->pNext->pPrev = cur->pPrev;
            if(cur->pPrev) 
                cur->pPrev->pNext = cur->pNext;
            else 
                pHead = cur->pNext;
            delete cur;
            break;
        }
    }
}

{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Discussion

- We should change ``break`` to ``return``.
    - Not necessarily.
- They forget to check the nulity of ``cur`` at ``line 5``

#### Fixed code

{% capture code %}
{% highlight cpp linenos %}
void delete1K(DNode* &pHead, int k)
{
    for(DNode *cur = pHead; cur; cur = cur->pNext) {
        if(cur->data == k) {
            //-------------------------------//
            if(cur->pNext)
                cur->pNext->pPrev = cur->pPrev;
            //-------------------------------//
            if(cur->pPrev) 
                cur->pPrev->pNext = cur->pNext;
            else 
                pHead = cur->pNext;
            delete cur;
            break;
        }
    }
}

{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

### Problem 3

#### Student's code

{% capture code %}
{% highlight cpp linenos %}
void DelAllks(DNode*& pHead, int k){
    insertAtBeginning(pHead, -1);
    for(DNode* cur = pHead->pNext; cur; cur=cur->pNext){
        if(cur->data == k){
            
            if(cur->pNext)
                cur->pNext->pPrev = cur->pPrev;
            
            cur->pPrev->pNext = cur->pNext;
            
            DNode* tmp = cur;
            cur = cur->pPrev;
            delete tmp;
        }  
    }
    delete1K(pHead, -1);
}

{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Discussion

- The idea of the dummy node ``-1`` is good, but is it necessarilly?
    - No, it's not necessarilly, notice that the order of deleting is not important, so we can treat the first node as the dummy node we desired.

#### Fixed code

{% capture code %}
{% highlight cpp linenos %}
void DelAllks(DNode*& pHead, int k){
    //insertAtBeginning(pHead, -1);
    for(DNode* cur = pHead->pNext; cur; cur=cur->pNext) {
        if(cur->data == k) {
            
            if(cur->pNext)
                cur->pNext->pPrev = cur->pPrev;
            
            cur->pPrev->pNext = cur->pNext;
            
            DNode* tmp = cur;
            cur = cur->pPrev;
            delete tmp;
        }  
    }
    //delete1K(pHead, -1);
    delete1K(pHead, k);
}

{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Discussion

- Oh no! Because the dummy node is deleted, the trying to access into the ``pHead`` in ``line 3`` didn't check the nulity.
- They tried to play around with the code in ``line 17``. But for the efficiency's sake, when the DLL doesn't have ``k`` anymore, ``delete1K()`` will iterate through the list for nothing.

#### Fixed code

{% capture code %}
{% highlight cpp linenos %}
void DelAllks(DNode*& pHead, int k){
    //insertAtBeginning(pHead, -1);
    if(!pHead) return;
    for(DNode* cur = pHead->pNext; cur; cur=cur->pNext) {
        if(cur->data == k) {
            
            if(cur->pNext)
                cur->pNext->pPrev = cur->pPrev;
            
            cur->pPrev->pNext = cur->pNext;
            
            DNode* tmp = cur;
            cur = cur->pPrev;
            delete tmp;
        }  
    }
    //delete1K(pHead, -1);
    if(pHead->data == k)
        delete1K(pHead, k);
}

{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Teacher's comment

We are using DLL but the code make it seems like we still code in SLL phylosophy.

#### Teacher's code

{% capture code %}
{% highlight cpp linenos %}
void DelAllks(DNode*& pHead, int k) {
    for(DNode* cur = pHead; cur;)
        if(cur->data == k) {
            if(cur->pNext)
                cur->pNext->pPrev = cur->pPrev;
            if(cur->pPrev)
                cur->pPrev->pNext = cur->pNext;
            else pHead = pHead->pNext;
            DNode* tmp = cur;
            cur = cur->pNext;
            delete tmp;
        }  
        else cur = cur->pNext;
}

{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}