---
layout: post
title: CS162 - 6B - Review
parent: Introduction to Computer Science II
grand_parent: Semester II
--- 

{% include toc.md %}

## Sections

### Pointer

- [CS161 - 1B](https://hc22apcs2.github.io/docs/CS162/b1/)

### Dynamically allocated array

- [CS162 - 1B/#array-allocation](https://hc22apcs2.github.io/docs/CS162/b1/#array-allocation)

### Linked List
1. Singly Linked List
- [CS162 - 2B/#build-linked-list](https://hc22apcs2.github.io/docs/CS162/b2b/#now-its-time-to-build-a-simple-linked-list)
- [CS162 - 3A](https://hc22apcs2.github.io/docs/CS162/b3a/#additional-sub-problem)
- [CS162 - 3B](https://hc22apcs2.github.io/docs/CS162/b3b/)

2. Ordered Linked List
- [CS162 - 4A/#singly-ordered-linked-list](https://hc22apcs2.github.io/docs/CS162/b4a/#introduction---singly-ordered-linked-list)

3. Doubly Linked List
- [CS162 - 4A/#double-linked-list](https://hc22apcs2.github.io/docs/CS162/b4a/#double-linked-list)
- [CS162 - 4B](https://hc22apcs2.github.io/docs/CS162/b4b/)

4. Circular Linked List
- [CS162 - 5A](https://hc22apcs2.github.io/docs/CS162/b5a/)
- [CS162 - 5B](https://hc22apcs2.github.io/docs/CS162/b5b/)
- [CS162 - 5B (Bonus)](https://hc22apcs2.github.io/docs/CS162/b5b-bonus/)

#### Linked List operations
- Create the list
- Display the list
- Remove the whole list
- Search an element in the list
- Insert a new item into the list
    - beginning
    - after `x`
    - before `x`
    - ...
- Remove a node from the list



|               |              Create               |              Display              |            Remove all             |              Search               |              Insert               |         Remove some nodes         |
| ------------- |:---------------------------------:|:---------------------------------:|:---------------------------------:|:---------------------------------:|:---------------------------------:|:---------------------------------:|
| **Singly LL**   | [code](https://ideone.com/DAnHcV) | [code](https://ideone.com/xLBVeD) | [code](https://ideone.com/89SReN) |               code                | [code](https://ideone.com/xwFzC5) | [code](https://ideone.com/VH1qiJ) |
| **Ordered LL**  |               code                | [code](https://ideone.com/xLBVeD) | [code](https://ideone.com/89SReN) |               code                | [code](https://ideone.com/1VitMx) | [code](https://ideone.com/VH1qiJ) |
| **Doubly LL**   |               code                |               code                | [code](https://ideone.com/fWDFRc) |               code                | [code](https://ideone.com/5ruPUt) | [code](https://ideone.com/HVcHCM) |
| **Circular LL** |               code                |               code                |               code                | [code](https://ideone.com/YSHeuK) |               code                | [code](https://ideone.com/TTDQON) |


### Data abstraction
- Data members
- Member functions

$\Rightarrow$ Struct

### Stack (LIFO)

- [CS162 - 6A/#stack](https://hc22apcs2.github.io/docs/CS162/b6a/#stack)

2 operations:
- push
- pop

If implementation based on `SLL`:
- `push` at the ***beginning*** of `SLL`.
- `pop` at the ***beginning*** of `SLL`.

#### Implementation
{: .no_toc}
{% capture code %}
{% highlight cpp linenos %}
struct MyStack {
    Node* pHead = nullptr;
    
    void push(Node* pNew);
    Node* pop();
};

void MyStack::push(Node* pNew) {
    pNew->pNext = pHead;
    pHead = pNew;
}

Node* MyStack::pop() {
    if(!pHead) return pHead;
    Node* tmp = pHead;
    pHead = pHead->pNext;
    return tmp;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

Full code (able to run): [here](https://ideone.com/PwPmtQ)

### Queue (FIFO)

- [CS162 - 6A/#queue](https://hc22apcs2.github.io/docs/CS162/b6a/#queue)

2 operations:
- enqueue
- dequeue

If the implementation is based on `SLL`:
- `dequeue` at the ***beginning*** of `SLL` 
- `enqueue` at the ***end*** of `SLL`.

#### Implementation
{: .no_toc}

{% capture code %}
{% highlight cpp linenos %}
struct MyQueue {
    Node* pHead = nullptr;
    Node* pTail = nullptr;
    
    void enqueue(Node* pNew);
    Node* dequeue();
};

void MyQueue::enqueue(Node* pNew) {
    if(!pHead) {
        pHead = pNew;
        pTail = pNew;
        pHead->pNext = nullptr;
    } else {
        pTail->pNext = pNew;
        pTail = pTail->pNext;
    }
}

Node* MyQueue::dequeue() {
    if(!pHead) return nullptr;
    Node* tmp = pHead;
    pHead = pHead->pNext;
    if(!pHead) pTail = nullptr;
    return tmp;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

Full code (able to run): [here](https://ideone.com/EEtT3g)

### Comparisions

#### Linked List and Array

|   Linked List    |            Array            |
|:----------------:|:---------------------------:|
| Access in $O(n)$ | Can random access in $O(1)$ |
|   Flexible size  |          Fixed size         |

## Notes
- Validity of pointer: pointing to `null` or not.
- Memory leaking: allocate $\Rightarrow$ deallocate.
- Doubly Linked List: algorithms have to be done the `DLL` way, don't try to use the `SLL` approaches.

## Q&A

#### Q1
{: .no_toc}
{% capture code %}
{% highlight cpp linenos %}
int *pArr;
pArr = new int[n];
delete[] pArr;
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

Why not `delete[n] pArr`? How does the system know the number of elements to delete?

#### A1
{: .no_toc}

The system stores the size somewhere. Where?

For some programming languages where arrays are "1-indexed", they try to store the size in the 0-th element. But `C++` arrays are "0-indexed", where does the system store the size? Go home and find out!

#### Editor's note:
{: .no_toc}

`delete[n] pArr` was actually what people used to do. However, the system now stores its size, so you don't have to (or rather, you can't) explicitly tell the system how many elements to delete (it would be dangerous if you delete the wrong number of elements). You can still do `delete[n] pArr` nowadays, but `n` will be ignored by the compiler.

Now, where is the size of the array stored? **Short answer: Magic** ([yes, the C++ Core Guidelines really said that](https://isocpp.org/wiki/faq/freestore-mgmt#num-elems-in-new-array)).

The longer answer is that there are two popular methods, which you can read by clicking on the link to the C++ Core Guidelines above if you are interested.

---

#### Q2
{: .no_toc}

Can we jump in the middle of an array and deallocate some of the elements but still use the un-deallocated elements?

#### A2
{: .no_toc}

Unexpected result, we don't know what will happen when we play around with the deallocation of the array. If you allocate the whole array, deallocate the whole array. You can still try deallocating in the middle of the array *at your own risk*.

---

#### Q3
{: .no_toc}

What happens when you allocate 0 slots and delete 0 slots of an array? Is it okay?

```cpp
int* a = new int[0];
delete[] a;
```

#### A3
{: .no_toc}

The allocation is okay, and the deallocation is... okay too. If you forget to deallocate the 0-sized array,... no memory is leaking too, but for the standard implementation you should write out the deallocation, it's a good practice.

#### Editor's note
{: .no_toc}

**Forgetting to deallocate a 0-sized array can also lead to memory leak**. It's more than just a good practice to deallocate even a 0-sized array.

When you allocate an array of `n` elements, *some* compilers will actually allocate `n + 1` elements: the extra element is for the size of the array. If you forget to delete the array, then this extra element will stay there the whole time.

Note that this behavior only applies for *some* compilers. If you return back to the Editor's note on Q1, this is one of the *magic* methods to store the size of a dynamically allocated array.

## Revision problems

### Given a singly linked list, you are asked to build the following functions:
{: .no_toc}

#### Print out the middle node. If the size of the `SLL` is odd, print the middle one. If the size of the `SLL` is even, print the left one.
{: .no_toc}

{% capture code %}
{% highlight cpp linenos %}
int getNumNode(Node* pHead) {
    int res=0;
    Node* cur = pHead;
    while(cur) {
        res++;
        cur = cur->pNext;
    }
    return res;
}

void printMiddle(Node* pHead) {
    if(pHead = nullptr) {
        cout<<"Nothing";
        return;
    }
    int numNode = getNumNode(pHead);
    int mid = (numNode - 1) / 2;
    Node* cur = pHead;
    while(mid--) cur = cur->pNext;
    cout<<"Middle value is "<<cur->data;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

#### Check if a given SLL is palindrome
{: .no_toc}

{% capture code %}
{% highlight cpp linenos %}
bool isPalindrome(Node* pHead) {
    int n = getNumNode(pHead);
    int* arr = new int[n];
    
    for(int i=0; i<n; i++) {
        arr[i] = pHead->data;
        pHead = pHead->pNext;
    }
    int left = 0, right = n-1;
    while(left <= right) {
        if(arr[left] != arr[right]) {
            delete[] arr;
            return false;
        }
        left++; right--;
    }
    delete[] arr;
    return true;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

There are a few more ways to implement the solution:



| Idea                                                                                                                                                                   | Time complexity | Memory complexity | Notes                                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| The above code                                                                                                                                                         | $O(n)$          | $O(n)$            | The allocation of consecutive blocks of memory (array) where $n$ is big is sometimes hard to achieve                                                |
| Iterate through the list and find the symmetric element to check whether they are identical or not                                                                     | $O(n^2)$        | $O(1)$            | Although the time complexity is way worse than the previous way, the memory complexity is just $O(1)$ which is very easy to allocate.               |
| Copy the `SLL` to another `SLL` and reverse it, then check the copied list with the original one to see if it's identical or not                                       | $O(n)$          | $O(n)$            | Although the memory complexity is the same as the first idea, the allocation does not need to be consecutive which is way easier to achieve.        |
| Detach the second half of the list into a new `SLL`, reverse the detached list and check it with the first half, after checking, re-attach it into the first half.     | $O(n)$          | $O(1)$            | Best complexity but more complex implementation, not recommended for paper-based exams.                                                             |
