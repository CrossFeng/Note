# Java Socket 编程

## 使用Socket实现TCP

参考

[Java Socket 基础]: http://blog.csdn.net/yangyi22/article/details/7523968
[非阻塞方式实现Socket]: http://blog.csdn.net/chjttony/article/details/7181427
[Java Socket编程 标准范例（多线程）]: http://blog.csdn.net/benweizhu/article/details/6615542/
[JAVA 通过 Socket 实现 TCP 编程]: http://blog.csdn.net/qq_23473123/article/details/51461894

TCP 服务器端

```java
//TCP Server
package javaSocket;

import java.io.DataInputStream;
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
public class TCPServer {
	public static void main(String[] args) throws IOException {
		ServerSocket ss = new ServerSocket(3336);
		while(true){
			Socket s = ss.accept();
			DataInputStream dis = new DataInputStream(s.getInputStream());
			System.out.println(dis.readUTF());
			System.out.println("Hello client "+s.getInetAddress()+" :"+s.getPort());
			dis.close();
			s.close();
		}
	}
}
```

TCP 客户端

```java
public class TCPClient {
	public static void main(String[] args) throws UnknownHostException, IOException {
		Socket s = new Socket("127.0.0.1",3336);
		OutputStream out = s.getOutputStream();
		DataOutputStream dos = new DataOutputStream(out);
		dos.writeUTF("Hello Server");
		dos.flush();
		dos.close();
		s.close();
	}
}
```

当然，为了 TCP可以处理多个客户端的请求，需要为每一个客户端分配一个线程

```java
Socket client = s.accept();
new ClientThread(client,F_DIR).start();
```

## ?对于实现双向的通信 如果关闭某个流那么 会造成 套接字关闭

```java
//Server
package javaSocket;

import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class TCPServer {
	public static void main(String[] args) throws IOException {
		@SuppressWarnings("resource")
		ServerSocket ss = new ServerSocket(3336);
		Socket s = ss.accept();
		DataInputStream dis = new DataInputStream(s.getInputStream());
		System.out.println(dis.readUTF());
		//System.out.println("Hello client "+s.getInetAddress()+" :"+s.getPort());
		OutputStream out = s.getOutputStream();
		DataOutputStream dos = new DataOutputStream(out);
		dos.writeUTF("Hello Client");
		
		dos.flush();
		dis.close();
		s.close();
	}
}
//Client
package javaSocket;

import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.net.Socket;
import java.net.UnknownHostException;

public class TCPClient {
	public static void main(String[] args) throws UnknownHostException, IOException {
		Socket s = new Socket("127.0.0.1",3336);
		OutputStream out = s.getOutputStream();
		DataOutputStream dos = new DataOutputStream(out);
		dos.writeUTF("Hello Server");
		dos.flush();
      	 //dos.close  如果不注释掉，那么会造成:
      /* Exception in thread "main" java.net.SocketException: Socket is closed
		at java.net.Socket.getInputStream(Socket.java:903)
		at javaSocket.TCPClient.main(TCPClient.java:18) */
		DataInputStream dis = new DataInputStream(s.getInputStream());
		System.out.println(dis.readUTF());
		dos.close();
		s.close();
	}
}
```



## 实现FTP协议

命令端口 21 数据端口20
主动模式 被动模式

命令格式 "command\r\n"