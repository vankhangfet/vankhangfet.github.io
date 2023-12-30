---
layout: post
title: Setup sonarqube on mac
tags: [Others]
---

Sonarqube là một công cụ rất mạnh mẽ trong việc scan code. Công cụ này có thể giúp bạn scan những vấn đề trong về source code như:

- Detect Bugs & basic Vulnerabilities
- Review Security Hotspots
- Track Code Smells & fix your Technical Debt
- Code Quality Metrics & History
- CI/CD integration

Ví dụ dưới đây là kết quả khi bạn scan project với sonarqube
![sonarqube](https://www.c-sharpcorner.com/article/step-by-step-sonarqube-setup-and-run-sonarqube-scanner/Images/Step%20By%20Step%20SonarQube%20Setup%20And%20Run%20SonarQube%20Scanner7.jpg)

Đây là một công cụ nên sử dụng khi bạn làm việc với dự án, nó sẽ giúp cho code của bạn tốt hơn, giảm bớt sự phụ thuộc hay tiết kiệm thời gian review code.
Trong lúc rảnh rỗi tôi có setup để dùng cho dự án của tôi, dự án là một ứng dụng ios, việc setup có rất nhiều bài hướng dẫn. Lần này tôi setup theo bài hướng dẫn sau
https://dev.to/onmyway133/how-to-use-sonarqube-in-swift-projects-5db5

Tuy nhiên để setup chạy ngay lần đầu tiên cũng 
không hề dễ dàng cho lắm, nên tôi note lại để có thể ghi nhớ cho lần sau. 

Việc setup có vẻ đơn giản, chỉ cần download Sonarqube từ: https://www.sonarsource.com/products/sonarqube/downloads/
Sau đó giải nén và chạy command sau:
```` 
~/sonarqube/bin/macosx-universal-64/sonar.sh console
````
Tuy nhiên một đống lỗi sẽ xuất hiện, mất một lúc tìm hiểu thì tôi mới có thể chạy được Sonarqube. Nếu như để dễ dàng hơn bạn có thể dùng docker, cách này sẽ dễ hơn.

Lỗi không chạy được liên quan tới java version. Trong lúc loay hoay setup java thì tôi vô tình tìm được tool sau: https://sdkman.io/install.
sdkman sẽ giúp bạn download java version và thiết lập phiên bản java tương ứng một cách rất dễ dàng.

Ngoài ra bạn cũng có thể tham khảo link sau, nếu như gặp khó khăn khi cài java trên mac và muốn thay đổi các version của java tùy vào dự án. https://stackoverflow.com/questions/52524112/how-do-i-install-java-on-mac-osx-allowing-version-switching
