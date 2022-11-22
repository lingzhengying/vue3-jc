vue脚手架创建步骤：
                1.执行npm install -g @vue/cli命令
                2.切换到需要创建的项目执行 vue create xxx  xxx是文件名 cd Desktop 切换到桌面
                3.


01.初识Vue:
        1.想让vue工作，必须创建一个vue实例，且要传入一个配置对象
        2.root容器里的代码必须符合html规范，只不过混入了一些特殊的vue语法
        3.root容器里的代码被称为 vue模板
        4.vue实例和容器是一一对应的
        5.真实开发中只有一个vue实例，并且还会配合组件一起使用
        6.{{xxx}} 中的xxx要js表达式，且xxx可以自动读取到data中的所有配件
        7.一但data中的数据发生改变，那么页面中用到该数据的地方也会自动更新

        js表达式 和 js代码：
                            1.表达式：一个表达式会产生一个代值，可以放在任何一个需要值的地方
                                    1.a
                                    2.a + b
                                    3.demo(0)
                                    4.x === y ? 'a' : 'b'
                            2.js语句：
                                    1.if(){}
                                    2.for(){}

02.vue模板语法有两大类：
                    1.插值语法：
                            功能.用于标签体内容
                            写法：{{xxx}} xxx是js表达式，且可以直接读取到data中的所有内容
                    2.指令语法：
                            功能：用于解析标签(标签属性，标签体内容，绑定事件)
                            举例：v-bind:href="xxx" 简写 :href="xxx" xxx要写js表达式且可以直接读取到data中的所有内容

03.两种数据绑定：
              1.单向绑定(v-bind 简写 : ): 数据只能从data流向页面 
              2.双向绑定(v-model): 数据不仅能从data流向页面，还可以从页面流向data 一般都应用在表单元素上

 MVVM模型： M：模型 对于data里的数据
            V： 试图 模板
            VM: 视图模型 vue实例对象

06.数据代理：通过一个对象代理对另一个对象中属性的操作(读/写)
        1.vue中的数据代理：通过vm对象来代理data对象中属性的操作(读/写)
        2.vue中数据代理的好处：更加方便的操作data中的数据
        3.基本原理： 
                  1.通过Object.defineProperty()把data对象中所有的属性添加到vm上
                  2.为每一个添加搭配vm上的属性，都指定一个getter/setter
                  3.在getter/setter内部去操作(读/写)data中对应的属性

07.事件处理：
            1.使用v-on:xxx 或@xxx 绑定事件，其中xxx是事件名
            2.事件的回调需要配置在methods对象中，最终会在vm上
            3.methods中配置的函数，不要使用箭头函数，否则this就不是vm了
            4.methods中配置的函数，都是被vue所管理的函数，this的指向是vm 或 组件实例对象
            5.@click='demo' 和 @click'demo($event)' 效果一样，但后者可以传参

08.计算属性：
            1.定义：要用的属性不存在，要通过已有属性计算的来
            2.原理：底层借助了Object.defineProperty方法提供的getter和setter
            3.get什么时候执行：
                            1.初次读取时会执行一次
                            2.当依赖的数据发生变化时会再次被调用
            
  监视属性：
            1.当被监视的属性变化时，回调函数自动调用，进行相关操作
            2.监视的属性必须存在，才能进行监视
            3.监视的两种方法：
                            (1)new value时传入watch配置
                            (2)通过vm.$watch监视
  深度监视：
            1.vue中的watch默认不监视对象内部的改变(一层)
            2.配置deep:true可以监测内部值得改变(多层)
  computed和watch的区别：
                       1.computed能完成的watch都能完成
                       2.watch能完成的，computer不一定能完成 例如：watch可以进行异步操作

09.绑定样式：
           1.class样式 写法 class='xxx' xxx可以是字符串 对象 数组
           2.style写法 （1）:style='{fontSize: xxx}' xxx是动态值 
                         （2）:style='[a,b]' a,b是样式对象

11-列表渲染：
        key: 1.虚拟DOM的作用：
                            1.key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据[新数据] 生成 [新的虚拟DOM]
                              随后vue进行[新虚拟DOM] 与 [就虚拟DOM的差异比较]
             2.对比规则：
                        1.旧虚拟DOM中找到了与新虚拟DOM相同的key
                                                            1.若虚拟DOM中内容没变，直接使用之前的真实DOM
                                                            2.若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM
                        2.旧虚拟DOM中未找到与新虚拟DOM相同的key
                                                            1.创建新的真实DOM，随后渲染到页面
             3.用index作为key可能会引发的问题：
                                           1.落对数据进行：逆序添加，逆序删除等破坏顺序操作，会产生没有必要的真实DOM更新 ===> 界面效果没问题，但效率低
                                           2.如果结构中还包含输入类的DOM，会产生错误DOM ===> 界面有问题
             4.界面如何选择key：
                              1.最好使用每条数据的唯一标识作为key，比如id，手机号，身份证号，学号等唯一标识
                              2.如果不存在对数据的逆序添加，逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的
        
        vue监视数据的原理:
                        1.vue会监视data中所有层次的数据
                        2.如何监视对象中的数据：
                                             通过setter实现监视，且要在new Vue时传入要检测的数据
                                             1.对象中后追加的属性，vue默认不做响应式处理
                                             2.如需给后添加的属性做响应式请使用如下API：
                                                Vue.set(target,propertyName/index,value)或
                                                vm.$set(target,propertyName/index,value)

                        3.如何检测数组中的数据？
                                        通过包裹数组更新元素的方法实现，本质就是为了做两件事
                                        1.调用原生对应的方法对数组进行更新
                                        2.重新解析模板，进而更新页面
                        4.在vue修改数组中的某个元素一定要用如下方法：
                          1.使用这些API：push(), pop(), shift(), unshift(), splice(), sort(), reverse()
                          2.Vue.set() 或  vm.$set()
                        
                特别注意：Vue.set() 和 vm.$set 不能给vm 或 避免的根数据对象 添加属性！！！

