#TCP/IP

TCP/IP提供一种`面向连接的`，`可靠的`字节流服务。

面向连接意味着两个使用TCP的应用在彼此交换数据之前必须建立一个tcp连接

在一个tcp连接中仅有两方进行彼此通信，广播和多播不能用于tcp

#####tcp将使用下列方式提供可靠性
	－应用数据被分割成tcp认为最合适大小的的数据块，由tcp传递给ip的信息单位被称为报文段或者段
    －当tcp发出一个段后，将启动一个定时器，等待目的段确认收到了这个报文段，如果不能收到确认将会重发。
    －当tcp收到发自tcp连接另一端的数据，它将回复一个确认。这个确认不是立即发送，而是要延时几分之一秒（为什么会要延时）
    －tcp将保持它首部和数据的检验和，这是一个端到端的检验和，目的是检测数据在传输过程中是否发生了变化，如果检验和有差错，tcp将丢弃这个报文段并不确认收到此报文段，希望对端超时重发。
    －既然tcp报文段使用ip数据报来传输，而ip数据报的到达可能会失序，因此收到的tcp报文段也会失序，如果必要tcp将对收到的数据进行排序。
    －tcp会丢弃重复的数据。（如何判断数据是否重复）
    －tcp还能进行流量控制，tcp连接的每一方都有固定大小的缓冲空间，tcp接收端只允许另一端发送接收端缓冲区数据所能接纳的数据。防止缓冲区溢出。（什么是缓冲区溢出）

每个tcp段都包含源端口和目的端口号用于寻找发端和收端应用进程。这两个值加上ip首部的源ip和目的ip地址唯一确定一个tcp连接。

#####tcp首部

![tcp首部数据格式](http://s11.sinaimg.cn/mw690/0064m8yBgy6Sov6aPrQba&690)

tcp数据格式，如果不计算任选字段，通常是20字节

**序号**用来标识从发端到收端的数据字节流，表示这个报文段中的地多少个数据字节。如果将字节流看作两个应用程序之间的单向流动，则tcp用序号对每个字节进行计数，从０开始到２^32-1后又从０开始。

