---
layout: post
title: '[js] 비동기 함수의 순차적 실행 보장'
date: 2019-10-25 00:10
categories: js
tags: [js]
---
async/await 를 이용하면 간단하게 비동기함수를 순차적으로 실행할 수 있다.

```javascript
async () => {
  await asyncFn()
  await asyncFn()
  await asyncFn()
}
```

하지만 이것은 caller 입장에서만 처리가 가능한 방법이다. `asyncFn` 함수를 제공하는 입장에서 `asyncFn` 이 순차적으로 실행됨을 보장하고자 하면 어떻게 함수를 정의해야 할까

예를 들면 `asyncFn` 을 사용하는 caller 는 아래와 같이 해당 함수를 막? 호출할 수도 있다. (이는 `asynFn` 함수를 제공하는 입장에서 통제할 수 있는 영역이 아니다)

```javascript
async () => {
  asyncFn()
  asyncFn()
  asyncFn()
}
```

위와 같이 `await` 없이 연속적으로 비동기함수를 호출하는 상황에서도 `asyncFn` 의 순차적 실행을 보장할 수 있도록 유틸성 함수를 `atomic` 을 하나 만들어 보았다.

```javascript
function atomic(asyncFn) {
  const queue: Array<Promise<void>> = []
  return (...args) => {
    queue.push(
      new Promise(async (resolve) => {
        if(queue.length > 0){
          await queue[queue.length - 1]
          queue.shift()
        }
        const result = await asyncFn(...args)
        resolve()
        return result
      }),
    )
  }
}
```

<br>

### Usage
```javascript
const atomicAsyncFn = atomic(asyncFn) // atomic 으로 래핑된 함수 asyncFn 은 어떤 상황에서도 순차적 실행이 보장된다
async () => {
  atomicAsyncFn()
  atomicAsyncFn()
  atomicAsyncFn()
}
```

<br>

### testcase
```javascript
it('should be excuted subsequentially with continuous call', async () => {
  const delay = ms => {
    return new Promise(resolve => {
      setTimeout(resolve, ms)
    })
  }
  let count = 0
  const asyncFn = async () => {
    await delay(100)
    count++
  }
  asyncFn()
  asyncFn()
  await delay(150)
  expect(count).to.be.equal(2)

  count = 0
  const atomicAsyncFn = atomic(asyncFn)
  atomicAsyncFn()
  atomicAsyncFn()
  await delay(150)
  expect(count).to.be.equal(1)
  await delay(100)
  expect(count).to.be.equal(2)
})
```
