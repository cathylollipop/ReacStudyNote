# ReactStudyNote

## 3 Flux & Redux

* MVC框架
	* Model 管理数据
	* View 渲染用户界面
	* Controller 接受用户输入，根据输入调用Model逻辑，产生结果交给View渲染输出
	* <img width="341" alt="mvc" src="https://user-images.githubusercontent.com/20292261/37730657-3c3154b4-2d0e-11e8-8c01-1cd05ae44ef9.png">


* Flux - 单向数据流, 更严格的数据流控制
	* <img width="326" alt="flux" src="https://user-images.githubusercontent.com/20292261/37730701-58205ed6-2d0e-11e8-9e15-c524a90bf7aa.png">
	* Dispatcher 处理动作分发，Dispatcher调用回调函数的顺序是无法预期的。
	* Store 一个对象，存储应用状态，接受Dispatcher派发的action并决定是否要更新应用状态。当store状态发生变化的时候，需要通知View作出响应，用消息的方式建立Store和View的联系。Store可以扩展EventEmitter.prototype。
		EventEmitter
        * emit 广播一个特定事件
        * on 挂在这个EventEmitter对象特定事件上的处理函数
        * removeListener 删除挂在这个EventEmitter对象特定事件上的处理函数
	* Action JS对象，代表一个动作的纯数据。2个文件：ActionTypes 和 Actions (action creator) -> 定义了能够产生并派发action对象的函数而不是action对象本身
	* View 显示界面。创建时读取Store的状态来初始化组件内部状态；当Store上状态发生变化时，组建要立刻同步更新内部状态保持一致；View想改变Store状态必须派发action.action.

* Flux 规矩：如果要改变界面，必须改变Store中的状态，如果要改变Store中
的状态，必须派发一个action对象。在Flux中，Store只有get方法，没有set方法，根本可能直接去修改其内部状态，View只能通过get方法获取Store的状态，无法直接去改状态，如果View想要修改Store状态的话，只有派发一个action对象给Dispatcher。
* Flux 不足：
	* 如果两个Store有逻辑依赖关系，比如用Dispatcher的waitFor函数，告诉Dispatcher，先让一个store处理action，只有搞定之后下一个store才能处理这个action。靠register函数的返回值dispatcherToken。
	* 服务器端渲染困难
	* Store封装了数据和处理数据的逻辑

* Redux - Flux框架的一种实现
  基本原则：
    * 唯一数据源 - 应用的状态数据应该只存储在唯一的一个Store上。树形对象。每个组件是树形对象上一部分的数据。（Flux允许多个Store，通过waitFor保持一致性）
    * 保持状态只读 - 不能去直接修改状态，要修改Store的状态，必须要通过派发
一个action对象完成。（同Flux）但是改变状态的方法不是去修改状态上值，而是创建一个新的状态对象返回给Redux，由Redux完成新的状态的组装。
	* 数据改变只能通过Reducer完成 - reducer(state , action）state是当前状态，action是收到的action对象，reducer函数根据state和action产生一个新的对象返回。
      
      


  
