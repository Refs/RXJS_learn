# Function programming in javascript

> video: https://www.youtube.com/watch?v=1DMolJ2FrNY&list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84&index=4

> 这应该是学习 rxjs 的前提， 而 rxjs 又是学习 ngrx 的前提， rxjs 的很多的操作符 都是来源于 普通的 es array 方法的；

## filter

>  filter : is a function on the array that accepts another function as it's argument which it will use to return a new filtered version od the array 

```js
var animals = [
    { name: 'Fluffykins', species: 'rabbit' },
    { name: 'Caro', species: 'dog' },
    { name: 'Hamilton', species: 'dog' },
    { name: 'Harold', species: 'fish' },
    { name: 'Ursula', species: 'cat' },
    { name: 'Jimmy', species: 'fish' },
]

// 传统写法
var dog = [];
for (var i = 0; i < animals.length; i++) {
    if (animals[i].species === 'dog') {
        dog.push(animals[i])
    }
}

// array.prototype.filter
var dogs = animals.filter(function(animal) {
    return animal.species === 'dog'
})

// filter accepts anoter callback function which is sended to another function, filter will loop through each item in the array and for each item it's going to pass it into the callback function and when it does it will expect the callback function to return either true or false to tell filter whether or not this item should be in the new array . When the it is  done it will return the new filtered array 

// 增强写法： 函数式编成的一个好处是，函数的复用
var isDog = function(animal) {
    return animal.species === 'dog'
};
var dogs = animals.filter(isDog);
// reject() is NOT built into js like filter is. you can find reject in underscore.js and simliar libraries
var otherAnimals = animals.reject(isDog);


```

## map

> just like filter map is another high-order function which accepts anoter functions as its arguments; Also, like filter it goes through an array, but unlike filter it doesn't throw the objects away instead it transform them  

```js
var animals = [
    { name: 'Fluffykins', species: 'rabbit' },
    { name: 'Caro', species: 'dog' },
    { name: 'Hamilton', species: 'dog' },
    { name: 'Harold', species: 'fish' },
    { name: 'Ursula', species: 'cat' },
    { name: 'Jimmy', species: 'fish' },
]

// we want to get an array of all the names of all the animals 

// 传统做法
var names = [];
for (var i = 0; i < animals.length; i++) {
    names.push(animals[i].name)
}

// Map will take a callback function, just like filter does . The callback function will be passed each item in the animals array . Filter expect that its callback function to return a true or false value that determine wheither or not the item should be included in the array or not . Map will include all the items in the array , but insetead it expects the callback function to return a transformed object that it will put into the new array, instead of the original animal in this case that will be the name ;
var names = animals.map(function(animal) {
    return animal.name;
}) 

// Using map to return a subset of an object like this where we just return the name property is a very common usage pattern, however since map just expects the callback to return any object , we can use it to create completely new objects 
var names = animals.map( function(animal) {
    return animal.name + 'is a' + animal.species
} )

```

## reduce 

> we have learned a couple of higher-order functions , map, filter and reject. What all theses have in common is that they transform a list into something else . Map will take an array and tranform that into an array of the same length but with each individual item transformed . Filter transforms an array into a smaller array . Reject does the same thing as filter but inverted. Find does the same thing as filter but only returns the first item so that transforms an array into a single item. 

> map, filter, reject, find are all list tranformations they turn your list into something else but they all pretty specific. Reduce is not , reduce is the multi tool on list transformations , it can be used to express any list transformation. in fact we can use reduce to implement function like all above function 

> Reduce is the super list transformation that you can fall back on if you can't find a prebuilt list tranformation that fits your problem   

```js
var orders = [
    { amount: 250 },
    { amount: 400 },
    { amount: 100 }, v
    { amount: 325 }
]

// Our mission is to summarize the amounts to show you how to do this use reduce 

// 传统做法：
var totalAmount = 0;
for (var i = 0; i < orders.length; i++) {
    totalAmount += orders[i].amount;
}

// use reduce
// reduce is a function on the array object and just like map and filter it takes a callback function , but unlike map and filter it also wants an object . You can just think of this object as a starting point for our sum , and it's going to zero. 

// just like map reduce will also receive the iterated item but it's going to the second argument 

var totalAmount = oders.reduce(function(sum, order) {
    return sum + order.amount
}, 0)
/**
*   reduce 会接收两个参数，一个是callback函数，一个是一个初始值
*   初始值 会首先赋值给 callback 的第一个参数， 紧接着callback 每一次的执行结果，有又会赋值给callback的第一个参数，
*   数组每次遍历的 item 会赋值给callback 函数的第二个参数；
*   数组每遍历一个元素，callback都会被执行一次
*/

```

## Reduce Advanced 为操作数组提供了一个函数式编程的接口；

> 你想要什么， 就从 从 reduce 里面去返回什么， 同样你的初始值 就去传递什么； 以这个观点来看， reduce 的确是可以将 一切都处理了；

```js
import fs from 'fs';
var output = fs.readFileSync('data.txt', 'utf8')
    .trim()
    .split('\n')
    .map(line => line.split('\t'))
    .reduce(
        (customers, line) => {
            customers[line[0]] = customers[line[0]] || [];
            customers[line[0]].push({
                name: line[1],
                price: line[2],
                quantity: line[3]
            })
            return customers
        }, {}
    )

// 与上面简单的使用 reduce 不同，上面是想返回一个数值， 所以 刚开始的时候就去传入一个数值； 而此处我们想要返回一个对象， 所以 init 的时候，就去传入一个对象；结果reduce 方法 返回的也是一个对象； 

// 同样， 我们若想达到 map 与 filter 的效果，只要init 的时候 传入一个 [] 最后返回的时候，也是一个数组； 这就是 reduce 的意义，其为操作数组，提供了一个 函数式编程的结构

```


```js

// 求各同学的总分 sum:

var arr = [
    {
        name:'lisi',
        age:21,
        score:{
            yuwen:40,
            shuxue:50,
            yingyu:60
        }
    },
    {
        name:'zhangsan',
        age:25,
        score:{
            yuwen:10,
            shuxue:20,
            yingyu:30
        }
    }
]

var result= arr.reduce(
    (a,r)=>{
        a[r.name]=Object.values(r.score)
                        .reduce(
                            (aa,rr)=>aa+rr
                        );
        return a;}
,{})

```

### Object.values(obj)

> Object.values()返回一个数组，其元素是在对象上找到的可枚举属性值。属性的顺序与通过手动循环对象的属性值所给出的顺序相同。

```js
var obj = { foo: 'bar', baz: 42 };
console.log(Object.values(obj)); // ['bar', 42]

// array like object
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.values(obj)); // ['a', 'b', 'c']
```