12.收集表单数据：
    若：<input type="text"/> 则v-model收集的是value值，用户输入的就是value值
    若：<input type="radio"/> 则v-model收集的是value值，且要给标签配置value值
    若：<input type="checkbox"/> 
                             1.没有配置input的value属性，那么收集的就是check（勾选 or 为勾选，布尔值）
                             2.配置input的value属性：
                              (1).v-model的初始值是非数组，那么收集的就是checked 勾选 or 为勾选，布尔值）
                              (2).v-model的初始值是数组，那么收集的就是value组成的数组
                         v-model的三个修饰符：
                                        1.  lazy：失去焦点再收集数据
                                        2.  number：输入字符串转化为有效的数据
                                        3.  trim： 输入收尾空格过滤 

13.过滤器：
        定义：对要显示的数据进行特定格式化后再显示(用于显示一些简单逻辑处理)
        语法：
            1.注册过滤器:Vue.filter(name,callback) 或 new Vue(filters:{})
            2.使用过滤器:{{xxx | 过滤器名}} 或 v-bind:属性 = "xxx | 过滤器名"
        备注：
            1.过滤器也可以接收额外的参数，多个过滤器也可以串联
            2.并没有改变原数组的数据，是产生新的对应的数据

15.自定义指令：
             一.定义语法：
                       1.局部指令：
                                new Vue({
                                   directives:{指令名：配置对象}  或   new Vue({
                                })                                     directives{指令名：回调函数} 
                                                                      })
                        2.全局指令：
                                Vue.directives(指令名，配置对象) 或  Vue.directives(指令名,回调函数)
                二.配置对象中常用的三个回调：
                                          1.bind(element,binding)      指令与元素成功绑定时(一上来)
                                          2. inserted(element,binding) 指令所在元素被插入页面时
                                          3.update(element,binding)    指令所在模板被重新解析时
                三.备注：
                        1.指令定义时不加v-,但使用时要加v-
                        2.指令名如果是对个单词，需使用kebab-case命名方式，不要用camelCase

16.生命周期钩子：
              1.又名：生命周期回调函数，生命周期函数，生命周期钩子
              2.是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数
              3.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的
              3.生命周期函数中的this指向是vm 或 组件实例对象

17.非单文件组件：
        Vue中使用组件的三大步骤:
                1.定义组件(创建组件)
                2.注册组件
                3.使用组件

                一、如何定义一个组件
                使用Vue.extend(options)创建 其中options和new.Vue(options)时传入的options几乎一样，但也有点区别
                区别如下：
                1.el不要写，因为最终所有的组件都要经过一个vm的管理，有vm中的el决定服务那个容器
                2.data必须写成函数，避免重复使用时，数据存在引用关系
                备注：使用template可以使用配置组件结构

                二、如何注册组件？
                1.局部注册：靠new Vue的时候传入components选项
                2.全局注册：靠Vue.component（'组件名'，组件词）

                三、编写组件标签
                如：<school></school>
        几个注意点：
                  1.关于组件名：
                             一个单词组成：
                                      第一种写法(首字母小写) school
                                      第二种写法(首字母大写) School
                             多个单词组成：
                                      第一种写法：(kebab-case)命名：my-school
                                      第二种写法：(CamelCase):MySchool(需要脚手架支持)
                             备注：
                                 (1).组件名尽可能回避HTML中已有的元素名称.例如：H2,h2都不行
                                 (2).可以使用name配置项指定组件在开发者工具中呈现的名字
                  2.关于组件标签：
                            第一种写法：<school></school>
                            第二种写法：<school> //需要使用脚手架
                  3.一个简写方式：
                            const school = Vue.extend(options) 可简写为：const school = options
        关于VueComponent方法：
                  1.school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extent生成的
                  2.我们只需要写<school></school>或</school>.Vue解析时会帮我们创建school组件的实例对象，既Vue帮我们执行的:new VueComponent(options)
                  3.特别注意：每次调用Vue.extend,返回的都是一个全新的VueComponent！！！
                  4.关于this指向：
                    (1).组件的配置：
                           data函数，methods中的函数，watch中的函数，computed中的函数，它们的this均是(VueComponent) vc
                    (2).new Vue(options)配置中：
                           data函数，methods中的函数，watch中的函数，computed中的函数，它们的this均是(Vue实例对象) vm


                                                Vue-cli
关于不同版本的vue：
                1.vue.js与vue.runtime.xxx.js的区别
                  (1).vue.js是完整版的vue 包含：核心功能+模板解析器
                  (2).vue.runtime.xxx.js是运行版的vue.只包含：核心功能：没有模板解析器
                2.只因为vue.runtime.xxx.js没有模板解析器，所有不能使用template配置项，需要使用
                  render函数接收到的createElement函数去指定具体内容


vue打包工具：
           webpack：npm create +项目名字   npm run serve
              vite: 1.npm init vite-app + 项目名字
                    2.npm i
                    3.npm run dev


                   