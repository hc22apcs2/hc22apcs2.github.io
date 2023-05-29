---
layout: post
title: CS162 - 7B (not really...)
parent: Introduction to Computer Science II
grand_parent: Semester II
--- 

{% include toc.md %}

## Lời mở đầu

Cũng là lời cảnh báo: Bài viết này là bài viết đền bù vì mình đã trễ học tiết 7B. Bài viết này là do mình bịa ra (không đi học nên không biết thầy giảng gì) nên sẽ được viết bằng tiếng Việt cho dễ hiểu. Và bài viết này được tẩm đá.

Vì nhận thấy sự đau khổ của mọi người khi học đệ quy nên mình muốn chia sẻ mọi người một chút về việc làm sao để hiểu được đệ quy.

## Đệ quy có khó không?

Có.

## Liệu rằng bạn có hiểu được đệ quy không?

Chắn chắn.

## Tại sao bạn lại chật vật với đệ quy?

Đệ quy là một concept khó nuốt cho những người lần đầu tiếp xúc, vì thế không khó hiểu khi bạn không hiểu được đệ quy ngay lập tức dù định nghĩa nó rất đơn giản: "Lặp đi lặp lại một việc giống hệt nhau nhiều lần".

Tuy là khó nuốt nhưng mình thấy đa số những người học lập trình nói chung (không chỉ dân học lập trình thi đấu) sau khi tiếp xúc với concept một thời gian thì sẽ hiểu rất rõ về cách đệ quy hoạt động. Vì thế mình tin chắc mọi người sẽ làm được!

Để đệ quy thân thương và gần gũi hơn, có lẽ chúng ta nên xuất phát từ những hàm đơn giản trước.

## Giai thừa!

Trong môn toán thân thương chắc hẳn mọi người đã quen với định nghĩa của $n!$, nó được định nghĩa như sau:

$$n! = 1\times2\times3\times\cdots\times n$$

Thậm chí nó còn có định nghĩa đệ quy nữa:

$$n! = \begin{cases}1 && , 0\le n\le1\\n\times(n-1)!&&,1<n\end{cases}$$

Khi viết nó theo một hàm đệ quy trong `C++`, ta có thể viết như sau:

