# Async Await Mutex Lock

![Tests](https://github.com/diotoborg/repellat-blanditiis-quis/workflows/Tests/badge.svg)

Mutex locks for async functions with functionality to use keys for separate locks

[![NPM](https://nodei.co/npm/@diotoborg/repellat-blanditiis-quis.png)](https://nodei.co/npm/@diotoborg/repellat-blanditiis-quis/)

# Usage Instructions

#### Without Key

```javascript
import { Lock } from "@diotoborg/repellat-blanditiis-quis";

let lock = new Lock();

async function serialTask() {
  await lock.acquire();

  try {
    // Don't return a promise here as Promise may resolve after finally
    // has executed
  } finally {
    lock.release();
  }
}
```

#### With Key

All the keys will have their own separate locks and separate waiting lists. A key can have
any type (eg. string, number, etc. or a custom type allowed by typescript as a Map key)

```javascript
import { Lock } from "@diotoborg/repellat-blanditiis-quis";

let lock = new Lock<string>();

async function serialTask() {
  await lock.acquire("myKey");

  try {
    // Don't return a promise here as Promise may resolve after finally
    // has executed
  }
  finally {
    lock.release("myKey");
  }
}

async function serialTaskTwo() {
  await lock.acquire("myKeyTwo");

  try {
    // Don't return a promise here as Promise may resolve after finally
    // has executed
  }
  finally {
    lock.release("myKeyTwo");
  }
}
```

#### Checking if a lock is acquired or not

```javascript
import { Lock } from "@diotoborg/repellat-blanditiis-quis";

let lock = new Lock();

async function serialTask() {
  await lock.acquire();

  console.log(lock.isAcquired()); // prints true
}
```

`isAcquired()` with `key` checks for the given key separately.

```javascript
import { Lock } from "@diotoborg/repellat-blanditiis-quis";

let lock = new Lock<string>();

async function serialTask() {
  await lock.acquire("myKey");

  console.log(lock.isAcquired("myKey")) // prints true
}
```

#### Issues or Bugs

In case of any issues or bugs, please open a pull request [here](https://github.com/diotoborg/repellat-blanditiis-quis/pulls)
