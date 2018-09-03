---
title: 'react生命周期 '
date: 2018-08-31 14:47:29
tags: React
---
### React生命周期包含哪些
 #### getDefaultProps
  对于每个组件实例来讲，这个方法只会调用一次，该组件类的所有后续应用，getDefaultPops 
  将不会再被调用，其返回的对象可以用于设置默认的 props(properties的缩写) 值。
 #### getInitialState
 对于组件的每个实例来说，这个方法的调用有且只有一次，用来初始化每个实例的 state，在这个方法里，可以访问组件的 props。每一个React组件都有自己的 state，
 其与 props 的区别在于 state只存在组件的内部，props 在所有实例中共享
 getDefaultProps与getInitialState的区别
  getDefaultPops 是对于组件类来说只调用一次，后续该类的应用都不会被调用，
  而 getInitialState 是对于每个组件实例来讲都会调用，并且只调一次
 #### componentWillMount
  该方法在首次渲染之前调用，也是再 render 方法调用之前修改 state 的最后一次机会
 #### render
 render方法创建一个虚拟的DOM，用来表示组件的输出，对于一个组件来讲，render方法是唯一一个必须方法。
 ##### redner方法要满足：
 . 只要通过this.props和this.state访问数据，而且不能修改
 . 可以返回null, false 或者任何React组件
 . 只能出现一个顶级组件，不能返回一组元素
 . 不能改变组件的状态 
 . 不能修改DOM的输出
 render方法回来的结果并不是真正的DOM元素，而是一个虚拟的表现，类似于一个DOM tree的结构的对象。
 #### componentDidMount
 该方法不会在服务端被渲染的过程中调用。该方法被调用时，已经渲染出真实的 DOM，可以再该方法中通过 this.getDOMNode()访问到真实的 DOM(推荐使用 ReactDOM.findDOMNode())
 #### componentWillReceiveProps
 组件的props属性可以通过父组件来更改，这时候componentWillReceivePros将会被调用，这个时候可以在这个方法里使用this.setState更新state，以触发render方法重新渲染组件。
 #### shouldComponentUpdate
 如果你确定组件的 props 或者 state 的改变不需要重新渲染，可以通过在这个方法里通过返回 false 来阻止组件的重新渲染，返回false则不会执行 render 以及后面的 componentWillUpdate，componentDidUpdate 方法。
 #### componentWillUpdate
这个方法和 componentWillMount 类似，在组件接收到了新的 props 或者 state 即将进行重新渲染前，componentWillUpdate(object nextProps, object nextState) 会被调用，注意不要在此方面里再去更新 props 或者 state
 #### componentDidUpdate
 这个方法和 componentDidMount 类似，在组件重新被渲染之后，componentDidUpdate(object prevProps, object prevState) 会被调用。可以在这里访问并修改 DOM
 #### componentWillUnmount
 每当React使用完一个组件，这个组件必须从 DOM 中卸载后被销毁，此时 componentWillUnmout 会被执行，完成所有的清理和销毁工作，在 componentDidMount 中添加的任务都需要再该方法中撤销，如创建的定时器或事件监听器
 ### 一个React 组件的生命周期分为三个部分:实例化，存在期和销毁时。
 ### 实例化
 ##### 当组件在客户端被实例化，第一次被创建时候，会依次调用以下方法
 - getDefaultProps
 - getInitialState
 - componentWillMont
 - render
 - componentDidMount
 ##### 当组件在服务端被实例化，首次被创建时，会依次调用以下方法
 - getDefaultProps
 - getInitialState
 - componentWillMont
 - render 
 - componentDidMount (不会在服务端被渲染的过程调用) 
 ##### 每次修改state，都会重新渲染组件，实例化后通过state更新组件，回依次调用以下方法
 - shouldComponentUpdate
 - componentWillUpdate
 - render
 - componentDidUpdate
 不要直接去修改this.state,通过this.setState去修改
 ### 存在期
 ##### 此时组件已经渲染好并且用户可以与他进行交互，这时候会看到下面的方法会被调用
 - componentWillReceiveProps
 - shouldComponentUpdate
 - componentWillUpdate
 - render
 - componentDidUpdate
 ### 销毁时
 ##### 当再次装载组建时，以下方法将会被调用：
 - getInitialState
 - componentWillMount
 - render
 - componentDidMount