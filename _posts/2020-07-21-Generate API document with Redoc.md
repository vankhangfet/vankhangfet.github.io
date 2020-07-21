---
layout: post
title: Generate API document with Redoc
tags: [Others]
---

Để mô tả API chúng ta có thể dùng những tool rất hay như sau:
1. Open API 
   Open API rất trực quan để mô tả API, các bạn có thể xem ví dụ mẫu ở link sau: [ https://github.com/OAI/OpenAPI-Specification/blob/master/examples/v3.0/link-example.yaml]( https://github.com/OAI/OpenAPI-Specification/blob/master/examples/v3.0/link-example.yaml)

2. VS code + Redoc
  Nếu bạn nào chưa biết Redoc là gì thì xem link sau: [https://github.com/Redocly/redoc](https://github.com/Redocly/redoc)
   

3. Một số note khi viết API spec. Chúng ta có một số thẻ như sau. Ví dụ dưới đây là một ví dụ API method Post có header / cookie và request body 
~~~~
 parameters:
   - name: Accept 
     in: header  (cookie/path)
     required: true
     description: application/json
     schema: 
      type: string
 ~~~~  
 
 ~~~~
 requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object 
              required:
                - f_token
                - os_type
              properties:
                f_token:
                  type: string
                os_type:
                  type: string

 ~~~~

4. Genrate tài liệu với Redoc cli 
   Chúng ta sẽ cần cài đặt redoc cli, cách cài đặt rất đơn giản với command sau: 
   ~~~~
   npm install redoc-cli
   ~~~~
   Sau khi cài đặt thành công thì việc còn lại sẽ là viết spec mô tả dưới format JSON hoặc yml.
   Để Generate doc thì chúng ta dùng câu lệnh sau: 
   ~~~~
   npx redoc-cli bundle .\my_OpenAPI.yml --output index.html
   ~~~~
   
