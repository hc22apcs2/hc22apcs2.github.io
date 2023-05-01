---
layout: post
title: CS162 - 8A
parent: Introduction to Computer Science II
--- 

{% include toc.md %}

## Lời mở đầu

Trong tiết học này, chúng ta được học về một bài toán nổi tiếng: "Mã đi tuần". Chúng ta hãy ôn lại cách cài đặt thuật toán này nhé.

## Phát biểu bài toán

Cho một bàn cờ $n\times n$ và một quân mã đặt tại ô $(x, y)$. Tìm một hành trình để quân mã đi hết tất cả các ô trên bàn cờ, mỗi ô được đi đúng một lần và sau đó trở về vị trí xuất phát $(x, y)$.

## Ý tưởng

Từ ô $(x, y)$ ta có thể đi đến (tối đa) $8$ ô khác trên bàn cờ, ta có thể trừu tượng hóa bước đi thứ $i$ bằng việc đi tới ô $(x + row(i) , y + col(i))$ với $row$ và $col$ là 2 mảng được lưu trước, cụ thể:

```cpp 
const int row[8] = {-2, -1, +1, +2, +2, +1, -1, -2};
const int col[8] = {+1, +2, +2, +1, -1, -2, -2, -1};
```

## Implementation

Phần thân chung của chương trình:

{% capture code %}{% highlight cpp linenos %}
#include <iostream>

using namespace std;

const int row[8] = {-2, -1, +1, +2, +2, +1, -1, -2};
const int col[8] = {+1, +2, +2, +1, -1, -2, -2, -1};

void try2Move(int count, int x, int y, int** board, int n);
void printAns(int** board, int n);
bool isInBoard(int x, int y, int n);

int main() {
    int n;
    cout << "What is the size of the board: ";
    cin >> n;
    
    int** board = new int*[n]();
    for(int i=0; i<n; i++)
        board[i] = new int[n]();
    
    int x, y;
    cout << "Where is the starting position of the Knight (x, y): ";
    cin >> x >> y;
    
    board[x][y] = 1;
    try2Move(2, x, y, board, n);
    
    for(int i=0; i<n; i++)
        delete[] board[i];
    delete[] board;
    
    return 0;
}

void printAns(int** board, int n) {
    for(int i=0; i<n; i++) {
        for(int j=0; j<n; j++) {
            cout << board[i][j] << " ";
        }
        cout<<"\n";
    }
}

