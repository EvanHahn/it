# async-iterator-buffer-stream

[![Build status](https://travis-ci.org/achingbrain/async-iterator-buffer-stream.svg?branch=master)](https://travis-ci.org/achingbrain/async-iterator-buffer-stream?branch=master) [![Coverage Status](https://coveralls.io/repos/github/achingbrain/async-iterator-buffer-stream/badge.svg?branch=master)](https://coveralls.io/github/achingbrain/async-iterator-buffer-stream?branch=master) [![Dependencies Status](https://david-dm.org/achingbrain/async-iterator-buffer-stream/status.svg)](https://david-dm.org/achingbrain/async-iterator-buffer-stream)

> An async iterator that emits buffers containing bytes up to a certain length

## Install

```sh
$ npm install --save async-iterator-buffer-stream
```

## Usage

```javascript
const totalLength = //... a big number

// all options are optional, defaults are shown
const options = {
  chunkSize: 4096, // how many bytes will be in each buffer
  collector: (buffer) => {
    // will be called as each buffer is generated. the final buffer
    // may be smaller than `chunkSize`
  },
  generator: async (size) => {
    // return a promise that resolves to a buffer of length `size`
    //
    // if omitted, `Promise.resolve(crypto.randomBytes(size))` will be used
  }
}

let buffers = []

for await (buf of bufferStream(totalLength, options)) {
  buffers.push(buf)
}

// `buffers` is an array of Buffers the combined length of which === totalLength
```
