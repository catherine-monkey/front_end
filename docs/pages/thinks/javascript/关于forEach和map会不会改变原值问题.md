### 关于forEach会不会改变原数组问题

hello, 今天是我复工（好好学习技术）的第一天。先奉上我最爱的吸血鬼日记，清洗一下大家的眼睛，欣赏一下帅哥美女，然后开启今日的学习。

进入正文，上午coding的时候发现了关于数组循环的问题，我这人又比较懒就琢磨能不能简约点。于是就有了今天的这篇小总结~

大家比较熟悉的就是forEach不会改变原数组的值，map不改变原数组，可以返回一个新数组。

那有时候我们想修改原数组中的值，又不想使用map创建一个新数组的时候，可以怎么做呢?

凡事都可能有例外的情况，比如：如果这个数组的某一项是引用类型，那么也可以使用forEach进行修改。

```javascript
a = [1,2, {num: 1}, 'abc']
a.forEach(item => {
	item.num = 3
})
console.log(a)  // [1,2, {num: 3}, 'abc']
```
这样就可以直接写，方便了很多。但是注意，一定要是引用类型。
```javascript
a = [1,2, {num: 1}, 'abc']
a.forEach(item => {
	item = 'lalala'
})
console.log(a) // [1,2, {num: 1}, 'abc']
```

如上图，如是修改基础数据类型 `String Number Boolean Undefined Null`，那就不会改变。

然后再来看看map, map自身就接收一个返回值。

```javascript
a = [1,2,3,4]
a.map(item => {
	return item*2
})
console.log(a) // 2,4,6,8
```

