---
layout: post
title: Độ phức tạp thuật toán.
tags: [Algorithm]
---

Độ phức tạp thuật toán là một phần rất thú vị, nhưng hầu hết anh em dev sau một thời gian sẽ không còn nhớ hoặc quan tâm đến nó nữa. Lý do là vì công việc, khi không dùng đến nữa thì sẽ quên mất. Post này mình cũng ôn lại một số kiến thức cơ bản, chỉ note lại những điểm cần nhớ thôi. 

## 1. Tính độ phức tạp thuật toán như thế nào?
Có một số quy tắc cơ bản cần nhớ như sau:

 1.1 Quy tắc bỏ hằng số: 
 Nếu chương trình P có thời gian thực hiện T(n) = O(c1.f(n)), thì có thể coi chương trình có độ phức tạp O(f(n)).
 
 1.2 Quy tắc cộng lấy max
 Nếu T1(n) và T2(n) là thời gian chạy của 2 chương trình P1 và P2. T1(n) = O(f(n)) và T2 = O(g(n)), thì độ phực tạp của 2 chương trình khi  gọi nối tiếp nhau sẽ là O(max(f(n),f(n))
 
 Ví dụ cho các bạn dễ hiểu, nếu như chương trình có phép gán x:=1 có độ phức tạp O(1) và sau đó là readln(x) có độ phức tạp là O(1).
 Khi đó độ phức tạp của cả chương trình sẽ là O(max(1,1))
 
 1.3 Quy tắc nhân 
  Nếu T1(n) và T2(n) là thời gian chạy của 2 chương trình P1 và P2. T1(n) = O(f(n)) và T2 = G(f(n)), thì độ phực tạp của 2 chương trình khi lồng  nhau sẽ là O(f(n) * g(n))
 
Ngoài ra thì chúng ta có một số quy tắc tổng quát như sau:

- Thời gian thực hiện của mỗi lệnh gán, READ, WRITE là O(1).

- Thời gian thực hiện của một chuỗi tuần tự các lệnh được xác định bằng qui tắc cộng. Như vậy thời gian này là thời gian thi hành một lệnh nào đó lâu nhất trong chuỗi lệnh.

- Thời gian thực hiện cấu trúc IF là thời gian lớn nhất thực hiện lệnh sau THEN hoặc sau ELSE và thời gian kiểm tra điều kiện. Thường thời gian kiểm tra điều kiện là O(1).

- Thời gian thực hiện vòng lặp là tổng (trên tất cả các lần lặp) thời gian thực hiện thân vòng lặp. Nếu thời gian thực hiện thân vòng lặp không đổi thì thời gian thực hiện vòng lặp là tích của số lần lặp với thời gian thực hiện thân vòng lặp.

Bây giờ chúng ta xem độ phức tạp của thuật toán sắp xếp nổi bọt 
~~~~
procedure Bubble (var a: array[1..n] of integer);
var i,j,temp: integer;
begin
    for i:=1 to n-1 do                  {1}
        for j:=n downto i+1 do              {2}
            if a[j-1]>a[j] then          {3}
            begin
                temp:=a[j-1];           {4}
                a[j-1]:=a[j];           {5}
                a[j]:=temp;             {6}
            end;
end;
~~~~

Để tính độ phức tạp thuật toán trên, ta sẽ tính theo thứ tự từ trong ra ngoài. Dễ thấy rằng các phép gán tốn O(1), và phép so sánh tốn 
O(1), nên đoạn lệnh {3} -> {6}, sẽ lấy theo công thức cộng (max) tốn O(1). Tuy nhiên các phép tính này được thực hiện n-i lần trong vòng 
for {2}, nên trong vòng for {2} sẽ có độ phức tạp là O((n-i)* 1) = O(n-i). Áp dụng tiếp quy tắc lấy max thì vòng for {2} sẽ có độ phức tạp O(n-1). Cuối cùng ta xét đến vòng lặp for {1} được thực hiện n lần, như vậy độ phức tạp thuật toán này sẽ là O(n.(n-1)) = O(n^2). 

Note: với vòng lặp không biết trước số lần lặp thì độ phức tạp phải tính trên trường hợp xấu nhất. Chúng ta xem xét ví dụ tìm kiếm sau:

~~~~
FUNCTION Search(a:ARRAY[1..n] OF Integer;x:Integer):Boolean;
VAR i:Integer;
    Found:Boolean;
BEGIN
    i:=1;                                           {1}
    Found:=FALSE;                                   {2}
    WHILE(i<=n) AND (not Found) DO                   {3}
        IF A[i]=X THEN Found:=TRUE ELSE i:=i+1;     {4}
    Search:=Found;                                  {5}
END;
~~~~

Dễ thấy {1},{2} và {5} sẽ có độ phức tạp O(1), nên độ phức tạp của chương trình sẽ là độ phức tạp của lệnh lồng {3}. Trong trường hợp này vòng lặp sẽ chạy n lần trong trường hợp xấu nhất, nên độ phức tạp của {3} sẽ là O(n). 

Chương trình search ở trên sẽ có độ phức tạp O(n).




