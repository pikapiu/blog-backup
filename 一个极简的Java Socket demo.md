# 一个极简的Java Socket BIO demo



## 极简版



最近准备学习一波netty ,但是自己对Java的NIO、BIO、AIO还不熟悉，于是先来熟悉熟悉。

先来康康文档： [All About Sockets](https://docs.oracle.com/javase/tutorial/networking/sockets/index.html)

这文档太啰嗦了。。一时竟不知该从何处下手，随便找个 视频教程，还是个妹子讲的课，这我可就不困了啊，照着就手敲了一遍。

什么@Test @Sl4j 都给我边儿去，main方法和sout才是王道![d_01](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/d_01_1571074352067.png?x-oss-process=style/small)

话不多说，直接上代码和运行结果。

服务端代码：

```java
public static void main(String[] args) {
        final int PORT = 8899;
        ServerSocket serverSocket = null;
        BufferedWriter writer = null;
        try {
            serverSocket = new ServerSocket(PORT);
            System.out.println("服务器已启动！正在监听端口"+PORT);
            while (true){
               Socket socket = serverSocket.accept();
                System.out.println("客户端 "+socket.getPort()+" 已连接");
                BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
                String message = reader.readLine();
                if (message != null){
                    System.out.println("收到一条来自客户端 "+socket.getPort()+" 发送的消息:"+message);
                }
                //加了\n readLine才能生效
                writer.write("你才是" + message + "\n");
                writer.flush(); //清理缓冲区
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(writer != null){
                try {
                    writer.close();
                    System.out.println("服务器挂掉了。。再见");
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
```

客户端代码：

```java

    public static void main(String[] args) {
        final String Host = "127.0.0.1";
        final int Port = 8899;
        BufferedWriter writer = null;
        try {
            Socket socket = new Socket(Host,Port);
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
            BufferedReader console = new BufferedReader(new InputStreamReader(System.in));
            String message = console.readLine();
            writer.write(message+"\n");
            writer.flush();

            String responseMsg = reader.readLine();
            System.out.println("收到了来自服务器的回复：" + responseMsg);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(writer != null){
                try {
                    writer.close();
                    System.out.println("客户端关闭了连接");
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

```

先运行Server代码，此时服务成功启动！：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200310224302.png?x-oss-process=style/small)

再运行客户端代码，此时服务端和客户端连接成功!：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200310224449.png?x-oss-process=style/small)



在客户端发送消息：

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200310224540.png?x-oss-process=style/small)

![](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/20200310224736.png?x-oss-process=style/small)

## 多线程版

[这个教程](https://www.baeldung.com/a-guide-to-java-sockets)是一个多线程的版本，其实就是把服务端的代码中可以复用的部分抽出来单独作为一个内部类，继承Thread，然后在while循环里，每当有一个客户端前来访问，都将开启一个线程专门来处理这个客户端的请求

实际上，上面的极简版本代码，完全也可以多复制几个Client, 然后同时运行，Server端代码会一个个的按照顺序收到客户端的请求并返回对应的结果，while循环永不疲倦，除非断电![d_02](https://pkq-blog-img.oss-cn-hangzhou.aliyuncs.com/d_02_1571074352069.png?x-oss-process=style/small)

## 总结

这便是传说的BIO了，上手了一下，感觉简单的一比，至于底层的原理，无非就是TCP/IP那一套（虽然我也还不太熟悉。。）

接下来会慢慢深入。

typora的PicGo插件不知为何一直失败，上传图片的过程变得不再丝滑了，到处都找不到原因，有些影响心情。。

生活就是这样，永远也不知道下一块巧克力是苦是甜。

















