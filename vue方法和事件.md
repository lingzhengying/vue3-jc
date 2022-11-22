data：用于存储数据，数据供el所指定的选择器去使用
methods: 用于存储方法
computed: 计算属性
watch:监视属性  handler(newValue,oldValue)  immediate 立即执行的    deep:true 深度监视
filters: 过滤器
directives: 自定义指令   三个指令： 
                                1.bind(element,binding)      指令与元素成功绑定时(一上来)
                                2. inserted(element,binding) 指令所在元素被插入页面时
                                3.update(element,binding)    指令所在模板被重新解析时
component：配置单文件组件
render: 
props： 传递数据(父传子)
mixins: 混入

脚手架方法：
Vue.use() 定义全局
scoped 让样式在局部生效，防止冲突 写法:<style scoped>
$emit() 触发事件
$off()不写代表解绑全部 $off([])多个解绑 解绑事件
$nextTick 在下一次DOM更新结束后执行其指定的回调  this.$nextTick(回调函数)

vm的生命周期：
1.beforeCreate(将要创建)   无法通过vm访问到data中的数据，methods中配置的方法
2.created(创建完毕)        可以通过vm访问到data中的数据， methods中配置的方法
3.beforeMount(将要挂载)    1.页面呈现的是未经vue编译的DOM结构 2.所有对DOM的操作，最终都不奏效
4.mounted(挂载完毕)        Vue完成模板的解析并把初识的真实DOM元素放入页面后调用 (挂载完毕)  发送Ajax请求，启动定时器，绑定自定义事件，订阅消息等
5.beforeUpdate(将要更新)   数据是新的，但页面是旧的
6.updated(更新完毕)        数据是新的，页面也是新的
7.beforeDestroy(将要销毁)  销毁之前 vm中所有的：data，methods，指令等，都处于可用状态，一般在此阶段：关闭定时器，取消订阅消息，解绑自定义事件等收尾工作
8.destroyed(销毁完毕)      销毁完毕 完全销毁一个实例，清理它与其它实例的连接，解绑它的全部指令及事件监听器(自定义事件)
两个新的生命周期钩子：
                    1.activated(){}     路由组件被激活时触发
                    2.deactivated(){}   路由组件失活时触发
                    3.$nextTick()       在下一次DOM更新结束后执行其指定的回调 

v-bind：单向绑定 简写 ：
v-model: 双向绑定 
v-on:click 绑定事件 简写 @click        @click.prevent：阻止默认行为  @wheel:滚轮事件    @scroll: 滚动+滚轮事件
事件修饰符： 修饰符可以连续写
            prevent：阻止默认行为
            stop：阻止事件冒泡(常用)
            once：事件只触发一次
            capture：使用事件的捕获方式
            self：只有event.target是当前操作的元素时才触发事件
            passive：事件的默认行为立即执行，无需等待事件回调执行完毕
            native: 原生的本来的事件
v-if: 不展示的DOM元素直接被删除  v-if可以和：v-else-if,v-else 一起使用 但不能被打断  template模板：DOM元素不显示 配合v-if 一起使用
v-show：不展示的DOM元素未被删除，仅仅是隐藏掉
v-for: 1.用于展示列表数据   2.语法：v-for="(c,index) in xxx" :key="index"  3.可遍历：数组，字符串，对象，指定次数  :key=""：
v-text: 向其所在的节点中渲染文本内容  与插值语法的区别：v-text会替换掉节点中的内容 {{}} 不会
v-html: 1.向指定节点中渲染包含html结构的内容
        2.与插值语法的区别：1.v-html会替换掉节点中所有的内容,{{}}不会
                         2.v-html可以识别html结构
        3.严重注意：v-html有安全性问题
                   (1).在网站上动态渲染任意html是非常危险的，容易导致xss攻击
                   (2).一定要在可信的内容上使用v-html，永远不要在用户提交的内容上
v-cloak(没有值): 1.本质是一个特殊属性，Vue实例创建完毕并接管容器，会删掉v-cloak的值
                2.使用css配合x-cloak可以解决网速慢时页面展示出{{xxx}}的值
v-once(没有值)：1.v-once所在节点在初次动态渲染后，就视为静态内容了
                2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能
v-pre(没有值): 1.跳过其所在节点的编译过程
               2.可利用它跳过，没有使用指令语法，没有使用插值语法的节点，会加快编译



vue中常用的键盘别名： (可以连续写)两个键盘事件 @keyup:当按钮被松开时触发    @keydown当按钮按下时触发  
                    1.回车 => enter
                    2.删除 => delete
                    3.退出 => esc
                    4.空格 => space
                    5.换行 => tab (必须配合keydown使用)
                    6.上   => up
                    7.下   => down 
                    8.左   => left
                    9.右   => right

el：用于指定为那个容器服务
| 管道符
this.$destroy() 完全销毁一个实例，清理它与其它实例的连接，解绑它的全部指令及事件监听器(自定义事件)
1.局部注册：靠new Vue的时候传入components({})选项
2.全局注册：靠Vue.component（'组件名'，组件词）
vue inspect > output.js 查看vue配置

Vuex
modules:{} vuex模块化要写入里面
namespaced:true,开启命名空间

路由
<router-view></router-view> 指定组件的呈现位置
<router-link replace to="/"></router-link>  Vue中借助router-link标签实现路由的切换 replace 隐私模式   默认push
 routes:[
        {
            path:'/about',
            component:About,
            children:[
                 path:'news',
                 component:News,  
            ]
        },
        ] 父路由
children:[]子路由
$route.query.xxx 接收参数
<keep-alive include="Mews"><router-view></router-view></keep-alive> 组件缓存 include="Mews" 缓存指定组件名
meta:{isAuth:true},//配置路由权限
路由守卫：
        前置路由守卫：
                    router.beforeEach((to,from,next) => {} 全局前置路由守卫-初始化之前被调用-每次路由切换之前被调用 to到哪去  from从哪来  next放行
        后置路由守卫：
                    router.afterEach((to,from) => {}       全局后置路由守卫-初始化之前被调用-每次路由切换之后被调用 to到哪去  from从哪来
        独享路由守卫： 
                    beforeEnter:(to,from,next) => {}       只有前置独享路由守卫，没有后置独享路由守卫
        组件内守卫：
                    beforeRouteEnter(to,from,next){...}    进入守卫，通过路由规则，进入该组件时被调用
                    beforeRouteLeave (to, from,next) {...}      离开守卫，通过路由规则，离开该组件时被调用


内置关系：VueComponent.prototype.__proto__ === Vue.prototype


css样式
.v-enter-active 来的样式
v-leave-active 离开的样式


vue3:
    setup:组件中所用到的，数组，方法等，均配置在setup里面
    watchEffect: 
    生命周期钩子：
                beforeCreate(){}
                created(){}
                beforeMount(){}
                mounted(){}
                beforeUpdate(){}
                updated(){}
                beforeUnmount(){}
                unmounted(){}
   组合式api生命周期钩子：
                        onBeforeMount(()=>{})
                        onMounted(()=>{})
                        onBeforeUpdate(()=>{})
                        onUpdated(()=>{})
                        onBeforeUnmount(()=>{})
                        onUnmounted(()=>{})