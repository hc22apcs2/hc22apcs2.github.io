---
layout: post
title: CS162 - 2B
parent: Introduction to Computer Science II
---

{% include toc.md %}

## What will happen when you delete a pointer 2 times in a row?

{% capture code %}
{% highlight cpp linenos %}
int *p = new int;
delete p;
delete p;
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

This will crash. The first delete call will deallocate the data that ``p`` points to. Then, ``p`` still points to the same slot, but there's nothing in that slot to delete, so the next delete call will crash the program.

However, if you delete the ``null pointer``, either once or multiple times, nothing will happen. This is specified by the C++ Standard. You should always assign ``p`` to the ``null pointer`` immediately after deleting.

## Now it's time to build a simple linked list:

{% capture code %}
{% highlight cpp linenos %}
struct Node
{
    int data;
    Node* pNext;
};

Node* pHead;

//Add the first Node
pHead = new Node;
pHead->data = 1;
pHead->pNext = nullptr;

//Add the second Node
pHead->pNext = new Node;
pHead->pNext->data = 2;
pHead->pNext->pNext = nullptr;

//Add the third Node
pHead->pNext->pNext = new Node;
pHead->pNext->pNext->data = 3;
pHead->pNext->pNext->pNext = nullptr;

//Add the fourth Node
pHead->pNext->pNext->pNext = new Node;
pHead->pNext->pNext->pNext->data = 4;
pHead->pNext->pNext->pNext->pNext = nullptr;

//Add the n-th Node
pHead->...->pNext = new Node;
pHead->...->pNext->data = n;
pHead->...->pNext->pNext = nullptr;
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

As you can see, to add a new Node we need a lot of work to do, to make the work easier, we declare a pointer to help us:

{% capture code %}
{% highlight cpp linenos %}
Node* pHead;
Node* cur;

//Add the first Node
pHead = new Node;
cur = pHead;
cur->data = 1;
cur->pNext = nullptr;

//Add the second Node
cur->pNext = new Node;
cur = cur->pNext;
cur->data = 2;
cur->pNext = nullptr;

//Add the third Node
cur->pNext = new Node;
cur = cur->pNext;
cur->data = 3;
cur->pNext = nullptr;

//Add the fourth Node
cur->pNext = new Node;
cur = cur->pNext;
cur->data = 4;
cur->pNext = nullptr;

//Add the n-th Node
cur->pNext = new Node;
cur = cur->pNext;
cur->data = n;
cur->pNext = nullptr;
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

## Student's code


{% capture code %}
{% highlight cpp linenos %}
struct Node{
    int data;
    Node* pNext;
};

int main(){

    Node* pHead = nullptr;
    Node* cur = pHead;
    
    // Input the linked list
    while(true)
    {
        int x;
        cin>>x;
        if(x == 0) {
            //if (cur) cur->pNext = nullptr; 
            break;
        }
        
        if(pHead == nullptr) {
            pHead = new Node;
            cur = pHead;
        }
        else {
            cur->pNext = new Node;
            cur = cur->pNext;
        }
        
        cur->data = x;
        //cur->pNext = nullptr;
    }
    
    // Print the linked list
    for (cur = pHead; cur != nullptr; cur = cur->pNext)
    {
        cout << cur->data << endl;
    }
    
    // Delete the linked list
    for (cur = pHead; cur != nullptr;)
    {
        Node* next = cur->pNext;
        delete cur;
        cur = next;
    }
    pHead = nullptr;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}

## Discussion:

### Which assignment is better? ``line 17`` or ``line 31``

``line 17`` will run faster because it assign the ``nullptr`` value only once.

``line 31`` will safer because it ensure the structure of the linked list every time you add a new Node.

### Teacher's note

At ``line 12``, we should not use the ``while(true)`` loop, the compiler will not know how to optimize your code, it's not a good practice.

## Teacher's code

{% capture code %}
{% highlight cpp linenos %}
struct Node{
    int data;
    Node* pNext;
};

void inputLL(Node*& pHead);
void displayLL(Node* cur);
void deleteLL(Node*& pHead);

int main(){
    Node* pHead = nullptr;
    
    // Input the linked list
    inputLL(pHead);
    
    // Print the linked list
    displayLL(pHead);
    
    // Delete the linked list
    deleteLL(pHead);
    return 0;
}

void inputLL(Node*& pHead) 
{    
    int x;
    cout << "Please input the number: ";
    cin>>x;
    while(x != 0)
    {
        if(pHead == nullptr) {
            pHead = new Node;
            cur = pHead;
        }
        else {
            cur->pNext = new Node;
            cur = cur->pNext;
        }
        
        cur->data = x;
        cur->pNext = nullptr;
        cout << "Please input the number: ";
        cin>>x;
    }
}

void displayLL(Node* cur)
{
    for (; cur != nullptr; cur = cur->pNext)
    {
        cout << cur->data << endl;
    }
}

void deleteLL(Node*& pHead)
{
    while(pHead != nullptr)
    {
        Node* next = pHead->pNext;
        delete pHead;
        pHead = next;
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
