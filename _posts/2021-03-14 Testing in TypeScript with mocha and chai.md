---
layout: post
title: Viết Unit test khi làm việc với TypeScript với Mocha & Chai.
tags: [JS]
---

Khi làm việc với những dự án phần mềm, thì dù là chương trình phức tạp hay đơn giản chúng ta cũng nên thực hiện viết UnitTest.
Việc viết UT có rất nhiều lợi ích, một trong lợi ích lớn nhất mà UT mang lại đó là chúng ta có cơ hội được review lại code của mình một lần nữa.
Nếu như chúng ta cảm thấy khó khăn trong khi viết UT, điều đó có nghĩa chúng ta có thể viết code chưa đủ rõ ràng. Ngoài ra thì UT mang lại nhiều lợi hơn nữa. Post này mình tập trung vào việc cài đặt UT
trong dự án dùng TypeScript. Mình thấy việc sử dụng Mocha  và Chai là giải pháp tốt để viết UT. Các bước cài đặt cũng khá đơn giản.
Các bước cài đặt như sau: 

Step 1: Chúng ta cần cài đặt thư viện sau: 
~~~~
npm install chai mocha ts-node @types/chai @types/mocha --save-dev
~~~~

Step 2: Sửa lại configure trong file Package.json như sau:
~~~~
"scripts": { "test": "mocha -r ts-node/register tests/**/*.test.ts" }
~~~~

Step 3: Sau khi setup xong, ta tiến hành viết UT. Mình giả sử chúng ta có đoạn code sau:
~~~~
export const helloTest(){ return "hello"; }
~~~~

Chúng ta sẽ có code đoạn code UT như sau: 
~~~~
import { helloTest } from '../src/hello-test';
import { expect } from 'chai';
import 'mocha';

describe('First test', 
  () => { 
    it('should return true', () => { 
      const result = helloTest();
      expect(result).to.equal("hello"); 
  }); 
});
~~~~

Khi muốn chạy test thì chúng ta chỉ cần chạy câu lệnh đơn giản sau:
~~~~
npm run test
~~~~
Nếu như các test case đều OK, chúng ta sẽ thấy một repost trên console như sau:


