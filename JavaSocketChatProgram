服务端

package demo04;
 
import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.net.ServerSocket;
import java.net.Socket;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.ScrollPaneConstants;
 
public class ownServer {
 
	public static void main(String[] args) {
		// TODO Auto-generated method stub
 
		new Server().launch();
	}
}
class Server{
	JFrame frame;
	JTextArea  taArea;
	JTextField tfField;
	JButton sbButton;
	DataInputStream read ;
	DataOutputStream write;
	ServerSocket scServerSocket; 
	Socket socket;
	
	public void launch() {
		CreateUI();
		CreateNetWork();
		new ServerWrite().start();
		new ServerRead().start();
	}	
	public void CreateUI() {
		frame = new JFrame("MM Server");
		JPanel Panle = new JPanel();
		taArea = new JTextArea(15,25);
		taArea.setLineWrap(true);
		taArea.setWrapStyleWord(true);
		taArea.setEditable(true);
		JScrollPane qScroller=newJScrollPane(taArea); 
 qScroller.setVerticalScrollBarPolicy(ScrollPaneConstants.VERTICAL_SCROLLBAR_ALWAYS);                 
 qScroller.setHorizontalScrollBarPolicy(ScrollPaneConstants.HORIZONTAL_SCROLLBAR_ALWAYS);
		tfField = new JTextField(20);
		sbButton = new JButton("发送");
		Panle.add(qScroller);
		Panle.add(tfField);
		Panle.add(sbButton);		
        frame.getContentPane().add(BorderLayout.CENTER,Panle);
        frame.setSize(400,400);
        frame.setVisible(true);	
	}
	public void close()
	{
		try
		{
			write.close();
			read.close();
			socket.close();
			scServerSocket.close();
		}
		catch (Exception e)
		{
			System.exit(-1);
		}
	}	
	public void CreateNetWork() {	
			
		try {
		    scServerSocket =new ServerSocket(7780);
			socket= scServerSocket.accept();
			read = new DataInputStream(socket.getInputStream());
			write = new DataOutputStream(socket.getOutputStream());				
			System.out.print("网络连接");
		
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();
		}	
	}
	class ServerRead extends Thread{
		public void run() {	
			while (true) {
			  try {
					String message = read.readUTF();
					taArea.append("对方："+message+ "\n");
			} catch (Exception e1) {
				// TODO: handle exception
				JOptionPane.showMessageDialog(taArea,  "提示: 服务端已经断开连接");
				
				//e.printStackTrace();
				//System.exit(-1);
				return ;
			}				
			}
		}
	}
class ServerWrite extends Thread{
		
		public void run() {
			tfField.addActionListener(new ServerListen());
			sbButton.addActionListener(new ServerListen());
		}
	}
	class ServerListen implements ActionListener{
		@Override
		public void actionPerformed(ActionEvent e) {
			try {
				String str = tfField.getText();
				tfField.setText("");
				taArea.append("我: " + str + "\n");
				write.writeUTF(str);
				
			} catch (Exception e2) {
				// TODO: handle exception
				e2.printStackTrace();
			}
		}	
	}	
}

客户端
package demo04;
 
import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.io.DataInputStream;
import java.io.DataOutputStream;
 
import java.net.Socket;
 
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.ScrollPaneConstants;
 
public class ownClient {
 
	public static void main(String[] args) {
		// TODO Auto-generated method stub
	new Client().launch();
	}
}
class Client{
	JTextArea  taArea;
	JTextField tfField;
	JButton sbButton;
	DataInputStream read = null;
	DataOutputStream write = null;
	Socket socket;
	public void launch() {
		CreateUI();
		CreatNetWork();
		new ClientRead().start();;
		new ClientWrite().start();;
	}
	public void CreateUI() {
		JFrame frame = new JFrame("MM Client");
		JPanel Panle = new JPanel();
		taArea = new JTextArea(15,25);
		taArea.setLineWrap(true);
		taArea.setWrapStyleWord(true);
		taArea.setEditable(true);
		JScrollPane qScroller = new JScrollPane(taArea);
 qScroller.setVerticalScrollBarPolicy(ScrollPaneConstants.VERTICAL_SCROLLBAR_ALWAYS);
 qScroller.setHorizontalScrollBarPolicy(ScrollPaneConstants.HORIZONTAL_SCROLLBAR_ALWAYS);
		
		tfField = new JTextField(20);
		sbButton = new JButton("发送");
		
		Panle.add(qScroller);
		Panle.add(tfField);
		Panle.add(sbButton);	
				
        frame.getContentPane().add(BorderLayout.CENTER,Panle);
        frame.setSize(400,400);
        frame.setVisible(true);
	}
	public void CreatNetWork() {
		// TODO Auto-generated method stub
		try {
			socket = new Socket("127.0.0.1",7780);
			write = new DataOutputStream(socket.getOutputStream());
			read = new DataInputStream(socket.getInputStream());
			System.out.print("已建立网络连接");
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();
		}
	}
	class ClientRead extends Thread{
		
		public void run() {			
			while (true) {
			  try {
					String message= read.readUTF();
					taArea.append("对方："+message+ "\n");			
			} catch (Exception e1) {
				// TODO: handle exception
				JOptionPane.showMessageDialog(taArea,  "提示: 客户端已经断开连接");
				
				//e.printStackTrace();
				//System.exit(-1);
				return ;
			}						
			}
		}
	}	
	class ClientWrite  extends Thread{
		
		public void run() {
			
			tfField.addActionListener(new ClientListen());
			sbButton.addActionListener(new ClientListen());		
		}
	}	
	class ClientListen implements ActionListener{
		@Override
		public void actionPerformed(ActionEvent e) {
			try {			
				String str = tfField.getText();
				tfField.setText("");
				taArea.append("我: " + str + "\n");
				write.writeUTF(str);
				
			} catch (Exception e2) {
				// TODO: handle exception
				e2.printStackTrace();
			}
		}	
	}	
}



