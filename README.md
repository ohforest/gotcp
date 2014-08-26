一个TCP Server的小例子.

测试:

服务器接受了5000个TCP长连接，对于每个连接分别由goroutine处理，

每个连接分配1K缓冲区接收数据，当数据大于1K时会缓冲区自动扩容。

平均每个连接耗费大概20K内存，总共100M多一点。


一般认为系统底层默认的socket读写缓冲区各8K，当然每个系统的设置不一样，

也可以手动更改这个缓冲区大小。

另外golang现在的GC很慢，非常慢，客户端断开连接后，服务器需要等很久才

释放socket占用的内存。


####下面这个chatserver是在gotcp的基础上写的，已经用于生产环境：https://github.com/gansidui/chatserver
