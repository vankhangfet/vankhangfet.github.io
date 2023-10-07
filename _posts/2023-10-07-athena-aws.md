---
layout: post
title: Athena & Glue một service thú vị, nhưng cũng khá là khó hiểu?
tags: [Design]
---

Khi làm việc với Athena thì tôi thấy đây là một công cụ rất mạnh trong việc truy vấn dữ liệu, phân tích dữ liệu. 
Athena có thể truy vấn dữ liệu trên s3, dynamo db,etc. Hỗ trợ truy vấn phức tạp với SQL. Tuy nhiên mọi chuyện không hoàn toàn dễ dàng, 
và việc thiết kế với Athena làm tôi cảm thấy có chút khó hiểu? 

Vấn đề xảy ra khi tôi thực hiện truy vấn một bảng dữ liệu trong dynamo. Để thực hiện việc truy vấn này, các bạn sẽ cần triển khai theo infra như sau:
Refer: https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/access-query-and-join-amazon-dynamodb-tables-using-athena.html
![athena-lambda](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/patterns/images/pattern-img/e6ff94af-d208-40c7-94e4-af257755a603/images/bc8e0132-b578-463b-bf55-3c39ce359c17.png "aws athena")



