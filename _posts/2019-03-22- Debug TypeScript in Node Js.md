---
layout: post
title: Debug TypeScript trong Node JS với VS Code.
tags: [JS]
---

Post này mình note lại cách để debug TypeScript trong Node JS bằng cách sử dụng VS Code. 
Khi làm việc với TypeScript và Node JS thì VS code là một trong những lựa chọn theo mình là tốt để bắt đầu code. Đối với Dev thì việc debug
là một hoạt động rất quen thuộc, mình cũng mất chút thời gian để setup cho việc debug. Bài này vừa để note lại cũng như giúp các bạn debug 
nhanh hơn.

Trước khi setup debug, ta hãy xem qua cách thức khởi tạo project. Bạn phải cài package npm trước. Sau đó là install TypeSciprt sử dụng 
command dưới đây:
~~~~
npm init --yes
npm install typescript --save-dev
~~~~

Khi project được khởi tạo, ta chuẩn bị source như sau:

Tạo file app.ts
~~~~
import { hello } from './hello';

class App {
    /** Entry point of our app */
    public static start() {
        console.log(hello('world'));
    }
}

App.start();
~~~~

Tiếp đến tạo file hello.ts

~~~~
/** Say hello */
export const hello = (name: string) => {
    const greeting = `Hello ${name}!`;
    return greeting;
};
~~~~

OK, để build project ts, chúng cần tsconfig file (tsconfig.json). Nội dung file như sau:

~~~~
{
    "compilerOptions": {
        "outDir": "./out",
        "rootDir": "./src",
        "sourceMap": true,
        "moduleResolution": "node",
        "target": "es5"
    }
}
~~~~

Sau khi setup, chúng ta add thêm file "package.json" như sau:

~~~~
{
  "name": "vscode-typescript-debugging",
  "version": "1.0.0",
  "devDependencies": {
    "typescript": "^2.7.2"
  },
  "scripts": {
    "start": "node out/app.js",
    "prestart": "npm run build",
    "build": "tsc"
  }
}
~~~~

Để run app chúng ta dùng lệnh 

~~~~
npm start
~~~~

Ngoài start command, chúng ta có một số lệnh sau:

start — run the compiled app with node
prestart — is called automatically before the start script
build — runs the TypeScript compiler

OK, như vậy là chúng ta có thể run app. Để Debuging được thì, ta cần tạo file sau trong thư mục ".vscode"
~~~~
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Build Project",
            "program": "${workspaceFolder}\\src\\app.ts",
            "preLaunchTask": "npm: build",
            "sourceMaps": true,
            "smartStep": true,
            "internalConsoleOptions": "openOnSessionStart",
            "outFiles": [
                "${workspaceFolder}/out/**/*.js"
            ]
        }
    ]
}
~~~~

Ở đây có một số config bạn cần chú ý. Khi debug thì VSCode sẽ map step từ Js về Ts code do đó "sourceMaps" phải set là true.
khi chương trình chạy thì chúng ta cần chỉ ra entry file, ở đây chính là file app.ts. Sau khi đã config và create đầy đủ các file, chúng ta debug chương trinh thôi. Kết quả sẽ như dưới đây:

![debug_vscode](https://cdn-images-1.medium.com/max/1200/1*EdWPc8vRp0MC-E5nWDYOWw.png "Debug_vscode")



Link tham khảo: https://medium.com/@PhilippKief/how-to-debug-typescript-with-vs-code-9cec93b4ae56
