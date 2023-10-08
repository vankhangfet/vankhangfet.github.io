---
layout: post
title: How to manage Terraform state
tags: [Cloud]
---
![Terraform](/img/terraform-state-1.webp "terraform-state-1")
Tiếp theo part1 thì chúng ta cần add thêm tag cho EC2 như sau: 
```
resource "aws_instance" "example" {
  ami           = "xxxxxx"
  instance_type = "t2.micro"
  tags = {
    Name = "terraform-example"
  }
}
```
Sau đó "apply" để thực hiện thay đổi
```
$ terraform apply

aws_instance.example: Refreshing state...
(...)

Terraform will perform the following actions:

  # aws_instance.example will be updated in-place
  ~ resource "aws_instance" "example" {
        ami                          = "ami-0fb653ca2d3203ac1"
        availability_zone            = "us-east-2b"
        instance_state               = "running"
        (...)
      + tags                         = {
          + "Name" = "terraform-example"
        }
        (...)
    }

Plan: 0 to add, 1 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:
```
Vì Terraform có thể lưu lại thông tin thay đổi, do đó bạn sẽ thấy Terraform thực hiện "Refreshing state...". Quay lại vấn đề về State, mỗi khi 
bạn thực hiện câu lệnh "plan" hoặc "apply" thì Terraform sẽ tìm thông tin của resource được tạo ra trước đó và sau đó update lại configuration mới.
Terraform có thể thực hiện được việc này là khi mỗi khi chạy, Terraform sẽ lưu thông tin vào file gọi là "Terraform state file" --> "terraform.tfstate.

Ví dụ khi bạn chạy configure:
```
resource "aws_instance" "example" {
  ami           = "xxxx"
  instance_type = "t2.micro"
}
```
Sau khi chạy "apply" thì thông tin trong "terraform.tfstate" sẽ có thông tin như sau:
![Terraform1](/img/terraform-tfstate-file.webp "terraform-state-2")
```
{
  "version": 4,
  "terraform_version": "1.2.3",
  "serial": 1,
  "lineage": "86545604-7463-4aa5-e9e8-a2a221de98d2",
  "outputs": {},
  "resources": [
    {
      "mode": "managed",
      "type": "aws_instance",
      "name": "example",
      "provider": "provider[\"registry.terraform.io/...\"]",
      "instances": [
        {
          "schema_version": 1,
          "attributes": {
            "ami": "xxxx",
            "availability_zone": "us-east-2b",
            "id": "xxxx",
            "instance_state": "running",
            "instance_type": "t2.micro",
            "(...)": "(truncated)"
          }
        }
      ]
    }
  ]
}
```
