#### vue3 中的 watch 小结

主要总结一下在vue3中使用watch的几种常见的方式，在项目使用中依据不同的场景进行使用。

1. 监听一个变量

`watch(obj, (newV, oldV) => {`

`	// newV…`

`})`

注意：

- 如果这个obj是 reactive，那么无法监听到oldV。

- 同样有个好处：reactive自动开启深度监听，不需要deep。



2. ref 变量的深度监听

`watch(xxx, newV => {`

​	`// newV`

`}, {`

​	`deep: true,`

`		immediate: true`

`})`

 

3. 监听多个变量

`watch([xx, yy], ([xnewV, ynewV], [xoldV, yoldV]) => {`

`	// …`

`})`

 PS： 只要其中一个有修改，就监听到变化



4. 监听某个obj的某个属性

`watch(()=> obj.xx, (newV, oldV) => {`

`// newV`

`})`

或者

`watch(() => obj, (newV, oldV) => {`

`// newV`

`})`

 

5. watchEffect —— 自动监听变量，立即生效

   `const obj = reactive({x: 0, y: 1})`

   `watchEffect(()=> {`

   ​	`// obj.x`

   ​	`// obj.y`

   `})`

它与watch的不同之处在于一下几点：

1）不需要声明监听的变量， 在watchEffect中，涉及到的变量就是监听的变量，它会自动监听。

2）初始化的时候会执行一次，自动获取依赖。

3）只能得到最新的值，无法获取到原值。



最后有几个小提示：

1. vue2 和 vue3 中的 新值和旧值的顺序不一样。在Vue2 中是 (oldV, newV)， 而在Vue3 中是 (newV, oldV)。

2. watch 和 watchEffect 可以在同一个页面使用多次，用于监听不同的值。