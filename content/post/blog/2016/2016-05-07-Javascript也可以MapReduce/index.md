---
layout: single
title: Javascript也可以MapReduce
date: 2016-05-07
categories:
  - 博客日记
tags:
  - 每周五百字
--- 
想不想用做一下大数据试验？不需要各种复杂的理论，你只需要使用Javascript即可。近期我研究了一下Javascript语言自带的map、reduce、filter等方法，尝试一下如何使用MapReduce的思路统计我工作日志中各种词汇出现的频率，也算是一个轻量级的“大数据”“挖掘”试验了。

下面举个例子，使用的数据源是我六年多的工作日志，大概两千篇，三万六千多行。使用nodejs环境运行javascript，实际上完全可以在浏览器里运行，nodejs操作文件比较方便，为了省事，直接nodejs吧。要想将中文单词从语句中分离出来需要编写中文分词代码，但是由于不是本例研究重点，咱直接使用nodejieba（一个中文分词库，使用方便，执行效率也挺不错）。

具体思路如下：

1、打开工作日志文件（txt），将每一行的内容存入一个数组，得到一个存满字符串的数组；

2、将每一行的字符串使用中文分词库进行分割，得到一个个中文单词（当然日志中也有英文和数字）；

3、使用reduce方法全部汇总到一个数组里，此时单词是全部的有重复的数据；

4、再次使用reduce方法将单词汇总到一个包含两个数组的数组，其中之一保存去重后的单词，另外一个保存与之对应的单词计数；

5、再次使用reduce方法，变换数组为二维数组，第一列为单词，第二列为与之对应的单词的个数；

6、将结果写入文件；

经过统计，我这些年的工作日志出现的中文单词频率从高到底的前几名分别是：工作（4269次）、和（3781次）、我（2919次）、在（2703次）、完成（2304次）、任务（2254次）。连起来读也挺有意思的。

还有些比较有意思的，“问题”出现967次，“可以”出现1095次，看来办法总比问题多啊。

说起来好像比较抽象，还是放代码比较直接：

var fs = require('fs');

var nodejieba = require("nodejieba");

nodejieba.load();

fs.readFile('work.txt', 'utf8', function (err, data) {

if (err) {

console.log(err);

}

var strs = data.split('\n') // 先将读入的日志按照行分为一个书组

.reduce(function (last, now) {

nodejieba.cut(now).forEach(function (word) {

last.push(word);

});

return last;

}, []) // 通过reduce将每行的单词分出来，最终汇总成为一个包含全部单词的数组（有重复）

.reduce(function (last, now) {

var index = last[0].indexOf(now);

if (index === -1) {

last[0].push(now);

last[1].push(1);

} else {

last[1][index] += 1;

}

return last;

}, [[], []]) // 统计单词的个数，数组第一个元素为存放单词的数组，第二个元素为存放对应单词个数的数组

.reduce(function (last, now, index, context) {

var zip = [];

last.forEach(function (word, i) {

zip.push([word, context[1][i]])

});

return zip;

}); // 变换数组，变成二维数组，第一列为单词，第二列为单词对应的个数，没有传递给reduce第二个参数，默认为数组的第一个元素

var stream = fs.createWriteStream("count.txt");

stream.once('open', function (fd) {

strs.forEach(function (word) {

stream.write(word[0] + ',' + word[1] + '\n');

})

stream.end();

});

});