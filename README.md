# hello_vue
前端学习(vue.js)
## 响应式渲染
vuejs可以通过指令实现视图和数据的解绑，指令将前端对象转换为vue对象，在js中进行操作更方便。遵循mvvm模型，指令支持变量，也支持表达式。
#### 模板语法
#### 条件渲染
* v-if: 条件渲染，如`v-if="isTrue"`
* v-show: 条件隐藏，和v-if有区别，v-show只是修改可见属性

#### 列表渲染(循环)
* v-for: 用于循环的指令，如`v-for="(item, index) in itemList"`, 这里的itemList为vue.itemList中需定义数组变量，例子中的循环返回两个参数，item为具体值，index为索引，也可以只返回值，这时候就不用加小括号

在循环时绑定key，可以加快循环列表在virtual dom中的渲染速度，如在遍历一个jason数组时，设置一个唯一的key，如`data.id`，没有key的情况下，virtual dom在发现数据变动之后会全量比对变动前和变动后的dom：

```html
    <ul>
      <li v-for="(item, i) in list" :key="item.id">
        <input type="checkbox"> {{item.name}}
      </li>
    </ul>
```

* 数组更新检测(vue.js <3.x): push() pop() shift() unshift() splice() sort() reverse()
* 数组元素变动无法检测到的情况：filter(), concat() 和 slice() ,map(),新数组替换旧数组

#### 属性绑定
* v-bind: 可以绑定任意属性，如绑定样式：`v-bind:class="xxx"`，属性可以自己在js中写逻辑，很强大！！！！！这个指令支持缩写，如`v-bind:class`等于`:class`

#### 模型双向绑定
* v-model: 双向绑定模型，用于
#### 事件处理
* v-on: 将对象的监听事件转换为vue对象，如`onClick="xxx()"`可转换为`v-on:click="xxx()"`，这个指令支持简写，`@click="xxx()"`。在事件中，不加括号表示;
* 内联处理器方法-执行函数表达式 handleClick($event)，$event 为事件对象，可使用`$event.target.value`获取对应控件的值，类似this；
* [事件修饰符](https://cn.vuejs.org/v2/guide/events.html)：用于加事件属性，如`@click.self="handleClick"`，修饰符支持链式调用，如`v-on:submit.prevent="xxx()"`，也可以不接处理函数:
    - `.stop`: 阻止控件事件向父控件冒泡传播触发
    - `.prevent`: 阻止控件的默认行为，如超链接<a>的默认行为是点击即跳转
    - `.capture`：
    - `.self`: 只在当前控件选中的时候事件才被触发
    - `.once`: 只触发一次
    - `.passive`: 每次事件产生，浏览器都会去查询一下是否有preventDefault阻止该次事件的默认动作。我们加上passive就是为了告诉浏览器，不用查询了，不存在阻止默认动作的调用。这里一般用在滚动监听，@scroll，@touchmove 。因为滚动监听过程中，移动每个像素都会产生一次事件，每次都使用内核线程查询prevent会使 滑动卡顿。我们通过passive将内核线程查询跳过，可以大大提升滑动的流畅度。

    以下为官网上的例子：

```html
    <!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

#### 模板中插入html
* v-html: 避免转义，直接渲染html，这个指令避免在用户提交场景中使用，xss攻击


### 自定义组件