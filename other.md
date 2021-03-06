## 其他
### 为什么要使用vuex进行状态管理？
+ 组件之间通信的成本增高。React 采用了单项数据流，但是现实中组件的通信往往不是单向的。子组件想要改变父组件的状态的话（逆向），就只能通过父组件传递 callback 作为 props 这种方式来进行。但是随着组件嵌套层数的增加，就不得不把 callback 一级级地传递下去，这样做的成本显然是非常高的。
    
+ 数据流变得模糊。也正是因为上文提出的组件间通信的问题，传递 callback 使得子组件能够”改变“父组件的 state。但是这样一来，React 的单项数据流也就在一定程度上被破坏了，数据流也因而变得非常模糊复杂。
    
+ 组件变得臃肿。有的时候几个组件共用一个 state，这时候就不得不把这个 state 提升到这几个组件的共同父级组件。在这种情况下，组件所持有的一些特定状态往往很不 make sense，而只是为了组件间通信而强行加上去，导致某些组件变得十分臃肿。

### DNS 查询过程？
+ 浏览器检查域名是否在缓存当中（要查看 Chrome 当中的缓存， 打开 `chrome://net-internals/#dns`）。
+ 如果缓存中没有，就去调用 gethostbyname 库函数（操作系统不同函数也不同）进行查询。gethostbyname 函数在试图进行DNS解析之前首先检查域名是否在`本地 Hosts`里，Hosts 的位置 不同的操作系统有所不同
+ 它将会向 DNS 服务器发送一条 DNS 查询请求。DNS 服务器是由网络通信栈提供的，通常是本地路由器或者 ISP 的缓存 DNS 服务器。
	- 查询本地 DNS 服务器
        - 如果 DNS 服务器和我们的主机在同一个子网内，系统会按照下面的 ARP 过程对 DNS 服务器进行 ARP查询
        - 如果 DNS 服务器和我们的主机在不同的子网，系统会按照下面的 ARP 过程对默认网关进行查询