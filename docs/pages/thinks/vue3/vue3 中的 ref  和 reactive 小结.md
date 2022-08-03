#### vue3.0 中的 ref  和 reactive 小结

在vue3.0中，声明一个变量最常使用的就是ref  和 reactive 两种类型。这篇来总结一下两者的相同点和不同点。

一、ref

创建一个响应式的变量，主要是一些 **基本数据类型**，可以直接返回创建的值。

因为ref( ) 创建的是一个对象，所以在js中读取使用 **.value 形式获取**, 但在 template模板中可以直接读取，自动展开渲染内部的值。

```vue
<template>
	{{test}}
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
    
export default defineComponent ({
    setup () { 
        const test = ref('hello')
        
        console.log(test.value) // hello
        
        return {test}
    }
})

</script>
```

 二、reactive

创建一个响应式的对象，主要是 **object 和 array** 类型。

它与ref创建的变量有几点不同：

1. 在template模板中，需要用 x.y 的形式获取值；
2. 在js中，不需要.value，可以 **直接修改**
3. 可以直接返回创建的值，以链式调用读取，也可以直接读取变量里的值（需要用到 toRefs )

```vue
<template>
	{{test.name}}
	{{test.message}}
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';
    
export default defineComponent ({
    setup () { 
        const test = reactive({
            name: 'hello',
            message: 'world'
        })
        
        console.log(test.name) // hello
        
        return {test}
    }
})

</script>
```

三、toRefs

当遇到一些 reactive 创建的对象比较多的时候，我们又不想在template中使用链式调用。这个时候可以使用 toRefs， 结合扩展运算符 `...`  可以很方面的将他们暴露出来。

它的作用是将reactive 创建的变量，转化为普通的响应式变量。

```vue
<template>
	{{name}} // hello
	{{message}} // wolrd
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue';
    
export default defineComponent ({
    setup () { 
        const test = reactive({
            name: 'hello',
            message: 'world'
        })
        const testRef = toRefs(test)
      
        return {
            ...testRef
        }
    }
})

</script>
```

四、isRef

最后补充一个isRef ，用于判断当前这个变量是不是通过 ref ( ) 创建出来的。

```vue
<script lang="ts">
import { defineComponent, isRef } from 'vue';
    
export default defineComponent ({
    setup () { 
        const test1: string = 'hello'
        const test2 = ref<string>('world')
        const test3 = reactive({
            age: 18
        })
        
        console.log(isRef(test1))  // false
        console.log(isRef(test2)) // true
        console.log(isRef(test3)) // false
        
        return {
            test1,
            test2,
            test3
        }
       
    }
})

</script>
```

