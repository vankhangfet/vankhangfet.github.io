---
layout: post
title: Sử dụng curl để check http status trong bash script
tags: [Others]
---

Chúng ta có thể dùng đoạn script như sau: 
~~~~
#!/bin/bash

while true
do
  STATUS=$(curl -s -o /dev/null -w '%{http_code}' http://www.google.com)
  if [ $STATUS -eq 200 ]; then
    echo "Got 200! All done!"
    break
  else
    echo "Got $STATUS :( Not done yet..."
  fi
  sleep 10
done
~~~~
