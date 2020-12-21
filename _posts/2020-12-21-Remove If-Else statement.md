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
Tiếp đó chúng ta cần một Factory class như 
~~~~
public class OperatorFactory {
    static Dictionary<String, Operation> operationMap = new Dictionary<>();
    static {
        operationMap.put("add", new Addition());
        operationMap.put("divide", new Division());
        // more operators
    }

    public static Optional<Operation> getOperation(String operator) {
        return Optional.ofNullable(operationMap.get(operator));
    }
}
~~~~

Ví dụ muốn thực hiện toán tử "Addition", chúng ta có thể viết lại đoạn như dưới đây:
~~~~
public int calculateUsingFactory(int a, int b, String operator) {
    Operation targetOperation = OperatorFactory
      .getOperation(operator)
    return targetOperation.apply(a, b);
}
~~~~
Bây giờ code đã trở nên rất rõ ràng. Ngoài cách trên chúng ta có thể sử dụng "Command Pattern". Cách triển khai "Command Pattern" như sau: 

Trước tiên, chúng ta cần một interface "Command" 
~~~~
public interface Command {
    Integer execute();
}
~~~~

Sau đó là implement các operator 
~~~~
public class AddCommand implements Command {
    // Instance variables

    public AddCommand(int a, int b) {
        this.a = a;
        this.b = b;
    }

    public Integer execute() {
        return a + b;
    }
}
~~~~
Tiếp đó là class để thực hiện command này 
~~~~
public int calculate(Command command) {
    return command.execute();
}
~~~~

Ví dụ với việc thực hiện "Add command", ta dễ dàng thực hiện như sau: 
~~~~
public void whenCalculateUsingCommand_thenReturnCorrectResult() {
    Calculator calculator = new Calculator();
    int result = calculator.calculate(new AddCommand(3, 7));
    assertEquals(10, result);
}
~~~~

Great!!!!! Hy vọng là những cách trên có thể giúp bạn viết code đẹp hơn, dễ bảo trì hơn.
