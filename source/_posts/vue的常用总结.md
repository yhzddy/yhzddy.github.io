---
title: vue的常用总结
date: 2019-09-22 14:47:01
tags: Vue
categories: Vue
thumbnail: /assets/timg.jpg
---

1.Vue的组件传递属性


1. vue父亲组件传递值的使用
    父组件用到props给子组件传值，子组件只需要做一件事,那就是通过props接收
    父组件：
    ![10775147-f463d4511d501120.png](https://i.loli.net/2019/09/22/GJHdqLgwQbNx263.png)
    子组件：
    ![10775147-f0e970afe93891e4.png](https://i.loli.net/2019/09/22/nNODIadwv9JzSmT.png)
2. vue子组件传递值的使用
    子组件用到$emit给父组件响应，定义一个事件来触发响应的$emit使父组件可以知道有事件改变,进而接收对应的参数。
    父组件：
    ![10775147-f4bbc44393321a26.png](https://i.loli.net/2019/09/22/hGBCqr4Y7AkIRaK.png)
    ![10775147-00dd4916b775bb8b.png](https://i.loli.net/2019/09/22/zkBEKHL3d6NAsYt.png)
    子组件：
    ![10775147-d7ff29acbaa3d652.png](https://i.loli.net/2019/09/22/buI2tAFQklz4S8c.png)
    ![10775147-4d666ddfc4c163d3.png](https://i.loli.net/2019/09/22/XF2aoyEI7Jl5L9G.png)

2.Vuex的基础使用 
1. store的使用
      
        import Vue from 'vue'
        import Vuex from 'vuex'
        Vue.use(Vuex)
        export default new Vuex.Store({
        state: {
            //state就是Vuex中的公共的状态, 可以将state看作是所有组件的data, 
            用于保存所有组件的公共数据.
        },
        getters: {        
            //
            getters属性理解为所有组件的computed属性, 也就是计算属性. 
            vuex的官方文档也是说到可以将getter理解为store的计算属性, getters的返回值会根据它的依赖被缓存起来，且只有
            当它的依赖值发生了改变才会被重新计算。
        },
        mutations: {
            //将mutaions理解为store中的methods, mutations对象中保存着更改数据回调函数,
            该函数名官方规定叫type, 第一个参数是state, 第二参数是payload, 也就是自定义的参数.
            注意:调用mutaions中回调函数, 只能使用store.commit(type, payload)
        },
        actions: {
            //actions 类似于 mutations，不同在于：
                actions提交的是mutations而不是直接变更状态
                actions中可以包含异步操作, mutations中绝对不允许出现异步
                actions中的回调函数的第一个参数是context, 是一个与store实例具有相同属性和方法的对象 
                其中minusPriceAsync采用setTimeout来模拟异步操作,延迟2s执行 该方法用于异步改变我们刚才在mutaions中定义的minusPrice
                调用actions中回调函数, 只能使用store.dispatch(type, payload)
        },
        modules: {
        //给全局变量分组，所以需要写提前声明其他store文件，然后引入这里
        Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割
         }
        })
2. watch和computed属性的使用例子
         
        watch: {
            caseId () {
            this.personForm.caseId = this.caseId  
            }
        },
        computed: {
            caseId () {
            return this.$store.state.common.caseId //拿到store的值
            }
         },

         computed是计算属性，与data相似，但是具有缓存作用
         watch起到监听作用
         该例子为监听缓存中过的caseId
         该段落只做摘要，具体参考[这篇文章](https://blog.csdn.net/garfielder007/article/details/83721038)

3.mounted与created的区别
        
        created:在模板渲染成html前调用，即通常初始化某些属性值，然后再渲染成视图。
        mounted:在模板渲染成html后调用，通常是初始化页面完成后，再对html的dom节点进行一些需要的操作。
4.v-if与v-show
   
        v-if改变dom结构
        v-show仅作视觉效果变化

