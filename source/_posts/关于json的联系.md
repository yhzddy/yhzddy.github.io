---
title: 关于json的联系
date: 2019-09-17 22:01:37
tags: json，对象序列化
categories: javascript
thumbnail: /assets/gg.jpg
---

前因：
有个需求json格式的多条数据，所以今天在公司里做一个Array bb = [{name，age}，{name，age}]这样的数据类型,我通过调用arrayObject.push(newelement1，newelement2，....，newelementX)，来进行数据填充。在console台中非常完美的显示出来了，但是在进行表单提交数据到服务器的时候，数据的格式非常奇怪。

    这里我举一个例子 shuzu = []，key ：value格式。shuzu ： bb 这时候上传的数据格式应该是shuzhu: [[0],[1],....,[X]],可是在数据被服务器拒绝。
    经过排查，在http报文请求参数Form Data发现数据格式为shuzhu[0].name,shu[0].age,shu[1],name.shuzu[1].age
    理想情况name和age属性应该一个值，而不应该是分散的。
    出现这个问题因为我没有做json的序列化。
    数组中的js对象没做序列化
    [object,object]
    做序列化：
    bb = '[[0],[1],....,[X]]'
    shuzu ：bb
    
所以这里我要提到序列化的知识。

**序列化是什么？**
        
    百科的解释：序列化 (Serialization)是将对象的状态信息转换为可以存储或传输的形式的过程。 
    基本上所有的语言都有序列化对象的方法。“字符串”对于服务器端来说不管哪种语言都是可以识别的。  
    若作为网络的传输就是将js对象转换为字节流，将字节流转换回js对象 

**为什么要序列化呢？**

    网络数据传输，可以直接发送字符串，但不能直接发送一个结构体。
    网络上传输数据，因为发送端和接收端，通常不能保证是两边是相同的编程语言，
    直接将结构体的数据整理成流发送过去，数据排序或者长度会跟你想象的不一样。

**序列化有什么作用呢？**
    
    1.以某种存储形式使自定义对象持久化；
    2.将对象从一个地方传递到另一个地方，序列化确实可以很好的跨语言平台
    3.使程序更具维护性。

**通常的解决办法：**

    约定一个协议，协议规定好数据流中每个字节的含义。
    发送端要保证按照协议要求组装好数据流。
    接收端按照协议规定读取出里面的数据（解析）。

通过上面序列化的概念，我们在回到JSON(JavaScript Object Notation)这个来讨论，json是一种轻量级的数据交换格式。

    通过把任何JavaScript对象变成JSON，就是把这个对象序列化成一个JSON格式的字符串，这样才能够通过网络传递给其他计算机。
    如果收到一个JSON格式的字符串，只需要把它反序列化成一个JavaScript对象，就可以在JavaScript中直接使用这个对象了。


**javascript内置了序列化函数JSON.stringify(),和反序列函数JSON.parse()**
**1.JSON.stringify()示例**

        var xiaoming = {
            name: '小明',
            age: 14,
            gender: true,
            height: 1.65,
            grade: null,
            'middle-school': '\"W3C\" Middle School',
            skills: ['JavaScript', 'Java', 'Python', 'Lisp']
        };
        
        var s = JSON.stringify(xiaoming);
        //'{"name":"小明","age":14,"gender":true,"height":1.65,"grade":null,"middle-school":"\"W3C\" Middle School","skills":["JavaScript","Java","Python","Lisp"]}'

**2.JSON.parse()示例**

        JSON.parse('[1,2,3,true]'); // [1, 2, 3, true]
        JSON.parse('{"name":"小明","age":14}'); // Object {name: '小明', age: 14}
        JSON.parse('true'); // true
        JSON.parse('123.45'); // 123.45




**使用场景**
1.向后台传递参数、接收后台返回值

    如果后台返回的是一个String（Object序列化后返回），那么需要在js中使用parse转化为Object再使用；
    如果返回的时候传递了类型，比如就是Object，那么直接使用就好

2.在页面间传递数据，特别是数组时

    需要使用序列化，否则IE会报错：不能执行已经释放Script的代码

3.在进行本地存储时

    存储在本地window.localStorage.setItem(key,value)存储的value是json序列化的字符串；
    获取得到的window.localSorage.getItem(key)也是json序列化的字符串，需要经过json的反序列化进行使用（常见json序列化数组）

**额外知识点**


|类型|toString|
|:---:|:---:|
|Object      	|   返回"[object Object]"|
|stringObject	|   返回字符串|
|NumberObject	|   把一个 Number 对象转换为一个字符串，并返回结果。|
|booleanObject	|   把一个逻辑值转换为字符串，并返回结果。|
|arrayObject	    |   把数组转换为字符串，用逗号间隔，并返回结果|
|dateObject	    |   把 Date 对象转换为字符串，并返回结果|

自定义对象调用js 的 toString 方法，返回的不是对象序列化后的字符串，而是 [object Object] 字符串。这是因为自定义对象没有重写 toString 方法。



通过记录工作上的问题，学习知识，本文章的知识点来自网络上的各位前辈，仅作学习记录参考，感谢前辈们。
更多帮助请参考[廖雪峰](https://www.liaoxuefeng.com/wiki/1022910821149312/1023021554858080)