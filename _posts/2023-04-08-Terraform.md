---
layout: post
title: How to work with Terraform
tags: [Cloud]
---

Terraform là một trong những công cụ rất mạnh mẽ để bạn tự động hóa việc khởi tạo, quản lý resource trên cloud. Nếu như bạn đã làm quen với AWS và 
Cloudformation thì Terraform là một công cụ không thể bỏ qua.

### Tại sao nên sử dụng Terraform? 

Như các bạn đã biết thì việc sử dụng đa nền tảng đám mây ngày càng phổ biến. Một hệ thống có thể được triển khai trên nhiều cloud provider khác nhau
(AWS, Azure,etc.), do đó chúng ta cần một công cụ có thể triển khai dễ dàng trên các nền tảng khác nhau này.
Với Terraform thì việc triển khai IaC (Infrastructure as Code) sẽ dễ dàng hơn rất nhiều.

### Bắt đầu với Terraform như thế nào?
Cách tốt nhất để làm quen với Terraform là viết một script khởi tạo một tài nguyên trên cloud. Chúng ta có thể bắt đầu với việc tạo một EC2 trên AWS.

Điều kiện cần thiết là bạn phải có một AWS Account, và cần cài đặt Terraform. 

Chúng ta sẽ viết một script để tạo một máy ảo EC2 trên AWS như sau
1. Khai báo main script main.tf  như sau: 
```
provider "aws" {
  region = "us-east-2"
}
```
Vì chúng ta đang làm việc với AWS nên provider và region sẽ có các giá trị như trên. 

Tiếp đến là khai báo resource cần khởi tạo trên AWS, cụ thể ở đây là EC2 

```
resource "aws_instance" "example" {
  ami           =  "ami-0fb653ca2d3203ac1" 
  instance_type = "t2.micro"
}
```

Sau đó cần chạy command sau:

```
$ terraform init
Initializing the backend...
Initializing provider plugins...
    - Reusing previous version of hashicorp/aws from the lock file
    - Using hashicorp/aws v4.19.0 from the shared cache directory
Terraform has been successfully initialized!
```
Khi bạn khởi chạy câu lệnh "init", Terraform sẽ download code và thông tin provider vào file ".terraform.lock.hcl".

Tiếp theo chúng ta chạy câu lệnh "plan" như sau:
```
$ terraform plan

(...)

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-0fb653ca2d3203ac1"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      (...)
  }

Plan: 1 to add, 0 to change, 0 to destroy.
```
Lệnh "plan" sẽ cho bạn biết những thay đổi thực sẽ được triển khai khi khởi tạo resource. Nếu như không có vấn đề gì, chúng ta 
cần chạy lệnh "apply" để thực hiện việc triển khai.

```
$ terraform apply

(...)

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-0fb653ca2d3203ac1"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      (...)
  }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:
```

Nếu câu lệnh "apply" được thực thi thành công, chúng ta sẽ thấy một EC2 được tạo trên region AWS. 

Mọi thứ khá là đơn giản? Nhưng nếu chúng ta muốn thay đổi resource thì Terraform sẽ quản lý state của resource như thế nào?

