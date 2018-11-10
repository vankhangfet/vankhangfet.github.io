---
layout: post
title: Reverse string trong C# bằng đệ quy
tags: [.Net]
---

Reverse string là một question khá hay trong khi interview. Có khá nhiều cách để reverse string, trong đó có một cách sử dụng kỹ thuật đệ quy rất hay. Bài toán chúng ta cần làm như sau:

![csharp-recursion-image-exercise-14.png](/img/csharp-recursion-image-exercise-14.png "csharp-recursion-image-exercise-14")

OK! Hãy xem function đệ quy để giải quyết bài toán này như thế nào?

~~~~
using System;
class RecExercise14
    {
        static void Main()
        {
            string str; 
			Console.WriteLine("\n\n Recursion : Get the reverse of a string :");
			Console.WriteLine("----------------------------------------------"); 
			Console.Write(" Input the string : ");
            str = Console.ReadLine();
            str = StringReverse(str);
            Console.Write(" The reverse of the string is : ");
            Console.Write(str);
            Console.ReadKey();
             Console.Write("\n"); 
            
        }

        public static string StringReverse(string str)
        {
            if (str.Length > 0)
                return str[str.Length - 1] + StringReverse(str.Substring(0, str.Length - 1));
            else
                return str;
        }
    }
~~~~

Khá là thú vị, hy vọng ví dụ này các bạn sẽ thấy đệ quy được sử dụng thế nào và học thêm một cách để reverse string.

