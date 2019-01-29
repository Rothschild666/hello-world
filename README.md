# hello-world
just another repository
package xr;//匿名内部类的运用
interface Animal
{
	void shout();
	}
public class Test {
	public static void main(String[] args) {
		getanimal(new Animal() {//这个就是+
			
			@Override
			public void shout() {
				// TODO Auto-generated method stub
				System.out.println("miaomiao");
			}
		});
	}
	public static void getanimal(Animal animal)
	{
		animal.shout();
	}
}

package xr;//多态的运用
interface Animal
{
	void shout();
	}
class Cat implements Animal
{
	public void shout()
	{
		System.out.println("miaomiao");
	}}
class Dog implements Animal
{
	public void shout()
	{
		System.out.println("wangwang");
	}}
public class Test {
	public static void main(String[] args) {
		Animal animal1 = new Cat();//用父类对象引用子类对象
		Animal animal2 = new Dog();
		getanimal(animal1);
		getanimal(animal2);
	}
	public static void getanimal(Animal animal)//创建一个方法然后传递过来的父对象再根据父对象引用的子对象来输出相应的值
	{
		animal.shout();
	}
}

package xr;//用super调用父类的成员和方法
class Animal
{
	String name;
	public void getAnimal()
	{
		System.out.println("我是一个动物！");
	}}
class Dog extends Animal
{
	public Dog()
	{
		super.getAnimal();//这就是调用父类的方法的用法
	}}
public class Test {
	public static void main(String[] args) {
		Dog dog = new Dog();
	}
}

package xr;//方法内部类的运用
class Outer
{
	private static int num=4;
	public void getshow()
	{
		class Inner//在方法中定义一个方法内部类
		{
			public void show()
			{
				System.out.println("num="+num);
			}
		}
		Inner inner = new Inner();//只能在此方法中方法内部类创建对象
		inner.show();
	}
}
public class Test {
	public static void main(String[] args) {
		Outer outer = new Outer();
		outer.getshow();
	}
}

package xr;//静态内部类的应用
class Outer
{
	private static int num=4;
	static class Inner//静态内部类的定义
	{ 
		
		public void show()
		{
			System.out.println("num="+num);//静态内部类的方法之内引用静态外部变量
		}
	}
	public void getshow()
	{
		Inner inner = new Inner();
		inner.show();
	}
}
public class Test {
	public static void main(String[] args) {
		Outer outer = new Outer();
		outer.getshow();
		Outer.Inner oInner = new Outer.Inner();//在外部创建静态内部类对象的格式
		oInner.show();
	}
}

package xr;//内部类的应用
class Outer
{
	private int num=4;//外部类用private私有化外部变量
	class Inner
	{
		public void show()
		{
			System.out.println("num="+num);//内部类方法可以调用外部变量
		}
	}
	public void getshow()
	{
		Inner inner = new Inner();//外部方法也可以创建内部类的对象在调用内部类方法
		inner.show();
	}
}
public class Test {
	public static void main(String[] args) {
		Outer outer = new Outer();
		outer.getshow();
		Outer.Inner oInner = new Outer().new Inner();//还可以直接通过这种方式创建内部类对象然后调用内部类方法
		oInner.show();
	}
}

package xr;//单例模式的运用
class Single {
	private static Single Instance = new Single();//首先创建一个对象也是这个类的唯一对象并且私有化，因为后面的方法是静态的所以它返回的对象也必须是静态的
	private Single() {
	}//把这个类的构造方法进行私有化，然后就无法再创建新的对象
	public static Single GetSingle() {
		return Instance;//声明定义一个静态类的方法然后将唯一子对象与外界建立一个接口
	}
}

public class Test {
	public static void main(String[] args) {
		Single single1 = Single.GetSingle();//静态方法可以直接用类来引用静态方法
		Single single2 = Single.GetSingle();
		System.out.println(single1==single2);
	}
}

package xr;//遍历目录下的文件名
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		File file = new File("E:/音乐");//创建一个File对象
		FileWriter fWriter = new FileWriter("E:/音乐/音乐歌名.txt");//把原来文件目录下的文件名通过字符输出流写入到新文件中
		BufferedWriter bWriter = new BufferedWriter(fWriter);//字符输出流包装成字符缓冲输出流
		if(file.isDirectory())
		{
			String[] names = file.list();//通过list方法将文件目录的内容一一取出赋值到names这个字符数组
			for(String name:names)
			{
				bWriter.write(name);//通过字符缓冲输出流写入到新文件中
				bWriter.write("\r\n");
				System.out.println(name);
			}
			bWriter.close();
			System.out.println("任务完成！！");//友好提示成功写入和显示
		}
	}
}

