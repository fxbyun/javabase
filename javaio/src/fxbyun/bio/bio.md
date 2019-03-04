概念  
BIO ，全称 Block-IO ，是一种阻塞 + 同步的通信模式。
是一个比较传统的通信方式，模式简单，使用方便。但并发处理能力低，通信耗时，依赖网速。

原理  
服务器通过一个 Acceptor 线程，负责监听客户端请求和为每个客户端创建一个新的线程进行链路处理。典型的一请求一应答模式。
若客户端数量增多，频繁地创建和销毁线程会给服务器打开很大的压力。后改良为用线程池的方式代替新增线程，被称为伪异步 IO 。

关键代码：
~~~
while (true) {  
    socket = server.accept();  // 服务器监听：阻塞，等待Client请求 使用这个方法  
    executor.execute(serverHandler);
}

BufferedReader reader  //读取客户端消息
PrintWriter writer     //发送消息
~~~

小结  
BIO 模型中，通过 Socket 和 ServerSocket 实现套接字通道的通信。阻塞，同步，建立连接耗时。
