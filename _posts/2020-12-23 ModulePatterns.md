---
layout: post
title:  Module Patterns trong JavaScript
tags: [JS]
---

Module Pattern là một trong những Pattern quan trọng khi sử dụng Java Script. Đây là một Pattern phổ biến được dùng để đóng gói các method và variables trong vào trong 
một scope. Điều này cũng cho phép chúng ta chỉ expose ra những propertiy, method cần thiết. Việc triển khai Pattern này khá đơn giản trong Javascript. 

Chúng ta hãy xem xét ví dụ sau với module chỉ có 1 hàm public 
~~~~~
function EmployeeDetails() {
  var name: "Mayank";
  var age = 30;
  var designation = "Developer"
  
  return {
    name: name,
    age: age,
    designation: designation
  }
}

var newEmployee = EmployeeDetails()

var userName = newEmployee.name;
var userAge = newEmployee.age;
var userDesignation = newEmployee.designation;
~~~~~

Nếu như không muốn expose thuộc tính nào đó, chúng ta chỉ việc remove nó ra khỏi kết quả trả về của return. Trong trường hợp chúng ta muốn tương tác với data bên trong thì như
các bạn đã biết, chúng ta sẽ cần implement những public method như sau: 

~~~~
function EmployeeDetails() {
  var name: "Mayank";
  var age = 30;
  var designation = "Developer",
  var salary = 10000;

  var calculateBonus = function(amount) {
    salary = salary + amount;
  }

  return {
    name: name,
    age: age,
    designation: designation,
    calculateBonus: calculateBonus
  }
}

var newEmployee = EmployeeDetails()

var userName = newEmployee.calculateBonus(1000
~~~~


Qua đó ta thấy rằng module Pattern sẽ giúp cho việc đóng gói dữ liệu tốt hơn, nó mang lại những ích lợi sau: 

- Maintainability: Module Patterns enable better maintainability since all the related code can be encapsulated inside a single logical block. These logically independent blocks are relatively easier to update.

- Reusability: We single unit of code can be reused across the entire application. Functionality enclosed as a module can be reused and we do not need to define the same functions at multiple points.
