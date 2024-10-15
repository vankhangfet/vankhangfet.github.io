---
layout: post
title: Measuring DORA DevOps Metrics.
tags: [DevOps]
---

Trong quá trình phát triển sản phẩm thì việc hiểu rõ và tối ưu quy trình phát triển là một vấn đề quan trọng.
Có rất nhiều metric để đo lường, và gần đây thì đội nhóm phát triển của chúng tôi đã tìm hiểu và đo lường metric [DORA](https://cloud.google.com/blog/products/devops-sre/announcing-dora-2021-accelerate-state-of-devops-report)

DORA là gì? 
Được hỗ trợ bởi hơn 10 năm nghiên cứu từ chương trình Nghiên cứu và Đánh giá DevOps (DORA) của Google Cloud, 
các chỉ số DORA là bốn chỉ số chính được sử dụng để chỉ ra tốc độ và sự ổn định của phát triển phần mềm. Những phép đo này bao gồm:

| Metrics    | What is this? |
| -------- | ------- |
| 1. Deployment frequency  | How often an organization successfully releases to production    |
| 2. Lead time for changes  | The amount of time it takes for a commit to get into production   |
| 3. Change failure rate | The percentage of deployments causing a failure in production   |
| 4. Time to restore service | The amount of time it takes for an organization to recover from a failure in production   |

Chỉ có 4 chỉ số, nhưng việc đo lường 4 chỉ số này là một bài toán và thách thức cho các đội phát triển. Trước khi đi chi tiết vào đo lường, chúng
ta hãy xem các chỉ số này sẽ giúp cho đội phát triển như thế nào? Nó có ý nghĩa gì?

Trong DORA thì việc xác định năng suất được chia làm 4 level: low performers, medium performers, high performers, and elite performers.
| ---- | Deployment frequency     | Lead time for changes  | Change failure rate | Time to restore service |
|------| -------- | ------- | ------| ------ |
|Low performers|
|Medium performers|
|High performers|
|Elite performers|













