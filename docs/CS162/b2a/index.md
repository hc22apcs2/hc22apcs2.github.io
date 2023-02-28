---
layout: post
title: CS162 - 2A
parent: Introduction to Computer Science II
---

{% include toc.md %}

{% capture code %}
{% highlight cpp linenos %}
#include <iostream>
#include <cstring>

using namespace std;

void checkSubstring(char s1[], char s2[], int n, int m);
void concatenate(char* s1, char* s2 char*& str);

int main() {
    char * stmp = new char[100000];
    cout << "Please type in the first string: ";
    cin.get(stmp, 100000, '\n');
    cin.ignore();
    
    int n = int(strlen(stmp));
    char *str1 = new char[n + 1];
    for (int i=0; i <= n; ++i) {
        str1[i] = stmp[i];
    }
    
    cout << "Please type in the second string: ";
    cin.get(stmp, 100000, '\n');
    cin.ignore();
    
    int m = int(strlen(stmp));
    char *str2 = new char[m + 1];
    for (int i=0; i <= m; ++i) {
        str2[i] = stmp[i];
    }
    
    delete[] stmp;
    
    checkSubstring(str1, str2, n, m);
    
    char* str;
    
    cout << '\n' << "The merged string is: ";
    concatenate(str1, str2, str);
    for (int i=0; i<m+n; i++) {
        cout<<str[i];
    }
    str[n+m] = '\0';
    cout << '\n';
    
    delete[] str1;
    delete[] str2;
    delete[] str;
    return 0;
}

void checkSubstring(char s1[], char s2[], int n, int m){
    for (int i = 0; i < m-n; ++i) {
        if (s2[i] == s1[0]) {
            int j;
            for(j = 1; j < n; ++j) {
                if(s1[j] != s2[i+j])
                {
                    break;
                }
            }
            if (j==n) {
                cout << "s1 is a substring of s2";
                return;
            }
        }
    }
    cout << "s1 is not a substring of s2";
}

void concatenate(char* s1, char* s2 char*& str) {
    int n = strlen(str1);
    int m = strlen(str2);
    str = new char[n+m+1];
    for (int i = 0; i < n; ++i) {
        str[i] = s1[i];
    }
    for (int i = 0; i <= m; ++i) {
        str[i + n] = s2[i];
    }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}