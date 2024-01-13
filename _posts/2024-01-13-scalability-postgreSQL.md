---
layout: post
title: PostgreSQL Scalability - How Cloudflare Was Able to Support 55 Million Requests per Second With Only 15 Postgres Clusters
tags: [Design]
---
Trong lúc thiết kế hệ thống tôi đang cùng đội phát triển thảo luận về việc dùng DynamoDB hay PostgreSQL thì tôi có nhận được email từ 1 website mà tôi đã subcribe trước đó.
Nội dùng bài viết đó là: "Làm thế nào mà Cloudflare có thể hỗ trợ được 55 triệu request/second với chỉ 15 Postgres Cluster". Tôi thấy tiêu đề rất ấn tượng và quyết định đọc 
bài viết đó. Refer: https://newsletter.systemdesign.one/p/postgresql-scalability

Theo như số liệu bài viết thì Cloudflare đang phục vụ đến 20% lượng traffict trên internet tương đương với 55 triệu request/ second, đó là một con số rất ấn tượng.
Cloudflare được thiết kế với kiến trúc multi tenant, mỗi tenant sẽ có workload khác nhau, do đó việc xây dựng clust sẽ là một thách thức.
