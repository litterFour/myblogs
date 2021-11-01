##### 编程风格

1、组件名应该始终由多个单词组成，除了根组件App，以及\<transition>、\<component> 之类的Vue内置组件。避免与现有或者未来的HTML元素冲突。因为所有的HTML元素名称都是单个单词的。
```vue
反面例子：
app.component('todo', {
  // ...
})
export default {
  name: 'Todo',
  // ...
}
```
```vue
正面例子：
app.component('todo-item', {
  // ...
})
export default {
  name: 'TodoItem',
  // ...
}
```
2、prop的定义应该尽量详细，至少制定其类型。

细致的prop定义有2个优势：
* 它们写明了组件的API，所以组件的设计用法可以通俗易懂；
* 在开发环境下，如果为一个组件提供了格式不正确的 prop，Vue 将会告警，以帮助你捕获潜在的错误来源。
```vue
// 更好的例子
props: {
    status: {
        type: String,
        required: true,
        validator: value => {
            return [
                'syncing',
                'synced',
                'version-conflict',
                'error'
            ].includes(value)
        }
    }
}
```
3、不要在同一个元素上一起使用v-if和v-for。V-if比v-for优先级更高。
```vue
v-for="user in users" v-if="user.isActive"
// 优化1：
computed: {
    activeUsers() {
        return this.users.filter(user => user.isActive)
    }
}
// 优化2
<ul>
    <template v-for="user in users" :key="user.id">
        <li v-if="user.isActive">
            {{ user.name }}
        </li>
    </template>
</ul>
```
4、为组件样式设置作用域

对于应用来说，样式在顶层 App 组件和布局组件中可以是全局的，但是在其它所有组件中都应该是有作用域的。

这条规则只适用于单文件组件。不一定要使用 scoped attribute。作用域也可以通过 CSS Modules (一个基于 class 的，类似 BEM 的策略) 或者其它的库/约定来实现。
```vue
例子1：
<template>
<button :class="[$style.button, $style.buttonClose]">×</button>
</template>
<!-- 使用 CSS modules -->
<style module>
.button {
    border: none;
    border-radius: 2px;
}
.buttonClose {
    background-color: red;
}
</style>
例子2： 
<template>
<button class="c-Button c-Button--close">×</button>
</template>
<!-- 使用 BEM 约定 -->
<style>
.c-Button {
    border: none;
    border-radius: 2px;
}

.c-Button--close {
    background-color: red;
}
</style>
```
5、私有property名称

使用模块作用域来确保外部无法访问到私有函数。如果无法做到这一点，就始终应该为插件、mixin 等不考虑对外公开 API 的自定义私有 property 使用 $_ 前缀。并附带一个命名空间，以回避和其它作者的冲突 (比如 $_yourPluginName_)

Vue 使用 _ 前缀来定义其自身的私有 property，所以使用相同的前缀 (比如 _update) 有覆写实例 property 的风险。即便你检查确认了 Vue 当前版本没有用到这个 property 名，也不能保证和将来的版本没有冲突。

对于 $ 前缀来说，其在 Vue 生态系统中的目的是暴露给用户的一个特殊的实例 property，所以把它用于私有 property 并不合适。

不过，我们推荐把这两个前缀结合为 $_，作为一个用户定义的私有 property 的约定，以确保不会和 Vue 自身相冲突。

```vue
反面例子： 
const myGreatMixin = {
    // ...
    methods: {
        update() {
            // ...
        }
    }
}
正面例子：
const myGreatMixin = {
    // ...
    methods: {
        $_myGreatMixin_update() {
        // ...
        }
    }
}
// Even better!
const myGreatMixin = {
    // ...
    methods: {
        publicMethod() {
            // ...
            myPrivateFunction()
        }
    }
}
function myPrivateFunction() {
// ...
}
export default myGreatMixin
```
6、单文件组件的文件名应该要么始终是单词大写开头 (PascalCase)，要么始终是横线连接 (kebab-case)。

单词大写开头对于代码编辑器的自动补全最友好，因为这使得我们在 JS(X) 和模板中引用组件的方式尽可能地一致。然而，混用大小写的文件命名方式，有时候会导致其在大小写不敏感的文件系统中出现问题，这也是横线连接命名同样完全可取的原因。
```
components/
|- MyComponent.vue

components/
|- my-component.vue
```
7、基础组建名称：

应用特定样式和约定的基础组件 (也就是展示类的、无逻辑的或无状态的组件) 应该全部以一个特定的前缀开头，比如 Base、App 或 V。
![logo](./images/codeStyle.png ':size=WIDTHxHEIGHT')
```
components/
|- BaseButton.vue
|- BaseTable.vue
|- BaseIcon.vue 

components/
|- AppButton.vue
|- AppTable.vue
|- AppIcon.vue 

components/
|- VButton.vue
|- VTable.vue
|- VIcon.vue
```
8、单例组建名称。只应该拥有单个活跃实例的组件应该以 The 前缀命名，以示其唯一性。

这并不意味着组件只可被用于一个页面，而是每个页面只能使用一次。这些组件永远不接受任何 prop，因为它们是为你的应用所定制的，而不是它们所在的上下文。如果你发现有必要添加 prop，那就表明这实际上是一个可复用的组件，只不过目前在每个页面里只使用一次。
```
components/
|- TheHeading.vue
|- TheSidebar.vue
```
9、紧密耦合的组建名称

与父组件紧密耦合的子组件应该以父组件名作为前缀命名。

如果一个组件只在某个特定父组件的上下文中有意义，那么这层关系应该体现在其命名上。因为编辑器通常会按字母顺序组织文件，这么做也可以把相关联的文件排放在一起。

![logo](./images/codeStyle1.png ':size=WIDTHxHEIGHT')

10、组建命名中单词的顺序

![logo](./images/codeStyle2.png ':size=WIDTHxHEIGHT')

11、完整单词的组建命名 

编辑器中的自动补全已经让书写长命名的代价非常之低了，而其带来的明确性却是非常宝贵的。不常用的缩写尤其应该避免。
```
反面例子： 
components/
|- SdSettings.vue
|- UProfOpts.vue
正面例子：
components/
|- StudentDashboardSettings.vue
|- UserProfileOptions.vue
```
12、prop命名

在声明 prop 的时候，其命名应该始终使用 camelCase，而在模板和 JSX 中应该始终使用 kebab-case。
```
props: {
  greetingText: String
}
<WelcomeMessage greeting-text="hi"/>
```
13、多个 attribute 的元素应该分多行撰写，每个 attribute 一行。

14、指令缩写 (用 : 表示 v-bind:，@ 表示 v-on: 和用 # 表示 v-slot) 应该要么始终使用，要么始终不使用。