package xr;//转换流以及包装类的应用
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		FileInputStream in = new FileInputStream("test2.txt");//创建一个字节输入流
		InputStreamReader ins = new InputStreamReader(in);//包装成一个字符输入流
		BufferedReader bins = new BufferedReader(ins);//字符输入流包装成缓冲字符输入流
		LineNumberReader lr = new LineNumberReader(bins);//缓冲字符输入流包装成跟踪行号缓冲字符输入流
		FileOutputStream out = new FileOutputStream("test6.txt");//创建一个字节输出流
		OutputStreamWriter outw = new OutputStreamWriter(out);//包装成一个字符输出流
		BufferedWriter boutw = new BufferedWriter(outw);//字符输出流包装成缓冲字符输出流
		String str;
		while((str=lr.readLine())!=null)//如果不用lr调用readline这个方法去将内容读取到程序中那么后面的加行号这不能够不断自加一，而是一直为零
		{
			boutw.write(lr.getLineNumber()+":"+str);//将行号写入到文件中并不断自加一
			boutw.write("\r\n");
		}
		lr.close();
		bins.close();
		boutw.close();
		System.out.println("任务完成啦！！");//友好提示拷贝并输入行号完成
	}
}


package xr;//跟踪行号的输入流的运用
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		FileReader fd = new FileReader("test.txt");
		FileWriter fw = new FileWriter("test1.txt");
		LineNumberReader lr = new LineNumberReader(fd);//包装
		lr.setLineNumber(0);//设置读取文件的其实行号
		String str=null;
		while((str=lr.readLine())!=null)
		{
			fw.write(lr.getLineNumber()+":"+str);//将行号写入到文件中并不断自加一
			fw.write("\r\n");
		}
		fd.close();
		fw.close();
		lr.close();
		System.out.println("在原有文件中的每一行添加行号成功！");//友好提示拷贝并输入行号完成
	}
}

package xr;//用缓冲输入输出字符流拷贝文件
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		BufferedReader reader = new BufferedReader(new FileReader("test.txt"));//创建缓冲输入流读取文件内容到程序中
		BufferedWriter writer = new BufferedWriter(new FileWriter("test2.txt"));//创建缓冲输出流把程序的内容读取到另一个文件中
		String string;
		while((string=reader.readLine())!=null)//readline这个方法是用来读取原来文件中的字符串
		{
			writer.write(string);
			writer.newLine();//换行
		}
		reader.close();
		writer.close();//如果最后没有调用close方法那么文件的内容会暂时保留在缓冲区而不会流入拷贝到另一个文件中去
		System.out.println("用缓冲输入输出字符流拷贝文件完毕！");//友好提示拷贝完成
	}
}

package xr;//字符输出流的操作应用
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		FileWriter write = new FileWriter("test.txt",true);//创建一个write对象来向文件中输入数据
		String str="你好啊！很高兴见到你！";
		write.write(str);//可以直接将字符串输送到文件中
		write.write("\r\n");//在输入一个换行符进行换行
		write.close();
		System.out.println("已将程序内容流出到指定文件中！");//这个用来提示字符输出到文件成功完成
	}
}


package xr;//字符输入流的操作运用
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		FileReader reader = new FileReader("test.txt");//创建一个reader对象来读取文件中的字符
		int ch;
		while(true)
		{
			ch=reader.read();这个读取的是整型数据
			if(ch==-1)
				break;
			System.out.println((char)ch);//因为ch是整型数据所以如果要显示出来应该要把它强制转换为字符数据
		}
		reader.close();
	}
}

package xr;//字节缓冲流的拷贝
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		BufferedInputStream in = new BufferedInputStream(new FileInputStream("E:\\1.mp3"));//原有的文件
		BufferedOutputStream out = new BufferedOutputStream(new FileOutputStream("E:\\4.mp3"));//打算拷贝的文件
		int len=0;
		long begintime=System.currentTimeMillis();//开始的时间
		while(true)
		{
			len=in.read();
			if(len==-1)
			{
				break;
			}
			out.write(len);
		}
		long endtime=System.currentTimeMillis();//结束的时间
		System.out.println("复制花费的时间："+(endtime-begintime));//拷贝花费的时间
		in.close();
		out.close();
	}
}


package xr;//字节缓冲流
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		BufferedInputStream in = new BufferedInputStream(new FileInputStream("test.txt"));//创建一个带缓冲区的输入流，比起之前的
		BufferedOutputStream out = new BufferedOutputStream(new FileOutputStream("test2.txt"));//创建一个带缓冲区的输出流
		int len=0;
		while(true)
		{
			len=in.read();
			if(len==-1)
			{
				break;
			}
			out.write(len);
		}
		in.close();
		out.close();
	}
}


