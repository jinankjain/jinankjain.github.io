---
layout:     post
title:      typedArray in JS
date:       2016-08-25
summary:    Curious Case of Typed Arrays in JS
categories: Javascript, Typed Arrays
---

From the last few days I am working on [Bug 1294156 - Float32 RadixSort: NaNs with sign-bit set aren't sorted correctly](https://bugzilla.mozilla.org/show_bug.cgi?id=1294156). I would briefly explain what this bug is all about. So in firefox when try to sort some float32 array which contains some NaN for example your array is [NaN, NaN, 1]. Expected output would be [1, NaN, NaN] but it is kind of strange we get an output [NaN, 1, NaN] which is kind of completely random. In this post I would not go into details why is that happening, but I am going to focus on special type arrays in Javascript known as Typed Arrays, why because I was kind of not aware about them and they are used in inbuilt sorting function of JS :wink: 

### What are Typed Arrays?
In layman terms I would say Typed Array is just some slab raw memory and you can write any sort of binary data in that slab raw memory, that is much like how arrays work in C. Introducing these new type array representation had a huge impact on the performance of the Javascript Engine, now we don't have convert the data to a native representation which help in reducing that conversion cost that we had to pay before the introduction of typed arrays.

There are different types of views that can be associated with these typed arrays for example Float32Array, Float64Array, Int32Array, and Uint8Array. There is nothing much to explain in this as their names are quite self explanatory. These are used to represent somewhat homogenous data types but as I said earlier typed array is just a slab of raw memory, so you can also create heterogenous arrays i.e an array consisting of [Int32, Float32, Int64]

So the next question that might come to everyone's mind that how do you extract data from such hetrogenous arrays. So for that we have a special API known as DataView which allows us to read and write arbitrary data types at arbitrary byte offsets. 

### Basic Examples
Now moving on to some basic examples which would show how to use these typed arrays.

To use Typed Arrays you need a create a Array Buffer and a view for it. This can be done in two ways. Let's start with an easy way:

``` javascript
let f32 = new Float32Array(8); // declare a float32 array of size 8
f32[0] = 1.2
f32[1] = 2.3
```
In this case you directly create an array buffer and it's associated view. The other way would be first create an array buffer and then create the data view for the stored data.

``` javascript
let ab = new ArrayBuffer(256); // 256 byte of Array Buffer
```

For creating data view for this array buffer we could select the complete array buffer or some part of it. So you just need to pass two more parameters byteOffset and length. Let's see how can we do that:

``` javascript
let uaFull = new Uint8Array(ab); // Complete buffer as Uint8
let uaFirstHalf = new Uint8Array(ab, 0, 128);
let uaThirdQuater = new Uint8Array(ab, 128, 64);
```

There is one more way through you can create data view using the DataView API provided by Javascript. Suppose we have some file format that has a header with an 8-bit unsigned int followed by two 16-bit ints. Let's see how can we extract that data from array buffer:

``` javascript
let dv = new DataView(ab);
let a = dv.getUint8(0);
let b = dv.getUint16(1); // 1 byte offset
let c = dv.getUint16(3); // 3 byte offset
```

By default all the values are read in the big-endian if you want to read some values stored in little-endian format, then that can be done by passing an optional boolean parameter

``` javascript
let a = dv.getUint8(0, true);
```

### Browser APIs that support Typed Arrays

##### File API
The file API lets you access the local files on the system. There is a small piece of code that demonstrate how we can use ArrayBuffer to get the bytes of the submitted local file

```javascript
let fileInput = document.getElementById('fileInput');
let file = fileInput.files[0];
let reader = new FileReader();
reader.readAsArrayBuffer(file);
reader.onload = function () {
	let arrayBuffer = reader.result;
   	···
};
```

##### XMLHttpRequest
Newer version of XMLHttpRequest API supports array buffer

```javascript
let xhr = new XMLHttpRequest();
xhr.open('GET', someUrl);
xhr.responseType = 'arraybuffer';
    
xhr.onload = function () {
	let arrayBuffer = xhr.response;
    ···
};
    
xhr.send();
```

There are some more APIs which now support the use of ArrayBuffer.

I would like to conclude the post with this. Hope you like this post.


&lt;/Happy Coding/&gt;