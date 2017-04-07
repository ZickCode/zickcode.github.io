---
title: js数组方法
date: 2017-04-07 15:21:57
tags:
---

学习js数组方法的笔记

#### 1.数组长度
```
arr = [];
arr.length;    //输出0
```

#### 2.数组元素的添加和删除
```
arr = [];
arr[0] = '1';    //向数组中添加元素
delete a[0];    //删除了数组index=1位置的元素，但是数组长度不会减少
```

#### 3.数组遍历
```
arr = [];
for(var i=0;i<arr.length;i++){}    //简单的for循环遍历
```
如果不能确定数组是否为稠密数组，或不能确定所有元素都是合法数据，则需要进行检测
```
for(var i=0;i<arr.length;i++){
    if(!arr[i]) continue;    //跳过null，undefined和不存在的元素
    if(arr[i] === undefined) continue;    //跳过undefined和不存在的元素
    if(!(i in arr) ) continue;    //跳过不存在的元素
}
```
简单的for/in循环(index in array)，但是性能会略低于for循环
```
for(i in arr){}
```
forEach是数组的方法，作用是遍历一遍数组里面的元素，不能用break中断，只能使用try/catch语句抛出异常中断
```
arr.forEach(function(){});
```

#### 4.多维数组
```
arr = [[1],[2,3]]
arr[2][2];    //输出3，使用多个[]访问
```

#### 5.数组方法
```
var arr = ['1','2','3'];
```
join方法，将数组中所有元素转换为字符串并连接在一起，参数是分割元素的字符串
```
arr.join();    //输出123
arr.join(',')    //输出1,2,3
```
reverse方法，将数组顺寻颠倒
```
arr.reverse().join();    //输出321
```
sort方法，将数组按照字母表顺序进行排序(先排大写，再排小写)，参数为一个函数，可以指定排序规则
```
arr = [22,1,4444,555];
arr.sort(function(a,b){
    return a-b;
});    //输出[1,22,555,4444]
```
如果返回一个小于0的值，则a在前，大于0则b在前，等于0则两者顺序无所谓
concat方法，连接两个数组并返回一个新的，不会修改原数组
```
arr = [1,2,3];
arr.concat([4,5]);    //输出[1,2,3,4,5]
```
slice方法，返回指定数组的一个片段，不会修改原数组
如果是一个参数则当作起点一直到数组尾部；
如果是两个参数则前一个为起点，后一个为结束点；
如果参数为负数，则表示倒数第n个元素。
```
arr = [1,2,3,4,5];
arr.slice(0,2);    //输出[1,2,3]
arr.slice(2);    //输出[3,4,5]
arr.slice(3,-1);    //输出[4,5]
```
splice方法，在数组中插入或删除元素的方法 ，会修改调用的数组
第一个参数指定了插入/删除的起始位置；
第二个参数指定了删除元素的个数，如果省略，则从起点到结尾的元素都会被删除；
```
splice()返回一个由删除元素组成的数组，如果没有删除元素，会返回一个空数组
arr = [1,2,3,4,5];
arr.splice(3);    //返回[4,5]，arr=[1,2,3]
arr.splice(1,3);    //返回[2,3,4]，arr=[1,5]
```
前两个参数之后的任意个数的参数指定了需要插入到数组中的元素，从第一个参数的位置插入
```
arr = [1,2,3,4,5];
arr.splice(2,2,'a','b');    //返回[3,4]，arr=[1,2,'a','b',5]
```
push方法，在数组的尾部添加n个元素，返回数组新的长度，会修改调用的数组
pop方法，删除数组的最后一个元素，返回他删除的值，会修改调用的数组
```
arr = [];
arr.push(1,2,3);    //arr=[1,2,3]，返回3
arr.pop()    //arr=[1,2]，返回3
arr.push([2,3]);    //arr=[1,2,[2,3]]，返回3
arr.pop();    //arr=[1,2]，返回[2,3]
```
unshift()方法，和push相反，在数组头部插入，也返回数组新的长度，多个参数插入时是一次性插入，元素顺序和参数列表里的一致
shift()方法，和pop()相反，删除数组第一个元素，返回删除的元素
```
arr = [1];
arr.unshift(2);    //arr=[2,1]，返回2
arr.shift();    //arr=[1]，返回2
```
toString方法，将数组的每个元素转化为字符串，并输出用逗号分割的字符串列表。
toLocalString方法，是toString方法的本地化版本。

##### ES5新增的数组方法
forEach方法，遍历一遍数组里面的元素，不能用break中断，只能使用try/catch语句抛出异常中断
可以有三个参数，分别为数组元素，元素的索引，数组本身。
```
varr arr = [1,2,3];
var sum = 0;
//累加并赋值给sum
arr.forEach(function(value){
    sum += value;
});    
//将数组的每个元素都+1
arr.forEach(function(i,j,k){
    k[j] = i+1;
});
```
map方法，将调用的数组的每个元素传递给函数，然后返回一个数组，包含该函数的返回值。不会修改原数组。
```
a = [1,2,3];
b = a.map(function(x){ renturn x*x });    //b=[1,4,9]
```
filter方法，返回一个调用数组的子集。传递的函数用来做逻辑判定，如果返回值是true，则把元素添加到子集中。该方法会跳过稀疏数组中缺失的元素，所以返回的数组总是稠密的。
```
arr = [1,2,3];
small = arr.filter(function(x){ return x<3; });    //small = [1,2]
var dense = sparse.filter(function(){ return true; });    //压缩稀疏数组的空缺，返回一个稠密数组
a = a.filter(function(x){ renturn x !== undefined && x !== null; });    //压缩并删除数组中undefined和null的元素
```
every方法，some方法，这两个方法是对数组的逻辑判定，对数组用指定的函数进行判定，返回true/false，一旦确定返回值后，就会停止遍历数组。
```
a = [1,2,3,4,5];
//every在第一次遇到false的时候，就停止遍历，返回false，如果一直为true，则遍历整个数组。
a.every(function(x){
    return x<10;
});    //返回true;
//some在第一次遇到true的时候，停止遍历，返回true，如果一直为false，则遍历整个数组。
a.some(function(x){
    return x<3;
});    //返回true，第一个元素小于3，停止遍历，返回true;
```
reudce方法，reduceRight方法，使用指定的函数将数组的元素进行组合，生成单个值。
```
a = [1,2,3,4,5];
var sum = a.reduce(function(x,y){
    return x+y;
});    //将数组里的元素累加并返回累加的值
```