{% capture code %}{% highlight cpp linenos %}
int factorial(int n) {
    if(n<=1) return 1;
    return n * factorial(n-1);
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

### Phân tích cấu trúc

Hàm `factorial(n)` được dùng để tính $n!$ và ta có thể thấy nó rất tương đồng với định nghĩa dạng đệ quy của toán học. Thế nhưng ta cần phân tích kỹ lưỡng cấu trúc của hàm trên nhằm mục đích hiểu rõ hơn về đệ quy.

#### Trạng thái
{: .no_toc}

Trạng thái là bộ tham số của hàm, quy định những gì hàm đệ quy sẽ làm trong đó.

Trạng thái này của đệ quy thường sẽ phụ thuộc bởi trạng thái khác.

Ví dụ trong hàm `factorial(n)` trên thì bộ tham số quy định trạng thái là $(n)$. Trạng thái $(n)$ sẽ phụ thuộc vào trạng thái $(n-1)$.

#### Chuyển trạng thái
{: .no_toc}

Là cách thức các trạng thái phụ thuộc/quy định lẫn nhau.

#### Neo (Anchor)
{: .no_toc}

Hay còn được gọi là trạng thái suy biến, đây là trạng thái mà không phụ thuộc vào trạng thái nào khác, trạng thái này sẽ được quy định trước những gì sẽ được làm khi hàm đệ quy gọi trạng thái này.

Ví dụ trong hàm `factorial(n)` trên thì neo đệ quy của mình chính là 2 trạng thái $(0)$ và $(1)$. Hai trạng thái này đã được quy định trước giá trị trả về và không phụ thuộc vào trạng thái trước.

## Tổ hợp

Lại lấy một ví dụ trong toán học - Tổ hợp $\binom{n}{k}$. Nó được định nghĩa là số cách chọn (không quan trọng thứ tự) $k$ phần tử trong một nhóm gồm $n$ phần tử.

Nó còn có định nghĩa đệ quy sau:

$$\displaystyle \binom{n}{k} = 
\begin{cases}
0 &&, k < 0 \text{ or } n < k\\
1 &&, k = 0 \text{ or } n = k\\
\binom{n-1}{k} + \binom{n-1}{k-1} &&, 0 < k < n
\end{cases}$$

Khi viết nó theo một hàm đệ quy trong C++, ta có thể viết như sau:

{% capture code %}{% highlight cpp linenos %}
int binomial(int n, int k) {
    if(k < 0 || n < k) return 0;
    if(k == 0 || k == n) return 1;
    return binomial(n-1, k-1) + 
           binomail(n-1, k);
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

### Phân tích cấu trúc

#### Trạng thái
{: .no_toc}

Trạng thái của hàm này là bộ số $(n, k)$.

#### Neo (Anchor)
{: .no_toc}

Neo của hàm này là những bộ số thỏa mãn `dòng 2, 3` của code.

Qua 2 ví dụ, ta sẽ thường thấy neo của hàm đệ quy sẽ được viết ở đầu hàm. Sau đó mới tới phần chuyển trạng thái.

{% capture code %}{% highlight cpp linenos %}
void recursion(int a, int b, int c, ...) {
    // Here goes the anchor
    
    // Here goes the "Chuyển trạng thái"
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

#### Cây đệ quy
{: .no_toc}

Một vấn đề khó khăn khi học đệ quy đó là tưởng tượng cách chạy của nó, ta thường được bảo là đệ quy cơ bản là stack, nhưng khi chạy demo trong đầu thì sẽ rất khó để hình dung bức tranh toàn cảnh.

Vì thế mình xin được giới thiệu: Cây đệ quy.

Cây đệ quy là một cấu trúc hình tượng hóa với tính năng ưu việt: tốn giấy, nhưng dễ hiểu. Mình sẽ vẽ trước một cây đệ quy cho trạng thái $(4, 2)$ như sau:

![](uRo9WZI.gif)


Khi mình nói tới cây thì có nghĩa là một cái "sơ đồ mối quan hệ" (Về sau định nghĩa cây sẽ khác). Mỗi trạng thái được gọi là một đỉnh. Với trạng thái ở trên cùng được gọi là đỉnh gốc (root). 

Đỉnh hiện tại sẽ được nối bằng những cạnh màu tím với những trạng thái mà nó phụ thuộc và ở độ cao thấp hơn so với đỉnh hiện tại. Những đỉnh được tô đỏ chính là neo.

Dựa vào cây đệ quy ta có thể dễ dàng mô phỏng lại quá trình một hàm đệ quy bất kỳ chạy như thế nào!

#### Bài tập nhỏ
{: .no_toc}

Hãy chạy lại cây đệ quy với một vài trạng thái khác, như $(4, 3)$, $(5, 2)$, $(10, 5)$.

Hãy thử vẽ luôn cây đệ quy cho hàm `factorial(n)` nữa nhé! (Dễ òm à)

## Sinh dãy nhị phân

Tiếp theo sẽ lại là một bài toán cổ điển khác: Liệt kê dãy nhị phân độ dài $n$.

Để liệt kê thì ta cần để tâm đến việc mỗi vị trí trong $n$ vị trí sẽ có đúng $2$ cách điền (là $0$ hoặc $1$). Cách điền của mỗi vị trí sẽ **không phụ thuộc** vào cách điền của các vị trí còn lại.

Hàm sinh nhị phân có thể được viết như sau:

{% capture code %}{% highlight cpp linenos %}
int n;

void genBinary(int i, int* filled) {
    if(i == n) {
        print(filled);
        return;
    }
    
    //Điền vào ô thứ i số 0
    filled[i] = 0;
    genBinary(i+1, filled);
    filled[i] = -1;
    
    //Điền vào ô thứ i số 1
    filled[i] = 1;
    genBinary(i+1, filled);
    filled[i] = -1;
}

int main() {
    cin>>n;
    int* filled = new int[n];
    for(int i=0; i<n; i++) filled[i] = -1;
    genBinary(0, filled);
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

### Phân tích cấu trúc

Khác với 2 hàm trước, hàm đệ quy này là một hàm `void` dùng để chỉ thực thi một việc gì đó (ở đây là sinh dãy nhị phân).

Biến `i` là vị trí mình đang chuẩn bị điền vào. Mảng `filled` ở đây là những giá trị đã được điền. Khi `filled[i] = -1`, nghĩa là vị trí này chưa được điền.

#### Trạng thái
{: .no_toc}

Ở hàm này, trạng thái sẽ là cặp 2 giá trị `i` và mảng `filled`.

#### Neo
{: .no_toc}

Neo ở đây là khi mình đã điền hết thành công $n$ vị trí và mình đi tới vị trí không cần điền. Lúc này mình chỉ việc 

#### Tính kiên định của trạng thái
{: .no_toc}

Nếu bạn để ý, ở `dòng 12` và `dòng 17` sẽ có một dòng lệnh "Bảo toàn tính kiên định của trạng thái".

Trạng thái cần có tính kiên định. Khi bạn vẽ cây đệ quy ra mà không có 2 dòng code bảo toàn như đã nêu trên, bạn sẽ nhận ra rằng khi đi từ đỉnh thấp lên đỉnh cao, bạn đã vô tình thay đổi trạng thái của đỉnh cao hơn (Thay đổi mảng `filled`) và điều này sẽ không còn đúng với cây đệ quy trạng thái nữa! Vì vậy khi ta thay đổi một biến nào đó để chuyển trạng thái, ta cần phải bảo toàn tính kiên định của trạng thái trước khi chuyển đến trạng thái tiếp theo.

{% capture code %}{% highlight cpp linenos %}
void recursion(int a, int b, int c, ...) {
    // Here goes the anchor
    
    // Here goes the changing of variables
    // Here goes the "Chuyển trạng thái 1"
    // Here goes the "Bảo toàn tính kiên định"
    
    // Here goes the changing of variables
    // Here goes the "Chuyển trạng thái 2"
    // Here goes the "Bảo toàn tính kiên định"
    
    // Here goes the changing of variables
    // Here goes the "Chuyển trạng thái 3"
    // Here goes the "Bảo toàn tính kiên định"
    
    // ...
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

Thật ra với đoạn code trên, mọi người có thể sẽ tự hỏi "Tại sao lại chỉ bảo toàn tính kiên định của mảng `filled` mà lại không bảo toàn cho biến `i`"?

Thực chất với biến `i`, mình truyền vào hàm chuyển trạng thái là một bản copy của nó (pass by value) nên giá trị thực của biến `i` không bị thay đổi tại trạng thái đó. Ngược lại với mảng `filled` thì mình không tạo ra một bản copy mà mình truyền thằng mảng vào (pass by reference (kind of)) nên mình cần phải thực hiện bước bảo toàn.

Nếu mình có thể tạo ra bản copy của `filled` thì thực chất mình cũng không cần phải bảo toàn luôn.

{% capture code %}{% highlight cpp linenos %}
int n;

void genBinary(int i, int* filled) {
    if(i == n) {
        print(filled);
        return;
    }
    
    int* newFilled = new int[n];
    
    //Điền vào ô thứ i số 0
    for(int j=0; j<i; j++) newFilled[j] = filled[j];
    newFilled[i] = 0;
    genBinary(i+1, newFilled);
    
    //Điền vào ô thứ i số 1
    for(int j=0; j<i; j++) newFilled[j] = filled[j];
    newFilled[i] = 1;
    genBinary(i+1, filled);
    
    delete[] newFilled;
}

int main() {
    cin>>n;
    int* filled = new int[n];
    for(int i=0; i<n; i++) filled[i] = -1;
    genBinary(0, filled);
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

Tuy nhiên làm như vậy sẽ rất tốn bộ nhớ, vì thế người ta thường hy sinh tốn thêm chút não để bảo toàn trạng thái hơn là hy sinh bộ nhớ để tạo bản copy.

### Áp dụng?

Tại tiết học CS162-7B thì mình đã làm một bài toán "cái túi": Cho một cái túi đựng được tối đa $W$ trọng lượng, $n$ món vật, món thứ $i$ có trọng lượng là $w_i$ và giá trị là $v_i$. Tìm cách để chọn các món đồ sao cho tổng trọng lượng không quá tải cái túi và được tổng giá trị là lớn nhất.

Bài toán này có thể giải quyết bằng việc trừu tượng hóa việc chọn các món đồ thành một dãy nhị phân độ dài $n$, nếu vị trí đó ứng với số $1$ thì mình sẽ chọn món đồ đó, và ngược lại.

Mình có thể copy toàn bộ code sinh dãy nhị phân trên:

{% capture code %}{% highlight cpp linenos %}
#include <iostream>

using namespace std;

int n;
int W;
int* w;
int* v;
int* bestOption;

void updateOption(int* cur) {
    int bestW = 0;
    int bestV = 0;
    int curW = 0;
    int curV = 0;
    
    for(int i=0; i<n; i++)
        bestW += bestOption[i] * w[i];
    for(int i=0; i<n; i++)
        bestV += bestOption[i] * v[i];
    for(int i=0; i<n; i++)
        curW += cur[i] * w[i];
    for(int i=0; i<n; i++)
        curV += cur[i] * v[i];
        
    if(curW > W) return;
    
    if(curV > bestV){
        bestV = curV;
        for(int i=0; i<n; i++)
            bestOption[i] = cur[i];
    }
}

void genBinary(int i, int* filled) {
    if(i == n) {
        updateOption(filled);
        return;
    }
    
    int* newFilled = new int[n];
    
    //Điền vào ô thứ i số 0
    filled[i] = 0;
    genBinary(i+1, filled);
    filled[i] = -1;
    
    //Điền vào ô thứ i số 1
    filled[i] = 1;
    genBinary(i+1, filled);
    filled[i] = -1;
}

int main() {
    cin>>n>>W;
    w = new int[n];
    v = new int[n];
    bestOption = new int[n];
    for(int i=0; i<n; i++)
        cin>>w[i]>>v[i];
    
    int* filled = new int[n];
    for(int i=0; i<n; i++) filled[i] = -1;
    for(int i=0; i<n; i++) bestOption[i] = -1;
    genBinary(0, filled);
    
    for(int i=0; i<n; i++) if(bestOption[i]) {
        cout<<"I choose you, item "<<i<<"\n";
    }
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

Vâng, tôi bỏ qua hiệu suất chỉ để đoạn code dễ hiểu hơn!

### Tại sao rườm rà?

Như mọi người thấy thì vấn đề chọn những món đồ sao cho được nhiều giá trị nhất mà không vượt quá trọng tải khi nghĩ về nó thì có vẻ nó phải rất là đơn giản phải không?

- Chọn món đồ có giá trị nhất, xong bỏ vô túi, nếu không được thì thôi qua món khác.
- Chọn món đồ có giá trị nhì, xong bỏ vô túi, nếu không được thì thôi qua món khác.
- ...
- Chọn món đồ kém giá trị nhất, bỏ được thì bỏ không được thì thôi.

Không, cách làm này sai bét! Hay thử cách làm khác? Ưu tiên món đồ có giá trị $\displaystyle\frac{v_i}{w_i}$ lớn nhất thì sao? Thật ra cách này cũng sẽ dính trường hợp sai được luôn.

Mình nghĩ hết những cách có thể thì thấy không thấy cách nào ổn cả. Tại sao lại vậy?

Con người là một loài sinh vật thông minh và... tài lanh, ta luôn tự "tối ưu" sớm những việc ta thấy đơn giản để sống thảnh thơi. Cách làm đó có thể sẽ đúng cho đa số các trường hợp nhưng sẽ còn tồn đọng những trường hợp mà cách làm đó không giải quyết được triệt để. Những cách làm này được gọi bằng thuật ngữ "tham lam" (greedy).

Cách duy nhất cho tới hiện tại để giải quyết bài toán cái túi là mình phải thử hết tất cả các trường hợp có thể. Cách làm này được gọi bằng thuật ngữ "vét cạn".

### Sự thật
{: .no_toc}

Thật ra "Bảo toàn tính kiên định của trạng thái" là "back-tracking". 

## Sinh hoán vị

Với những kiến thức đã được truyền tải trước đó, ta hãy cùng phân tích đoạn code sinh hoán vị thân thương!

{% capture code %}{% highlight cpp linenos %}
int n;

bool isFilled(int* filled, int x) {
    for(int i=0; i<n; i++) if(filled[i] == x)
        return 0;
        
    return 1;
}

void genPermutation(int i, int* filled) {
    if(i == n) {
        print(filled);
        return;
    }
    
    for(int x=1; x<=n; x++) {
        if(isFilled(filled, x)) continue;
        
        filled[i] = x;
        genPermutation(i+1, filled);
        filled[i] = -1;
    }
}

int main() {
    cin>>n;
    int* filled = new int[n];
    for(int i=0; i<n; i++) filled[i] = -1;
    genPermutation(0, filled);
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

### Phân tích cấu trúc

Đoạn code để sinh hoán vị bây giờ nhìn rất là friendly phải không nào?

#### Trạng thái
{: .no_toc}

Ở hàm này, trạng thái sẽ là `(i, filled)`.

#### Neo
{: .no_toc}

Neo ở đây là khi mình đã điền hết thành công $n$ vị trí và mình đi tới vị trí không cần điền. Lúc này mình chỉ việc 

#### Chuyển trạng thái
{: .no_toc}

Ở cả 3 sections trước, một trạng thái chỉ phụ thuộc vào 1 hoặc 2 trạng thái khác. Trong hàm đệ quy này, nó sẽ phải phụ thuộc vào $n-i$ trạng thái khác nhưng chung quy cấu trúc đệ quy không hề thay đổi.

#### Tối ưu hóa
{: .no_toc}

Việc với mỗi vị trí phải duyệt lại toàn bộ mảng `filled` để tìm xem giá trị đó đã bị điền hay chưa thật sự rất tốn thời gian, vì thế ta sẽ thêm một mảng đếm để thực hiện nhanh việc kiểm tra!

{% capture code %}{% highlight cpp linenos %}
int n;

void genPermutation(int i, int* filled, bool* isFilled) {
    if(i == n) {
        print(filled);
        return;
    }
    
    for(int x=1; x<=n; x++) {
        if(isFilled[x]) continue;
        
        filled[i] = x;
        genPermutation(i+1, filled, isFilled);
        filled[i] = -1;
    }
}

int main() {
    cin>>n;
    int* filled = new int[n];
    bool* isFilled = new bool[n+1];
    for(int i=0; i<n; i++) filled[i] = -1;
    for(int i=1; i<=n; i++) isFilled[i] = 0;
    genPermutation(0, filled, isFilled);
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

#### Trạng thái bị thay đổi?
{: .no_toc}

Như ta nhận thấy thì bây giờ tham số của hàm đã có thêm một thành viên mới: `isFilled`. Vậy thì trạng thái của hàm sẽ phải tăng lên thành `(i, filled, isFilled)` đúng không?

Thật ra không hẳn là như vậy, ta sẽ dễ nhận thấy rằng giá trị của mảng `isFilled` hoàn toàn có thể nội suy từ mảng `filled`, vì thế ta có thể sử dụng thủ thuật "Giảm chiều trạng thái" để mặc kệ mảng `isFilled` này.

## Kết luận

Đệ quy không khó! Tôi khó!