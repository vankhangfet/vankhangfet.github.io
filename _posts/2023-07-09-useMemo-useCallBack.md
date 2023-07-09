---
layout: post
title: Understading useMemo and useCallBack
tags: [React]
---
Trong quá trình làm việc với các bạn dev React, tôi nhận thấy rằng trong React có rất nhiều bạn developer gặp vấn đề khi sử dụng useMemo và useCallBack. Post này tôi hy vọng có thể giúp bạn hiểu rõ hơn về useMemo và useCallBack.

Trước khi đi vào chi tiết, chúng ta nên chuẩn bị môi trường làm việc để có thể thực hành và chạy example code. Việc này sẽ giúp các bạn hiểu hơn. Nếu bạn nào chưa có tài khoản trên codesanbox thì hãy đăng ký tại https://codesandbox.io

**Hãy bắt đầu với useMemo**

Ý tưởng của useMemo đó là lưu lại giá trị, trạng thái của ứng dụng trong mỗi lần render. Mặc dù React đã tối ưu việc re-render UI, nhưng React cung cấp thêm useMemo giúp các bạn tối ưu hơn nữa việc render:
 1. Giảm workload (số lượng task cần thiết cho việc render) khi cần thực hiện việc render.
 2. Giảm thời gian khi cần render lại component.

 Không có gì dễ hiểu hơn là show code: 
 
 **Use Case 1: Heavy computations**

Giả sử chúng ta sẽ xây dựng một ứng dụng hiển thị tất cả các số nguyên tố nhỏ hơn một giá trị được nhập từ UI.

```js
import React from 'react';

function App() {
  // We hold the user's selected number in state.
  const [selectedNum, setSelectedNum] = React.useState(100);
  
  // We calculate all of the prime numbers between 0 and the
  // user's chosen number, `selectedNum`:
  const allPrimes = [];
  for (let counter = 2; counter < selectedNum; counter++) {
    if (isPrime(counter)) {
      allPrimes.push(counter);
    }
  }
  
  return (
    <>
      <form>
        <label htmlFor="num">Your number:</label>
        <input
          type="number"
          value={selectedNum}
          onChange={(event) => {
            // To prevent computers from exploding,
            // we'll max out at 100k
            let num = Math.min(100_000, Number(event.target.value));
            
            setSelectedNum(num);
          }}
        />
      </form>
      <p>
        There are {allPrimes.length} prime(s) between 1 and {selectedNum}:
        {' '}
        <span className="prime-list">
          {allPrimes.join(', ')}
        </span>
      </p>
    </>
  );
}

// Helper function that calculates whether a given
// number is prime or not.
function isPrime(n){
  const max = Math.ceil(Math.sqrt(n));
  
  if (n === 2) {
    return true;
  }
  
  for (let counter = 2; counter <= max; counter++) {
    if (n % counter === 0) {
      return false;
    }
  }

  return true;
}

export default App;
```
Sẽ không có vấn đề gì với đoạn code ở trên, nhưng nếu component này được render lại nhiều lần thì sao? 
Giả sử chúng ta sẽ cần hiển thời gian hệ thống trong Component này, do đó UI cần đồng bộ với thời gian hệ thống.
```js
import React from "react";
import format from "date-fns/format";

function App() {
  const [selectedNum, setSelectedNum] = React.useState(100);

  // `time` is a state variable that changes once per second,
  // so that it's always in sync with the current time.
  const time = useTime();

  // Calculate all of the prime numbers.
  // (Unchanged from the earlier example.)
  const allPrimes = [];
  for (let counter = 2; counter < selectedNum; counter++) {
    if (isPrime(counter)) {
      allPrimes.push(counter);
    }
  }

  return (
    <>
      <p className="clock">{format(time, "hh:mm:ss a")}</p>
      <form>
        <label htmlFor="num">Your number:</label>
        <input
          type="number"
          value={selectedNum}
          onChange={(event) => {
            // To prevent computers from exploding,
            // we'll max out at 100k
            let num = Math.min(100_000, Number(event.target.value));

            setSelectedNum(num);
          }}
        />
      </form>
      <p>
        There are {allPrimes.length} prime(s) between 1 and {selectedNum}:{" "}
        <span className="prime-list">{allPrimes.join(", ")}</span>
      </p>
    </>
  );
}

function useTime() {
  const [time, setTime] = React.useState(new Date());

  React.useEffect(() => {
    const intervalId = window.setInterval(() => {
      setTime(new Date());
    }, 1000);

    return () => {
      window.clearInterval(intervalId);
    };
  }, []);

  return time;
}

function isPrime(n) {
  const max = Math.ceil(Math.sqrt(n));

  if (n === 2) {
    return true;
  }

  for (let counter = 2; counter <= max; counter++) {
    if (n % counter === 0) {
      return false;
    }
  }
  console.log("render??");
  return true;
}

export default App;
```
Nếu chạy đoạn code trên bạn sẽ thấy hiện tượng này
![Re-calculate](https://www.joshwcomeau.com/_next/image/?url=%2Fimages%2Fusememo-and-usecallback%2Fclock-prime.png%3Fv%3D2&w=1920&q=75)


