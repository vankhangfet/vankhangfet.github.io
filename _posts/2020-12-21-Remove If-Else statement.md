---
layout: post
title: How to remove If-Else statement??
tags: [.Net]
---

Trong nhiều trường hợp If-Else không phải là xấu. Tuy nhiên khi đoạn code của bạn có quá nhiều if-else thì bạn nên thay đổi để code trở nên dễ đọc,
dễ dàng bảo trì hơn. Hãy xem xét ví dụ sau: 
~~~~
public int calculate(int a, int b, String operator) {
    int result = Integer.MIN_VALUE;

    if ("add".equals(operator)) {
        result = a + b;
    } else if ("multiply".equals(operator)) {
        result = a * b;
    } else if ("divide".equals(operator)) {
        result = a / b;
    } else if ("subtract".equals(operator)) {
        result = a - b;
    }
    return result;
}
~~~~

Nếu như chúng ta phải thêm nhiều toán tử khác thì if-else sẽ ngày càng nhiều, code trở lên khó đọc hơn. Vậy có cách nào để khắc phục điều này?
Chúng ta sẽ xây dựng một Interface như sau: 

~~~~
public interface Operation {
    int apply(int a, int b);
}
~~~~

Sau đó triển khai các operator từ interface này. Ví dụ với operator "Addition"

~~~~
public class Addition implements Operation {
    public int apply(int a, int b) {
        return a + b;
    }
}
~~~~