bool isInBoard(int x, int y, int n) {
    if(x < 0 || x >= n) return false;
    if(y < 0 || y >= n) return false;
    return true;
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

### Đáp án

{% capture code %}{% highlight cpp linenos %}
bool checkAns = false;

bool nextCellIsFirstCell(int x, int y, int** board, int n) {
    for (int i=0; i<8; i++) {
        int xN = x + row[i];
        int yN = y + col[i];
        if(!isInBoard(xN, yN, n)) continue;
        
        if(board[xN][yN] == 1)
            return true;
    }
    return false;
}

void try2Move(int count, int x, int y, int** board, int n) {
    if(checkAns == true) return;
    if(count > n*n) {
        if(!nextCellIsFirstCell(x, y, board, n)) return;
        printAns(board, n);
        checkAns = true;
    }
    
    for (int i=0; i<8; i++) {
        int xN = x + row[i];
        int yN = y + col[i];
        
        //checking:
        // (1) if the next cell is valid
        // (2) check if the next cell is visited
        if(!isInBoard(xN, yN, n)) continue;
        if(board[xN][yN] != 0) continue;
        
        board[xN][yN] = count;
        try2Move(count+1, xN, yN, board, n);
        board[xN][yN] = 0;
    }
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

Full code tại [đây](https://ideone.com/6Ye7uv).

### Thảo luận

Vì ta chỉ cần tìm ra một đường đi duy nhất, ta cần dừng lại ngay sau khi tìm ra một phương án. Vì thế ta có thể cài đặt một số phương pháp tối ưu để tăng cao hiệu quả thuật toán.

Các cách tối ưu này còn được gọi là "Nhánh cận", hay "Branch and Bound".

Một trong những cách tối ưu là "Warnsdorff's rule" (Tên gọi cụ thể của phương pháp thầy gọi là "Fail first"). Về cơ bản, cách làm này sẽ nhìn trước $1$ bước, với mỗi ô bàn cờ "ứng cử viên" của ô hiện tại, ta tính số ứng cử viên tiếp theo của những ô đó và ưu tiên cho quân mã đi về ô có ít ứng cử viên tiếp theo hơn.

Chi tiếp xem thêm tại wiki, link tại [đây](https://en.wikipedia.org/wiki/Knight%27s_tour#Warnsdorff's_rule).

Phần cài đặt của mình có sử dụng một loại dữ liệu là `pair<int, int>`, để hiểu thêm về loại dữ liệu này, vui lòng tham khảo tại [đây](https://cplusplus.com/reference/utility/pair/pair/).

#### Cài đặt
{: .no_toc}

{% capture code %}{% highlight cpp linenos %}
bool checkAns = false;

bool nextCellIsFirstCell(int x, int y, int** board, int n) {
    for (int i=0; i<8; i++) {
        int xN = x + row[i];
        int yN = y + col[i];
        if(!isInBoard(xN, yN, n)) continue;
        
        if(board[xN][yN] == 1)
            return true;
    }
    return false;
}

int numCan(pair<int, int> cur, int** board, int n) {
    int x = cur.first;
    int y = cur.second;
    int num = 0;
    
    for(int i=0; i<8; i++) {
        int xN = x + row[i];
        int yN = y + col[i];
        if(!isInBoard(xN, yN, n)) continue;
        
        if(board[xN][yN] > 0) continue;
        num++;
    }
    
    return num;
}

void try2Move(int count, int x, int y, int** board, int n) {
    if(checkAns == true) return;
    if(count > n*n) {
        if(!nextCellIsFirstCell(x, y, board, n)) return;
        printAns(board, n);
        checkAns = true;
    }
    
    pair<int, int> candidates[8];
    int nCandidate = 0;
    
    for (int i=0; i<8; i++) {
        int xN = x + row[i];
        int yN = y + col[i];
        if(!isInBoard(xN, yN, n)) continue;
        
        //If the number of candidates of first knight's
        //position is 0, it means there're no way back 
        //to the first position
        if(board[xN][yN] == 1) {
            if(numCan({xN, yN}, board, n) == 0) return;
        }
        
        if(board[xN][yN] == 0) {
            candidates[nCandidate++] = {xN, yN};
        }
    }
    
    // Sort candidates by the number of next_candidates
    // using bubble sort
    for(int i=0; i < nCandidate - 1; i++) {
        for (int j = 0; j < nCandidate - i - 1; j++) {
            int num_a = numCan(candidates[j], board, n);
            int num_b = numCan(candidates[j+1], board, n);
            if(num_a > num_b)
                swap(candidates[j], candidates[j+1]);
        }
    }
    
    for(int i=0; i < nCandidate; i++) {
        int xN = candidates[i].first;
        int yN = candidates[i].second;
        if(!isInBoard(xN, yN, n)) continue;
        
        if(board[xN][yN] == 0) {
            board[xN][yN] = count;
            try2Move(count+1, xN, yN, board, n);
            board[xN][yN] = 0;
        }
    }
}
{% endhighlight %}{% endcapture %}{% include fix_linenos.html code=code %}

Full code tại [đây](https://ideone.com/aI0UDf).

### So sánh

Với cải tiến "Warnsdorff's rule", code của chúng ta chạy nhanh hơn rất nhiều, cụ thể khi chạy trên ideone thì code ngây thơ chạy được test tối đa $n=6$ trong khi code cải tiến chạy được đến $n=12$, nghĩa là số ô nhiều gấp $4$ lần.

## Bài tập mở rộng

Lấy ý tưởng từ trò chơi Minesweeper, cho trước một bảng trạng thái $n$ hàng $m$ cột chứa các số nguyên không âm không quá $9$. Số nguyên tại ô $(i, j)$ cho biết tổng số bom **chính xác** của các ô $(u, v)$ thỏa mãn:

$$\max(\vert u-i \vert, \vert v - j \vert) \le 1$$

Hãy tìm một cấu hình đặt những quả bom sao cho thỏa mãn bảng trạng thái cho trước hoặc cho biết không có các đặt nào thỏa mãn.