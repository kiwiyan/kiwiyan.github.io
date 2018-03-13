---
title: nodejs-fs文件操作模块
date: 2018-01-02 23:26:33
tags: fs文件模块
categories: nodejs
comments: true
---

fs模块提供常用文件操作，包含读写等功能，这些操作基本都有【异步】和【同步】两种方式。注意一般参数标注的方式，方法中带中括号的参数表示可选。

## 读取-文件，目录

### 异步读文件 readFile()
readFile(path[, options], callback),第二个参数可选，不设置编码的话，data为buffer数据。路径为文件夹则报错。
```js
fs.readFile('./test.js', 'utf-8', (err, data) => {
    if (err) throw err;
    console.log(data);
})
```
<!-- more -->
### 同步读文件 readFileSync()
readFileSync(path[, options])
```js
let text = fs.readFileSync('./test.js', 'utf-8');
```
或者
```js
let text = fs.readFileSync('./test.js').toString();
```

### 读取一级子目录 readdir() 
readdir(path[, options], callback) 第二个参数为编码方式，可选，默认值'utf-8'。比如文件夹somedir里有文件夹dir1，文件夹dir2，以及文件test.js，那读取的结果为['dir1', 'dir2', 'test.js']，注意是文件名，不是路径;读取的目标不是文件夹则报错。
```js
fs.readdir('./somedir', (err, files) => {
    if (err) throw err;
    console.log(files);
})
```

### 读取文件信息 stat()
fs.stat(path, callba)读取文件相关信息，包括创建时间，内存大小等，常用来判断是一个文件还是一个文件夹
```js
fs.stat('./testDir', (err, stats) => {
    if (err) throw err;
    if (stats.isFile()) { 
        // 如果路径是文件则执行  
    } else if (stats.isDirectory()) {
        // 如果路径是文件夹则执行
    }

})
```
### 读取层级目录

### 监听文件 watch()
fs.watch(filename[, options][, listener]) 监听文件的改变，删除，创建。
文件内容改变对应的事件为 change，创建删除对应的事件是rename 

```js
fs.watch('./testDir', (eventType, filename) => {
    console.log(`事件类型：${eventType}`);
    if (filename) { // 不同操作系统，filename不一定存在
        console.log(`提供的文件名: ${filename}`);
    } else {
        console.log('未提供文件名');
    }
})
```

## 写入-文件，目录

### 写入文件 writeFile
fs.writeFile(file, data[, options], callback) 第一个参数为路径，路径不存在则报错；第二个参数为写入的内容；第三个参数为编码默认为'utf-8'
```js
fs.writeFile('./test.js', 'some data', err => {
    if (err) throw err;
    console.log('write ok');
})
```

### 创建文件夹 mkdir()
fs.mkdir(path[,mode],callback)创建文件夹。第二个参数为操作目录的权限制，可选，默认0o777,表示所有人可读，可写，可执行。
只能创建一层文件目录，创建多层目录可以用递归的方式。
```js
fs.mkdir('./testDir', err => {
    if (err) throw err;
})
```

### 读写大文件 
createReadStream() createWriteStream() 读写大内存文件，搭配只用使用这两个方式会更有效率。
```js
let readStream = fs.createReadStream('./test.js');
let writeStream = fs.createWriteStream('./copy.js');
readStream.on('data', data => { 
    writeStream.write(); // 读取流监听读取的数据，实时写入 
}); 
readStream.on('error', err => { throw err; }); // 读取流监听错误
readStream.on('end', () => { 
    writeStream.end(); // 读取流监听读取完成事件
}); 
```
可以搭配pipe方法更方便实现大文件读写
```js
let readStream = fs.createReadStream('./test.js');
let writeStream = fs.createWriteStream('./copy.js');
readStream.pipe(writeStream); // pipe像管道般将数据流导入另一个文件
readStream.on('end', () => { 
    console.log('write done!')
})
```

