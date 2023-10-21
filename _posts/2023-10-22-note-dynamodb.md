---
layout: post
title: Dynamo DB một số điều cần lưu ý
tags: [Design]
---

Dynamo DB là một NoSQL rất hay được sử dụng trên AWS. Bạn có thể sử dụng Dynamo trong hầu hết các ứng dụng. Nó rất đơn giản, và cho phép lưu trữ cũng như truy vấn 
với dữ liệu lớn rất tuyệt vời. Tuy nhiên khi thiết kế với Dynamo DB cũng không hề dễ dàng. Việc thiết kế cơ sở dữ liệu với Dynamo không dễ dàng như bạn nghĩ.
Hãy thử xem qua một số vấn đề khi làm việc với Dynamo, bạn đã bao giờ gặp vấn đề với Throttling? 

What is DynamoDB Throttling?
Như các bạn đã biết thì khi lưu trữ dữ liệu thì Dynamo gồm rất nhiều các "partition". Các bản ghi sẽ được lưu trữ trong các partion này.
Việc lưu dữ vào partion sẽ được lưu trữ dựa trên partition key. 
Tham khảo: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.Partitions.html

Ngoài ra thì mỗi partition có giới hạn tối đa read/write (RCUs/WCUs) là 3000 RCUs và 1000 WCUs. 
Nhưng cần lưu ý là giớ hạn này được chia đều cho các partions. Để cho dễ hiểu ta hãy xem ví dụ sau:
Giả sử chúng ta configure RCUs và WCUs là 50 cho table và tabel này có 2 partition thì mỗi partition sẽ có giới RCUs/WCUs là 25.

Do đó mỗi khi bạn thực hiện read/write data vào table thì request sẽ được thực hiện trên các partition và khi số lượng read/write vượt quá giới hạn thì exception
Throttling sẽ xảy ra. Mặc dù chúng ta thấy rằng Dynamo DB là fully-mananged service, nhưng khi thiết kế vấn đề Throttling nên cần được quan tâm. 

Chúng ta đã biết mỗi khi tạo một table, AWS sẽ cung cấp cho chúng ta 2 lựa chọn 
1. Provisioned model
2. On-demand model

Với option 1, có thể dễ thấy là Throttling có thể xảy ra nếu như chúng ta tính toán sai về RCUs/WCUs. Vậy còn option 2? Vì là On-demand nên không xảy ra Throttling?
Tuy nhiên option 2 vẫn không hoàn toàn tránh được Throttling, nó vẫn xảy ra dưới điều kiện sau: 

1. Not enough capacity - When most of the partitions exceed the 3000 RCU and 1000 WCU.
2. When traffic doubles the previous peak - If your DynamoDB traffic increases more than double the previous peak within 30 minutes, you might experience throttling.

Vậy làm sao có thể giảm thiểu throttling? Chúng ta hãy xem xét những yếu tố sau: 

*Hot partitions*

Vậy Hot partition là gì?
Như đã đề cập trước đó thì giới hạn RCUs/WCUs được chia đều cho các partition. Nên nếu như thiết kế không tốt dẫn đến khả năng 1 partition nào đó bị truy cập quá nhiều sẽ dẫn đến việc mất cân bằng, và vượt quá giới hạn. Để dễ hình dung ta hãy xem ví dụ sau: 
Giả sử chúng ta thiết kế table Product để lưu trữ các sản phẩm, và sử dụng "Product_Id" làm partition key. Khi đó nếu như product_Id này có số lượng tìm kiếm. hoặc update 
lớn thì rất dễ gây ra hiện tượng Throttling. Vậy làm sao để hạn chế việc này, cách tốt hơn là chúng ta nên sử dụng "Category" làm partition key và sort key là "Product_Id".
Khi đó mỗi khi chúng ta thực hiện tìm kiếm/ update "Product_Id" thì request sẽ được chia đều vào các partition "Category".
Ngoài ra để monitor các partitions các bạn có thể dùng tool sau: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/contributorinsights_HowItWorks.html

*Sudden increases in traffic*