package xr;//装饰设计模式
class Car
	{
		String car_name;
		Car(String car_name)
		{
			this.car_name=car_name;
		}
		public void show()
		{
			System.out.println("我是"+car_name+",具有基本功能。");
		}
	}
class Radarcar
	{
		public Car myCar;//定义了一个car对象
		Radarcar(Car myCar) {//然后把car对象作为此构造函数的传递参数
			this.myCar=myCar;
		}
		public void show()//对原来的show进行装饰
		{
			myCar.show();//用car对象引用car类中的方法
			System.out.println("具有雷达倒车功能！");
		}
	}
public class Xr1 {
public static void main(String[] args)
	{
		Car myCar = new Car("benz");
		System.out.println("----------包装前------------");
		myCar.show();
		Radarcar decoratedcar = new Radarcar(myCar);//将创建的mycar对象作为radarcar的构造函数的参数
		System.out.println("----------包装后-------------");
		decoratedcar.show();
	}
}


package xr;//用字符流来进行程序的文件拷贝
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		FileInputStream in = new FileInputStream("target\\2.mp3");
		FileOutputStream out = new FileOutputStream("target\\3.mp3");
		int b = 0;
		byte[] zf= new byte[1024];//这里是将新建一个1024个byte大小的字符zf
		long begintime= System.currentTimeMillis();//计算的是当前的程序执行的时间，这里是指拷贝开始的时间
		while(true)
		{
			b=in.read(zf);//这里是将文件中的内容以zf字符通过输入流读取到程序中赋值给b
			if(b==-1)
			break;
			out.write(zf,0,b);//这里通过输出流以0~b个zf字符大小信息传输到target\\3.mp3
		}
		long endtime=System.currentTimeMillis();//计算的是当前的程序执行的时间，这里是指拷贝结束的时间
		System.out.print("拷贝花费的时间为："+(endtime-begintime));//(endtime-begintime)减少了很多，提高了拷贝的效率
		out.close();
		in.close();
	}
}


package xr;//这个代码讲的是程序文件的拷贝
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		FileInputStream in = new FileInputStream("target\\1.mp3");//这个是在工程之中已有的文件1.mp3，要注意为什么用\\是由于一个\是转义字符，两个才代表1个\
		FileOutputStream out = new FileOutputStream("target\\2.mp3");//这个时需要复制拷贝的文件2.mp3
		int b = 0;
		long begintime= System.currentTimeMillis();//这个运行调用的System.currentTimeMillis();//计算的是当前的程序执行的时间，这里是指拷贝开始的时间
		while(true)
		{
			b=in.read();
			if(b==-1)
			break;
			out.write(b);//这个很简单就是从已有的文件获取字节信息再用输入流输出到程序再用输出流将信息流入到自己指定的路径然后建立相关文件
		}
		long endtime=System.currentTimeMillis();//这个运行调用的System.currentTimeMillis();//计算的是当前的程序执行的时间，这里是指拷贝结束的时间
		System.out.print("拷贝花费的时间为："+(endtime-begintime));
		out.close();
		in.close();//最后都要把输入输出流建立的对象关闭
	}
}


package xr;//从程序中通过输出流将数据输出到自己定义的路径创建的文本文件，然后再通过输入流读取输入的文本文件的内容
import java.io.*;
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		FileOutputStream out = new FileOutputStream("test.txt");
		String mean="abcde";
		byte[] be = mean.getBytes();
		for(int i=0;i<mean.length();i++)
		{
			out.write(be[i]);
		}
		out.close();//每一次开始都要进行关闭
		FileInputStream in = new FileInputStream("test.txt");//创建一个文字字节的输入流，后面如果没有true那么也同样会覆盖
		int b=0;
		while(true)
		{
			b=in.read();//将文件内的内容转换为字节然后一个一个赋值给b
			if(b==-1)
				break;//当文本文件的内容已经没有时会让-1传给b，所以把终止条件这么设置
			else
				System.out.println(b);
		}
		in.close();//每一次开始都要进行关闭
	}
}

