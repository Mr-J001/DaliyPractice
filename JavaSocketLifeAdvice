人生建议小程序

服务器端代码
import java.io.IOException;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;
 
public class severSocket {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		DailyAdviceServer server = new DailyAdviceServer();
		server.go();
	}
}
class DailyAdviceServer{
	String[] adviceList = {"早睡早起身体好","每天吃早餐","今天很美好","青春就是用来挥霍的","做你害怕做的事情,然后你会发现,不过如此",
  "永远留住30%的神秘","不知道做什么，就先健身吧！","千万千万不要自欺欺人","听从你自己的节奏。"};
	public void go() {	
		try {
			ServerSocket serverSock =new ServerSocket(5222);//监听客户端对该机器在端口5222的要求
			while(true) {
				Socket sock = serverSock.accept();//该方法会等到接收到要求继续执行下面程序
				PrintWriter writer =new PrintWriter(sock.getOutputStream());//建立输出链接
				String advice=getAdvice(); //选择输出内容
				writer.print(advice);
				writer.close();//输出后链接关闭
				System.out.print(advice);			
			}			
		} catch (IOException e) {
			// TODO: handle exception
			e.printStackTrace();
		}			
	}
	public String getAdvice() {
		// TODO Auto-generated method stub
		int random = (int)(Math.random()*adviceList.length);
		return adviceList[random];
	}
}

客户端代码
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.Socket;
 
public class chatSocket {
	public static void main(String[] args)throws Exception {
		// TODO Auto-generated method stub		
		DailyClient client = new DailyClient();
		client.go();
	}
}
class DailyClient{
	public void go() {
		try {
			Socket chatSk = new Socket("127.0.0.1",5222);//链接端口5222
			InputStreamReader streamReader = new InputStreamReader(chatSk.getInputStream());//建立字节流
			BufferedReader reader = new BufferedReader(streamReader);//建立缓冲区
			String advice= reader.readLine();		
			System.out.println("Today you should: "+advice);
			reader.close();					
		} catch (IOException e) {
			// TODO: handle exception
			e.printStackTrace();
		}
	}
}

原文链接_我的博客：https://blog.csdn.net/sinat_28809019/article/details/103738835
