# RXJS_learn

video: https://www.youtube.com/playlist?list=PL55RiY5tL51pHpagYcrN9ubNLVXF8rGVi

## Course 10 switchMap() 

an operator which allows us to trigger some value emissions whenever another onserverable emits a value 

>  use in http request : if you have some Auto completion functionality and you reach out to you server whenever the user type someting you don't want these old request to continue whenever whenever the user changes his opinion , you 're sending a new ewquest and you want to cancel the old one you want to cancel the old observables  so you don't have to handle the data which you will eventually come back . (这里面的一个关键点就在于，当一个observable 被订阅的时候，其就会去执行异步的操作，observer 会去监听异步操作的结果，)  （还有一个关键点在于，the data which you will eventually come back， 我们做出的异步操作，发送出去的请求，无论做出请求的 observable 有没有被cancel, 操作的结果都会被正常返回，不同的是 返回的结果 不会被 预定的observer（触发订阅事件的） 监听;;  新的observable 生成之后， observer 会转而 订阅与监听 新的observable）   所为cancle observabe 意思并不是去拦截 已经开始进行的异步操作（发送出去的请求<请求一旦发送出去，就没有请求这一说，且能够正常返回>），只不过是取消监听的而已；

> observable 被订阅的时候，代码会执行，调用next 方法的时候，observer 会被执行；

> 上面的理解有误 原因就在于官方文档的这一句话；
> "calling" or "subscribing" is an isolated operation: two function calls trigger two separate side effects, and two Observable subscribes trigger two separate side effects. As opposed to EventEmitters which share the side effects and have eager execution regardless of the existence of subscribers, Observables have no shared execution and are lazy.
 
> lazy computations 


> Each call to observable.subscribe triggers its own independent setup for that given Observer.

> Each Observable must define how to dispose resources of that execution when we create the Observable using create 
 

This shows how subscribe calls are not shared among multiple Observers of the same Observable. You can do that by returning a customun subsrcibe function from within function subscribe()


```js
// 未使用 swithmap 时的情况

var button = document.querySelector('button');
var obs1 =  Rx.Observable.fromEvent( botton, 'click');
var obs2 = Rx.Observable.interval(1000);

obs2.subscribe(
    (event) => {
        obs2.subscribe(
            (value) => {
                console.log(value);
            }
        )
    }
)

// 我们每点击一次button 就会有
// 现在自己不理解的地方，在于同一个 observable 被多次订阅的情况；

```



```js
var button = document.querySelector('button');

var obs1 = Rx.Observable.fromEvent('button', 'click');


// whiat I want to do is  we want to start an interval(间隔) which emits a new value every x seconds . wheneve i click the button but i want that emitting observable that interval to start over when I click the button again so the old emission the old interval should be conceled   

// we switch to values  and we cancel any old ones 

// Each time it observes one of these inner Observables  


```