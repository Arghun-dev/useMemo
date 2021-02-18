# useMemo

this is performance optimizaion.

Notice we have a `clock` which re-renders every second. so React have to re-render every second, this component has to re-render every single second, the way that React works that if it re-render the parent component by default it will re-render all the child components as well, it's kind of performance optimization, they don't have to go check everything, it says well, this changed probably everything under need to changed and it doesn't do extra checking and this render method in general is really fast.

```js
import React, { useState, useMemo } from 'react';

const fibonacci = n => {
  if (n <= 1) {
    return 1;
  }
  
  return fibonacci(n - 1) + fibonacci(n - 2)
}

const MemoComponent = () => {
  const [num, setNum] = useState(1);
  const [isGreen, setIsGreen] = useState(true);
  const fib = useMemo(() => fibonacci(num), [num]);
  
  return (
    <div>
      <h1
        onClick={() => setIsGreen(!isGreen)}
        style={{ color: isGreen ? "limeGreen" : "red" }}
      >
        useMemo Example
      </h1>
      <h2>
        Fibonacci of {num} is {fib}
      </h2>
      <button onClick={() => setNum(num + 1)}>+</button>
    </div>
  )
}
```

fbonacci operation is a really heavy operation,
if we don't use `useMemo` our application is going to get really slow, because it's going to recalculate every single time, user clicks the fibonacci.
but `useMemo` solves this problem