package xr;//从程序中将数据通过字节输出流输出到自己指定的路径中然后创建的文本
import java.io.*;//导入输入输出的相应的包然后才能引用相应的类
public class Xr1 {
public static void main(String[] args) throws IOException
	{
		FileOutputStream out1 = new FileOutputStream("test.txt",true);//创建一个文字字节输出流，后面的如果没有true，那么将会把输出的内容覆盖之前已有的内容，加上则是表示在原内容上进行追加
		String mean="欢迎各位校友回家！";
		byte[] b = mean.getBytes();//将mean中的字符串通过getbytes这个函数转换成单个字节存入到字节数组b[]中
		for(int i=0;i<b.length;i++)
		{
			out1.write(b[i]);在通过之前创建的对象引用write（）将字符一个一个输入到创建的新文本中
		}
		for(int i=0;i<b.length;i++)
		{
			out1.write(b[i]);
		}
		out1.close();
	}
}

package xr;//多线程之同步代码块的应用
class Saleticket implements Runnable
	{
		private int  ticket=10;
		Object lock = new Object();在这里定义了一个object的对象作为锁对象，默认情况下锁对象标志位为1
		public void run()
		{
			while(true) {
			synchronized (lock) {//当有线程进入时，锁对象标志位为1会改成0，然后其他线程就无法进入直到进入的线程执行完毕
				try {
					Thread.sleep(500);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
				if(ticket>0)
				{
					System.out.println(Thread.currentThread().getName()+"出售："+ticket--);
				}
				else break;
			}}
				
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Saleticket th = new Saleticket();
		new Thread(th,"窗口一").start();
		new Thread(th,"窗口二").start();
		new Thread(th,"窗口三").start();
	}
}

package xr;//多线程之线程插队的应用
class JoinThread implements Runnable
	{
		public void run()
		{
			for(int i=0;i<3;i++)
			{
				System.out.println(Thread.currentThread().getName()+"正在运行中");
			}		
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		JoinThread j = new JoinThread();
		Thread t = new Thread(j,"线程一");
		t.start();
		for(int i= 0;i<6;i++)
		{
			System.out.println(Thread.currentThread().getName()+"正在运行");
			if(i==1)
			{
				try {
					t.join();//当其他线程（包括主线程在内）调用另一个线程的join函数，那么这个调用的线程则会阻塞直到被join加入的线程执行完毕为止
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}
	}
}

package xr;//多线程之让步线程的应用
class YieldThread implements Runnable
	{
		public void run()
		{
			while(true)
			{
				System.out.println(Thread.currentThread().getName()+"正在运行中");
				Thread.yield();//让步线程的Thread函数调用
			}		
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		new Thread(new YieldThread(),"线程一").start();
		new Thread(new YieldThread(),"线程二").start();
	}
}

package xr;//多线程之线程休眠的应用
class SleepThread implements Runnable
	{
		public void run()
		{
			while(true)
			{
				
				System.out.println(Thread.currentThread().getName()+"is running");
				try {
					Thread.sleep(2000);//线程休眠的Thread函数调用
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
			
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		SleepThread st = new SleepThread();
		Thread s = new Thread(st,"线程一");
		for(int i=0;i<10;i++)
		{
			System.out.println("main线程正在运行");	
		}
		s.start();		
	}
}

package xr;//多线程之后台线程的运用
class DamonThread implements Runnable
	{
		public void run()
		{
			while(true)
			{
				System.out.println(Thread.currentThread().getName()+"is running");//获得目前进入run函数正在运行的线程的名字
			}
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		System.out.println("main线程是后台线程吗？"+Thread.currentThread().isDaemon());//isDaemon()这个函数是否是后台线程
		DamonThread dt = new DamonThread();
		Thread th = new Thread(dt,"后台线程");
		System.out.println("th线程是默认后台线程吗？"+th.isDaemon());
		th.setDaemon(true);//这个是将th线程设定为后台线程，并且设置后台线程必须要在start之前
		th.start();
		for(int i=0;i<10;i++)
		{
			System.out.println(i);
		}
	}
}

package xr;//多线程的运用，此运行过程对CPU占用率极大一定要及时停止程序的运行
class Mythread implements Runnable
	{
	private int tickets=100;
		public void run()
		{
			
			while(true)
			{
				
				if(tickets>0)
				{Thread th = Thread.currentThread();
				String th_name=th.getName();
				System.out.println(th_name+"正在运行"+tickets--+"张票");}
			}
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Mythread tw = new Mythread();//这里只建了一个对象
		new Thread(tw,"窗口1").start();//下面五个的线程都只用了一个对象作为开启，所以所有线程共享一个对象资源
		new Thread(tw,"窗口2").start();
		new Thread(tw,"窗口3").start();
		new Thread(tw,"窗口4").start();
		new Thread(tw,"窗口5").start();
		
	}
}

package xr;//多线程的函数运用
class Mythread implements Runnable
	{
		public void run()
		{
			while(true)
			{
				Thread th = Thread.currentThread();
				String th_name=th.getName();//这个步骤和上面那个步骤一起使用可以获得已经进入调用此函数的线程名称
				System.out.println(th_name+"正在运行");
			}
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		new Thread(new Mythread(),"线程1").start();//如果没有我们给线程命名那么系统也会给他们自动分配命名
		new Thread(new Mythread(),"线程2").start();//建立了一个两个对象的线程，并且给线程命名了
		while(true)
		{
			System.out.println("Main线程在运行");
		}
	}
}

package xr;//多线程的运用
class Mythread implements Runnable//定义一个类去实现Runnable
	{
		public void run()
		{
			while(true)
			{
				System.out.println("Mythread线程在运行");
			}
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Mythread mythread = new Mythread();//建立起此类的对象
		Thread thread = new Thread(mythread);//把这个对象作为多继承的对象被Thread（）传送到Thread，然后可以调用才可以start
		thread.start();
		while(true)
		{
			System.out.println("Main线程在运行");
		}
	}
}

package xr;//单线程的尝试运用
class Mythread extends Thread//定义一个类然后继承Thread这个类，之后在在主函数中用此类中的start开始单线程的运用
	{
		public void run()
		{
			while(true)
			{
				System.out.println("Mythread线程在运行");
			}
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Mythread mythread = new Mythread();//建立一个类的对象同时也相当于继承Thread中的start函数开启单线程
		mythread.start();//开启单线程
		while(true)
		{
			System.out.println("Main线程在运行");
		}
	}
}

package xr;

public class xr6 {
public static void main(String[] args)
    {
		System.out.println("这是第一个"+"JAVA的程序");//就是运用加号讲两句话连起来输出
	}

}

package xr;

public class xr6 {
	public static void main(String[] args)
	{
		char a='a';
		byte b=0;
		int c=10;
		long d=10000L;
		float e=12.5f;
		double f=236.222d;
		boolean g=false;
		System.out.println(g);//对基本类型的声明定义的标准的格式
	}
}

package xr;

public class xr6 {
public static void main(String[] args) {
	int num=20;
	byte c='a';
	c=(byte)num;//数据的强制转换
	System.out.println(c);
}
}

package xr;

public class xr6 {
	public static void main(String[] args)
	{
		byte a=1;
		byte b=2;
		byte c=(byte)(a+b);//这个是表达式类型自动提升从byte转换成int型所以需要强制转换
		System.out.println(c);
	}
}
package xr;

public class xr6 {
	public static void main(String[] args) {
		int a=5%(-2);
		int b=(-5)%2;//余数的正负取决于取余号的前面的数的正负，两者符号相同
		System.out.println(a+"<-两者区别->"+b);
		
	}
}
package xr;

public class xr6 {
	public static void main(String[] args)
	{
		int a,b,c;
		a=b=c=5;//可以证明JAVA中三个变量可以同时赋值，但要注意不能在声明中连续赋值
		System.out.println(a);
	}
}
package xr;

public class xr6 {
	public static void main(String[] args)
	{
		int a=0,b=0,c=0;
		boolean x,y;
		x=a>1&b++>1;//两边的计算都可以发生
		y=a++>2&&++c>0;//短路与&&，只有前面的成立后面的计算式才会计算
		System.out.println(x);
		System.out.println(b);
		System.out.println(y);
		System.out.println(c);
	}
}
package xr;

public class xr6 {
	public static void main(String[] args)
	{
		int i,j;
		itcast:for(i=1;i<=4;i++)
			{for(j=1;j<=i;j++)
			{
				if(i>4)
					break itcast;//原本break只能终止一层循环，但是可以用对外层循环进行标记的方法来终止内外循环
				System.out.print('*');
			}
		System.out.print('\n');}//注意print和printIn的区别在于第一个输出是不换行
	}
}
package xr;
public class xr6 {
	public static void printrectangle(int height,int width)
    {
		int i,j;
		for(i=1;i<=height;i++)
		{
			for(j=1;j<=width;j++)
			{
				System.out.print('*');
			}
			System.out.print('\n');
		}
		System.out.print('\n');
	}
	public static void main(String[] args)
	{
		printrectangle(10, 20);
		System.out.print('\n');
		printrectangle(5, 4);//调用函数进行运算
		
	}
}
package xr;
public class xr6 {
	public static int getarea(int x,int y)//注意可以返回函数值的函数的定义
	{
		int w;
		w=x*y;
		return w;
	}
	public static void main(String[] args)
	{
		int area;
		area=getarea(2, 3);//这是调用可以返回值的函数
		System.out.println("The area is:"+area);
	}
}
package xr;
public class xr6 {
	public static void main(String[] args)
	{
		int sum1,sum2;
		double sum3;
		sum1=add(0,1);//同样的函数名但是参数的个数或者参数的类型不同就可以调用，此为函数重载
		sum2=add(0, 1, 1);
		sum3=add(1.5, 1.5);
		System.out.println("sum1="+sum1);
		System.out.println("sum2="+sum2);
		System.out.println("sum3="+sum3);	
	}
	public static int add(int a,int b)
	{
		return (a+b);
	}
	public static int add(int a,int b,int c)
	{
		return (a+b+c);
	}
	public static double add(double a,double b)
	{
		return (a+b);
	}
}
package xr;
public class xr6 {
	public static void main(String[] args)
	{
		int[] arr=new int[4];//数组的创建的一种方式
		System.out.println(arr.length);//调用了数组的长度函数
	}
}
package xr;
public class xr6 {
	public static void main(String[] args)
	{
		int[] arr= {1,2,3,4};//这是数组的另一种创建方式以及初始化
		System.out.println(arr[0]+arr[1]);
		System.out.println(arr[2]+arr[3]);
		
	}
}
package xr;
public class xr6 {
	public static void main(String[] args)
	{
		int[][] arr=new int[3][];//二维数组的定义以及应用
		arr[0]=new int[]{1,2};
		arr[1]=new int[]{2,3};
		arr[2]=new int[]{3,4};
		int sum=0,i,j;
		for(i=0;i<arr.length;i++)//这里的arr.length大小为行的大小
		{
			int groupsum=0;
			for(j=0;j<arr[i].length;j++)//这里的arr[i].length表示第i列的大小长度
				groupsum=arr[i][j]+groupsum;
			sum=sum+groupsum;
			System.out.println("第"+i+"组的销售总数："+groupsum);
		}
		System.out.println(sum);
	}
}
package xr;
class Person
	{
		int age=10;
		void speak()
		{
			int age=18;
			System.out.println("我今年的岁数是："+age+"岁!");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Person x =new Person();//类的实例化对象的定义，注意格式
		x.speak();//输出的是我今年的岁数是：18岁!，此时访问的是speak中的局部变量age=18
		System.out.println(x.age);//这个输出的是10，这个调用的是类的成员变量
	}
	
}
package xr;
class Person
	{
		int age;
		void speak()
		{
			System.out.println("我今年的岁数是："+age+"岁!");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Person x1 =new Person();
		Person x2 =new Person();
		x1.age=18;//这是对x1中的成员变量赋值
		x1.speak();//成员变量赋值所以输出18
		x2.speak();//成员变量没有赋值所以是0
	}
	
}
package xr;
class Person
	{
		int age;
		void speak()
		{
			System.out.println("我今年的岁数是："+age+"岁!");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Person x1 =new Person();
		Person x2 =new Person();
		x1.age=18;//这是对x1中的成员变量赋值
		x1.speak();//成员变量赋值所以输出18
		x2=null;//一旦把x2这个对象的引用给指向空了，就不能再调用这个类的成员
		x2.speak();//所以这个引用
	}
	
}
package xr;
class Student1
	{
		private String name;
		private int age;
		public String getname()
		{
			return name;
		}
		public void setname(String n)
		{
			name=n;
		}
		public int getage()
		{
			return age;
		}
		public void setage(int a)
		{
			if(a>0)
			age=a;
			else 
				System.out.println("输入的年龄不合法！！");
		}
		public void introduce()
		{
			System.out.println("大家好，我的名字叫做："+name+",我今年"+age+"岁！");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Student1 x = new Student1();
		x.setage(10);
		x.setname("小红");
		x.introduce();
	}
	
}
package xr;
class Person
	{
		int age;
		public Person(int a)//建立了类的构造方法
		{
			age=a;
		}
		public void speak()
		{
			System.out.println("我现在的岁数是："+age);
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Person p = new Person(18);//建立了构造方法之后建立对象也是有变化的
		p.speak();
	}
}
package xr;
class Person
	{
		int age;
		public Person(int age)
		{
			this.age=age;//this关键字可以明确的访问类的成员变量从而解决与局部变量名冲突问题
		}
		public void speak()
		{
			System.out.println("我现在的岁数是："+age);
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Person p = new Person(18);
		p.speak();
	}
}
package xr;
class Person
	{
		public Person()
		{
			System.out.println("无参的构造函数被调用了！");
		}
		public Person(String name)
		{
			this();//只能在构造函数中调用this去调用其他构造函数，并且不能互相调用而且只能放在第一行
			System.out.println("有参的构造函数被调用了"+name);
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Person p = new Person("hnust");
	}
}
package xr;
class Student2
	{
		static String schoolname;//用关键字static声明的类变量能够被该类的所有实例对象共享
	}
public class xr6 {
	public static void main(String[] args)
	{
		Student2 x1=new Student2();
		Student2 x2=new Student2();
		Student2.schoolname="hnust";//可以用类名.变量来进行赋值改值
		System.out.println(x1.schoolname);
		System.out.println(x2.schoolname);
	}
}
package xr;
class Student2
	{
		static void sayhello()//声明定义了一个static的方法，它只能调用static的成员变量
		{
			System.out.println("hello");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Student2.sayhello();//可以直接用类名.方法来用
	}
}
package xr;
class Student2
	{
		static 
		{
			System.out.println("Student2中的静态代码块执行了");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Student2 x1 = new Student2();//静态代码块只执行一次，所以上面的话只输出一次
		Student2 x2 = new Student2();
	}
}
package xr;
class Single//单列模式的应用
	{
		private static Single instance= new Single();//对类的对象的构造方法进行私有化，然后就不能在主类中引用构造
		private Single() {}
		public static Single getinstance()//定义一个静态类方法这样就可以直接用类名.方法名调用这个方法复值对象
		{
			return instance;
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		Single s1=Single.getinstance();
		Single s2=Single.getinstance();
		System.out.println(s1==s2);//一般输出的内容有判断输出的为布尔类型如true
	}
}
package xr;
class Single//单列模式的另一种表示
	{
		private Single() {}//对构造函数进行私有化这样可以防止主类中再重新构造此类的对象
		public static final Single instance=new Single();//static表示可以用类名.成员变量引用但final表示不可以改变对象的值
	}
public class xr6 {
	public static void main(String[] args)
	{
		Single s1=Single.instance;
		Single s2=Single.instance;
		System.out.println(s1==s2);//一般输出的内容有判断输出的为布尔类型如true
	}
}
package xr;
class outer//声明定义了一个外部类
	{
		private int num=18;
		public void test()
		{
			inner i = new inner();//外部类要访问内部类必须先定义一个内部类对象
			i.show();//用内部类对象调用内部类成员方法
		}
		class inner
		{
			void show()
			{
				System.out.println(num);//而内部类可以直接调用外部类的成员
			}
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		outer o = new outer();
		o.test();
	}
}
package xr;
class outer//声明定义了一个外部类
	{
		private static int num=18;//定义外部类静态成员变量
		static class inner//可以定义一个静态内部类，可以在不创建外部类对象的情况下被实例化，在静态内部类中可以定义静态成员
		{
			void show()//在非静态内部类中不能定义静态成员
			{
				System.out.println(num);//静态方法调用的是静态成员变量
			}
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		outer.inner x = new outer.inner();//内部类被实例话，创建内部类对象
		x.show();//调用内部类方法
	}
}
package xr;
class outer//声明定义了一个外部类
	{
		private int num=18;
			void show()
			{
				class inner//声明定义了一个方法内部类，只能在方法中被使用
				{
					void showner()
					{
						System.out.println(num);//方法内部类还是可以调用外部类的成员
					}
				}
				inner n = new inner();
				n.showner();
			}
	}
public class xr6 {
	public static void main(String[] args)
	{
		outer o = new outer();
		o.show();
	}
}
package xr;
class animal//定义了一个父类
	{
		String name;
		void shout()
		{
			System.out.println("动物在发出叫声！");
		}
	}
class dog extends animal//定义了一个子类继承了父类
	{
		 public void printname()
		 {
			 System.out.println(name);//子类继承了父类的成员
		 }
	}
public class xr6 {
	public static void main(String[] args)
	{
		dog d = new dog();
		d.name="哈士奇";//对继承父类的成员变量的子类的对象的成员变量进行赋值
		d.printname();
		d.shout();//继承父类的子类调用父类中的方法
	}
}
package xr;
class animal//定义了一个父类
	{
		void shout()
		{
			System.out.println("动物在发出叫声！");
		}
	}
class dog extends animal//定义了一个子类继承了父类
	{
		 void shout()//对父类的方法进行重载，重载的方法必须是方法名、参数类型以及个数、返回值类型也要相同
		 {
			 System.out.println("狗在叫");//子类继承了父类的成员
		 }
	}
public class xr6 {
	public static void main(String[] args)
	{
		dog d = new dog();
		animal a = new animal();
		a.shout();//这个和下面输出的结果是不一样的
		d.shout();
	}
}
package xr;
class animal//定义了一个父类
	{
		void shout()
		{
			System.out.println("动物在发出叫声！");
		}
	}
class dog extends animal//定义了一个子类继承了父类
	{
		 void shout()//对父类的方法进行重载，重载的方法必须是方法名、参数类型以及个数、返回值类型也要相同
		 {
			 super.shout();//用super可以调用父类的构造函数只能放在第一行并且只能出现一次
		 }
	}
public class xr6 {
	public static void main(String[] args)
	{
		dog d = new dog();
		animal a = new animal();
		a.shout();//这个和下面输出的结果是不一样的
		d.shout();
	}
}
package xr;
abstract class animal//用abstract定义了一个抽象父类，抽象类是不能实例化对象的，含抽象方法的类必须是抽象类，但抽象类可以不包含抽象方法
	{
		abstract void show();
	}
class dog extends animal//定义了一个子类继承了父类
	{
		void show()
		{
			System.out.println("汪汪...");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		dog d = new dog();//对子类进行对象实例化
		d.show();//用对象调用子类的方法
	}
}
package xr;
interface animal//用interface定义了animal的接口，里面的都是抽象方法
	{
		int i=1;//定义全局变量，注意一定要赋初值，同等fianl定义一个变量时也需要开始赋初值然后成为常量
		void breath();//省略了public
		void run();
	}
class dog implements animal//用implements继承接口，要对接口中的所有抽象方法进行，必须对接口中的所有方法进行定义
	{
		public void breath()//不能省public
		{
			System.out.println("狗仔呼吸");
		}
		public void run()//不能省public
		{
			System.out.println("狗在跑");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		dog d = new dog();
		d.breath();
		d.run();
	}
}
package xr;
interface animal
	{
		int i=1;
		void breath();
		void run();
	}
interface animal2 extends animal//接口与接口之间也可以用extends继承，所以此接口也继承了animal接口中的抽象方法
	{
		void eat();
	}
class dog implements animal2//用implements继承接口，要对所继承的接口中的所有抽象方法进行，必须对接口中的所有方法进行定义
	{
		public void breath()
		{
			System.out.println("狗仔呼吸");
		}
		public void run()
		{
			System.out.println("狗在跑");
		}
		public void eat()
		{
			System.out.println("狗在吃");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		dog d = new dog();
		d.breath();
		d.run();
		d.eat();
	}
}
package xr;
interface animal//多态的应用
	{
		int i=1;
		void breath();
		void run();
	}

class dog implements animal
	{
		public void breath()
		{
			System.out.println("狗仔呼吸");
		}
		public void run()
		{
			System.out.println("狗在跑");
		}
	}
class cat implements animal
{
	public void breath()
	{
		System.out.println("猫在呼吸");
	}
	public void run()
	{
		System.out.println("猫在跑");
	}
}
public class xr6 {
	public static void main(String[] args)
	{
	    animal d = new dog();//用一个父类的对象来引用一个子类的对象
	    animal c = new cat();
	    animalbreathrun(d);//调用函数
	    animalbreathrun(c);
		
	}
	public static void animalbreathrun(animal an)//接受相应的父类对子类对象的引用的对象，子类继承父类的成员都可以通过传递用起来
	{
		an.breath();//通过父类的对象调用了子类中实例化的方法
		an.run();
	}
}
package xr;
interface animal
	{
		int i=1;
		void breath();
	}

class dog implements animal
	{
		public void breath()
		{
			System.out.println("狗仔呼吸");
		}
		public void run()
		{
			System.out.println("狗在跑");
		}
	}
class cat implements animal
{
	public void breath()
	{
		System.out.println("猫在呼吸");
	}
	public void run()
	{
		System.out.println("猫在跑");
	}
}
public class xr6 {
	public static void main(String[] args)
	{
		dog d = new dog();
	    cat c = new cat();
	    animalbreathrun(c);
		
	}
	public static void animalbreathrun(animal an)
	{
		cat c = (cat)an;//父类的引用对象不能调用子类的单独的方法，但是可以用强制转换
		c.breath();
		c.run();
	}
}
package xr;
class student3
	{
		void shout()
		{
			System.out.println("学生大喊大叫");
		}
	}
public class xr6 {
	public static void main(String[] args)
	{
		student3 stu = new student3();
		System.out.println(stu.toString());//虽然类中没有定义这个方法但是相当于类继承了object这个类，而toString()就是这个类中的方法
	}
}
package xr;
interface animal
	{
		void shout();
	}
public class xr6 {
	public static void main(String[] args)
	{
		animalshout(new animal() {//匿名内部类的一个声明定义，注意格式
			public void shout()
			{
				System.out.println("动物在叫");
			}
		});
	}
	public static void animalshout(animal an)
	{
		an.shout();
	}
}
