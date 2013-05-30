---
layout: post
title: "javascript quick learning"
description: ""
category: 
tags: []
---
{% include JB/setup %}


字符串："perth charles"  
求字符串长度："perth charles".length  


"cake".length * 9  
confirm("you must be kidding me!\n");  弹出窗口让用户确认某些信息
prompt("what is your name?")；	弹出窗口接受用户输入
console.log("Hello");	相当与printf语句

注意这两个比较操作符
=== Equal to
!== Not equal to

"wonderful day".substring(3,7);		输出字符的第4位到第7位

声明三种变量
a. var myName = "Leng";
b. var myAge = 30;
c. var isOdd = true;

// This is what a function looks like:
var divideByThree = function (number) {
    var val = number / 3;
    console.log(val);
};	//注意这个地方也有分号

生成一个0到1之间的随机数，如一次结果为：0.8760658339597285
var computerChoice = Math.random();

//检测x的类型
typeof(x) ！== 'number'

// Example of a for loop:
for (var counter = 1; counter < 6; counter++) {
	console.log(counter);
}

数组/列表
var arrayName = [data, data, data];
arrayName.length	//求数组/列表 长度
arrayName.push();	//给列表添加元素

isNaN()	//判断是否是一个数

逻辑运算符跟C一样


//一个对象的例子
var phonebookEntry = {};
phonebookEntry.name = 'Oxnard Montalvo';
phonebookEntry.number = '(555) 555-5555';
phonebookEntry.phone = function() {
  console.log('Calling ' + this.name + ' at ' + this.number + '...');
};
phonebookEntry.phone();


//又一个典型的对象声明例子
var friends = {};//相当与一个对象列表？
friends.bill = {
  firstName: "Bill",
  lastName: "Gates",
  number: "(206) 555-5555",
  address: ['One Microsoft Way','Redmond','WA','98052']
};

friends.steve = {
  firstName: "Steve",
  lastName: "Jobs",
  number: "(408) 555-5555",
  address: ['1 Infinite Loop','Cupertino','CA','95014']
};


//一个更加复杂的例子
/*
var friends = {};
friends.bill = {
    firstName: "Bill",
    lastName: "gates",
    number: "20",
    address: ["beijing", "china"]
};
friends.steve = {
    firstName: "Steve",
    lastName: "dddddd",
    number: "22",
    address: ["shanghai", "china"]
};
var list = function(){
    for(var example in friends){
        console.log(example);
    }
};

var search = function(name){
    for(var entity in friends){
        if(friends[entiry].firstName === name){
            console.log(friends[entiry]);
            return friends[entity];
        }
    }
};
*/


