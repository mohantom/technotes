Design Patterns
===================
reusable and extensible OOP

encapsulation, abstraction, inheritance, polymorphism

## Principles
1.开-闭原则（ocp）：一个软件实体应该对扩展开放（底层对业务的实现应该是可灵活改变的，针对接口编程？），对修改关闭（高层的业务逻辑由抽象类定义，确定后不能修改） 
  eg:模版方法，好莱坞原则 
2.里氏代换原则（lsp）：任何基类适应的地方，子类一定适用（继承？） 
3.依赖倒转原则（dip）：要依赖于抽象，不能依赖于实现（针对接口编程？） 
     a.零耦合  b.具体耦合（耦合关系建立在具体类之间）  c.抽象耦合（耦合关系依赖于抽象类或接口） 
     
4.接口隔离原则（isp）：使用多个专门的接口比使用单一的总接口要好 
     原因：服务定制与接口污染 
5.组合/聚合复用原则（crad）：要尽量使用组合/聚合，而不是使用继承来达到目的 
   原因： 
       继承复用的缺点：静态复用 
       什么使用使用继承：a.满足 is-a的关系，而不是 has-a的关系 
                         b.满足lsp原则 
       优点：a.简洁  b.父类修改某个方法，子类能获得 

6.迪米特法则（lod），也称最少知识原则：一个对象或模块应该和其它对象和模块尽量少的通信（高内聚），涉及的模式有：门面模式，调停者模式，前端控制器模式，业务代表模式，dao模式 


## 23 设计模式：
- Creational: deal with creation of objects
- Structural: concerned  with the structure (eg, class members)
- Behavioral: no central theme

接口型：适配器模式（Adapter）、外观模式（Façade）、合成模式（Composite）、桥接模式（Bridge）；
职责型：单例模式（Singleton）、观察者模式（Observer）、调停者模式（Mediator）、代理模式（Proxy）、职责链模式（Chain of Responsibity）、享元模式（Flyweight）；
构造型：构建者模式（Builder）、工厂方法模式（Factory Method）、抽象工厂模式（Abstract Factory）、原型模式（Prototype）、备忘录模式（Memento）；
操作型：模板方法模式（Template Method）、状态模式（State）、策略模式（Strategy）、命令模式（Command）、解释器模式（Interpreter）；
扩展型：装饰器模式（Decorator）、迭代器模式（Iterator）、访问者模式（Visitor）。


工厂模式：由工厂对象来实现对象的创建；好处，当扩展时没必要修改引用类的代码 
       a.简单工厂:一个工厂负责创建所有对象  
       b.工厂方法:一种对象由一种工厂创建 
单例模式：系统中你需要获得某个类的唯一实例（内存中只维护一个实例） 
         a.懒汉式:有线程安全问题，创建的对象可能不止一次，但只有一个被维护，     
       其余将会被gc，解决的方法是在静态方法前加synchronized 
        b.饥饿式 
组合模式:描述对象之间整体与部分之间的关系，需使用一个接口装配接口下的单纯元素与复合元素  eg:java.awt.Component的 Container 与java.io.File下的文件与目录 
观察者模式:当主题的状态发生改变的时候，需通知其它对象类  
          eg:java.awt的事件处理机制，数据库的缓存池维持的实例数目 
策略模式:从多个相似的算法中选择一个  
          eg:java.awt中的布局管理器 
mvc模式:解决模型层与视图层的耦合问题 
        m:观察者模式？ 
        v:组合/聚合模式？ 
        c:策略模式？ 

状态模式:与策略模式类似，对象的行为依赖与其状态，对象必须根据其状态选择不同的行为方式 
      *  状态模式提供依赖的是其自身的状态，策略模式由一个类控制实现哪一个算法 
委托：客户端通过委托类间接调用被委托类的方法，委托类可附加一些操作来为客户端服务 
代理:本质上也是一种委托模式，被委托类与委托类都实现同一个接口，客户端不区分被委托类和委托类



## Design principles
- DRY - Don't Repeat Yourself - Pretty much self-explanatory.  If you are re-writing the same block(s) of code in 
various places then you are ensuring that you'll have multiple places to change it later.  This is probably the #1
 warning flag that you should look into an alternative/pattern.

- YANGNI - You Ain't Gonna Need It - Don't code out every little detail that you can possibly think of because, 
in reality, you probably won't end up needing much of it.  So just implement what is absolutely necessary 
(save the GUI until later, for example!)

- KISS - Keep It Stupid Simple - When in doubt, make it easy to understand.  Don't try to build in too much complexity.  
If a particular design pattern overly complicates things (vs. an alternative or none at all) then don't implement it. 
This applies heavily to user interface design and APIs (application programming interfaces).

- POLA - Principle Of Least Astonishment - This has overlap with KISS...  Do the least astonishing thing.  
In other words: DON'T BE CLEVER.  It's nice that you can squeeze a ton of detail into a single line of code.  
But your future self and other developers will judge it by the number of "F"-words per minute when they open your source file.  
It should be relatively easy to jump into what your code is doing, even for an outsider who isn't quite as clever as you are.

Last, and most certainly NOT least...

- SOLID
    - Single Responsibility - A class should have only one reason to change;  Do one thing and do it well.
    - Open/Closed Principle - A class should be open for "extension" but closed for "modification".
    - Liskov Substitution Principle - Derived (sub) classes should fit anywhere that their base (super) class does.
    - Interface Segregation - Multiple specific interfaces are better than one general-purpose interface: 
        Printer, Scanner, Fax instead of Printer with print(), scan(), fax()
        Or use decorator: AIOPrinter { private printer; private scanner; }
    - Dependency Inversion - Depend on abstractions NOT on concrete implementations.  (Depend on abstract classes and interfaces, which can't be instantiated, rather then any specific instance)



Course: Design Patterns in Java Structural
Singleton, factory, strategy
Adapter: Legacy code -> adapter
Arrays.asList(arrayOfInts);

Take legacy class as member
Public void getEmail() {
	Return instance.getEmailAddress();
}

Can provide multiple adpaters.
Modify behavior (adds) and also provide a different interface.



## Decorator
```shell script
//改写com.mysql.jdbc.Connection中的close方法, 在调用时, 不是关闭连接而是返回池中
public class MyConnection implements Connection {  //java.sql.Connection
	private Connection conn;// 引用被改写对象
	private LinkedList<Connection> pool;
	public MyConnection(Connection conn, LinkedList<Connection> pool){//  通过构造方法注入需要的对象, 类似Spring
		this.conn = conn;
		this.pool = pool;
	}
		
	@Override
	public void close() throws SQLException {
		pool.add(conn);
	}


public class MyBufferedReader extends BufferedReader{
	private int count = 1;
	public MyBufferedReader(BufferedReader br){
		super(br);
	}
	//先拿到原有对象的对应方法, 判断其返回值后再进行包装
	public String readLine() throws IOException {
		String data = super.readLine();
		if(data==null)
			return data;
		return count+++data;
	}
}

```

Also called wrapper, add behavior without affecting others. More than just inheritance, single responsibility principle.
Java.io.InputStream
UI components

Inheritance based
Utilizes composition and inheritance (is-a, has-a)
Alternative to subclassing
Constructor requires instance from hierarchy

// Java example
```shell script
File file = new File("./output.txt");
file.createNewFile();
OutputStream oStream = new FileOutputStream(file);
DataOutputStream doStream = new DataOutputStream(oStream);
doStream.writeChars("text");
```

## Dynamic proxy
```shell script
	public synchronized Connection getConnection() throws SQLException {
		if(pool.size()>0){
			final Connection conn = pool.remove();//原有对象
			//返回动态代理对象
			return (Connection)Proxy.newProxyInstance(conn.getClass().getClassLoader(), conn.getClass().getInterfaces(), new InvocationHandler() {
				@Override
				public Object invoke(Object proxy, Method method, Object[] args)
						throws Throwable {
					if("close".equals(method.getName())){
						return pool.add(conn);  //重写close()
					}else{
						return method.invoke(conn, args); //其他方法调用原对象的
					}
				}
			});
		}else{
			throw new RuntimeException("对比起！服务器真忙");
		}

```


## Factory
传统方法：
		// Animal a = new Dog();
		// a.eat();
		// a = new Cat();
		// a.eat();
		// a = new Pig();
		// a.eat();
简单工厂模式：

* main：客户端
 * 客户端一般只是使用对象调用功能。
 * 而假设对象特别的多，创建比较复杂，那么，我们就应该按照职责分离思想，
 * 用一个工厂类来专门负责对象的创建。
 * AnimalFactory
public class AnimalFactory {
	private AnimalFactory() {
	}

	public static Animal createAnimal(String type) {
		if ("cat".equals(type)) {
			return new Cat();
		} else if ("dog".equals(type)) {
			return new Dog();
		} else if ("pig".equals(type)) {
			return new Pig();
		} else {
			return null;
		}
	}
}

// 简单工厂的调用
		// Animal a = AnimalFactory.createAnimal("cat");
		// a.eat();
		//
		// a = AnimalFactory.createAnimal("dog");
		// a.eat();
		//
		// a = AnimalFactory.createAnimal("pig");
		// a.eat();

工厂方法模式：
	/* 由于简单工厂是把所有对象的创建都放在了一个工厂类里面，假如要创建的对象特别的多,这个工厂类就非常的复杂，不利于后期的维护。怎么办呢？我们想了另外的一种方式：
	把每一个对象的创建，都有一个对应的工厂去做。这样的话，每一个工厂只需要负责自己对象的创建即可。这就叫工厂方式模式。
首先：定义一个工厂，在这个工厂里面定义了规范。定义一个Factory接口。接着，我们定义三个具体的工厂类，来创建每一个具体的对象。测试  */

public interface Factory {
	public abstract Animal createAnimal();
}

public class DogFactory implements Factory {
	@Override
	public Animal createAnimal() {
		return new Dog();
	}
}

// 工厂方法测试：
		Factory factory = new DogFactory();
		Animal a = factory.createAnimal();
		a.eat();

/* 优点：在工厂方式模式中,客户端不去负责对象的创建，而是把对象的创建交给了工厂类。如果有新产品进来,只需要添加一个具体的新产品的工厂，就可以使用了。 不会去影响我以前的代码。后期的维护就会非常的容易。 增强了系统的扩展性。（比如要创建一个狼类，只要加一个狼的WolfFactory 工厂，就可以了，不用修改以前的代码。
*/

抽象工厂模式：(了解)


## Template
HttpServlet -> HttpServletRequest, HttpServletResponse
	定义一个算法的执行骨架，将具体的算法实现延迟到子类完成。
为什么会有模板方法模式？	
	我现在有一个需求：
		要求用户做一个打印程序：规定必须打印表头，正文，表尾3部分。
		我们可以用一个简单的类就实现了。
public class Report {
	public void print(){
		System.out.println("打印表头");
		System.out.println("打印正文");
		System.out.println("打印表尾");
	}
}
	这个时候，我们好像看不到任何问题。	但是，需求是在不断的变化的。	比如说：我想在表头做一些修改，怎么办？改动代码。过一段时间，我又想在正文添加一些内容，怎么办？继续改动代码？这样，如果还有其他的需求，那么，最终我感觉就崩溃了。
	怎么解决呢？就可以采用我刚才说的模板方法模式改进。	改进的过程请查看代码。
```shell script
public abstract class Report {
	public void print() {
		printTitle();
		printBody();
		printTail();
	}
	public abstract void printTitle();
	public abstract void printBody();
	public abstract void printTail();
}

public class ReportImpl extends Report {
	@Override
	public void printTitle() {
		System.out.println("打印表头");	}
	@Override
	public void printBody() {
		System.out.println("打印正文");	}
	@Override
	public void printTail() {
		System.out.println("打印表尾");	}
}

// 如果有新的需求, 可以另外写一个实现. 不需要改动原来的实现.
public class ReportImpl2 extends Report {
	@Override
	public void printTitle() {
		System.out.println("使用另外的方式打印表头");	}
	@Override
	public void printBody() {
		System.out.println("使用另外的方式打印正文");	}
	@Override
	public void printTail() {
		System.out.println("使用另外的方式打印表尾");	}
}
```


总结：
	模板方法模式：抽象的骨架类，具体的实现类。
	优点：
		使用模板方法模式，在定义算法骨架的时候，可以灵活的实现具体的算法。
		满足用户多变的需求。
	缺点：
		假如算法骨架有改动，就需要修改抽象类，那么，具体的实现类，也会跟着
		修改。

实际应用：
	需求：计算一个程序的运行时间。
```shell script
public class GetTime {
	public void getTime() {
		long start = System.currentTimeMillis();
		// 运行一个程序
		for (int x = 0; x < 10000; x++) {
		System.out.println(x);
		}
		long end = System.currentTimeMillis();
		System.out.println("毫秒：" + (end - start));
	}
}
```

	这个时候，虽然完成了我们的功能，但是不好。 因为我们是直接在main方法里面做的。注意：main方法是测试别人写好的东西的。你不能直接把很多的代码都写在main里面。所以，我们需要改进。用一个类来封装代码改进。GetTime
虽然我们用一个类改进了代码，但是还是会有问题？问题是：我们要运行的代码是不固定的。
		// 比如说：我不喜欢for循环，我喜欢while，改代码。
		// 在比如说：我的代码根本就不是测试一个循环的次数。
		// 可能是一个上传文本文件的操作。我需要记录时间。
		// 怎么办呢？用抽象类定义一个算法骨架
	定义一个GetTime类。
	定义具体的实现类。
```shell script
public abstract class GetTime {
	public void getTime() {
		long start = System.currentTimeMillis();
		//表示将来要计算时间的代码
		code();

		long end = System.currentTimeMillis();
		System.out.println("毫秒：" + (end - start));
	}

	public abstract void code();
}

Public class ForDemo extends GetTime {
	@Override
	Public void getTime() {
		// 
	}
}
```


//测试
		GetTime gt = new ForDemo(); // 多态̬
		gt.getTime();
// 换成 while()的方式
		gt = new WhileDemo();
		gt.getTime();


## Proxy
	找房时候的中介，或者银行或基金的理财业务。都不用你自己去做，让别人做就可以。
静态代理
	缺点：如果操作类很多,我们就需要提供很的代理类。而且每个方法都是我们手动的加入纪录日志的功能。这样太麻烦了。

public class OperatorProxy implements Operator {

	private OperatorImpl operatorImpl;

	public OperatorProxy(OperatorImpl operatorImpl) {
		this.operatorImpl = operatorImpl;
	}

	@Override
	public void add() {
		System.out.println("纪录日志开始... ");
		// System.out.println("增加功能");
		this.operatorImpl.add();
		System.out.println("纪录日志结束... ");
	}

	@Override
	public void delete() {
		System.out.println("纪录日志开始... ");
		this.operatorImpl.delete();
		System.out.println("纪录日志结束... ");
	}

	@Override
	public void update() {
		System.out.println("纪录日志开始... ");
		this.operatorImpl.update();
		System.out.println("纪录日志结束... ");
	}

	@Override
	public void find() {
		System.out.println("纪录日志开始... ");
		this.operatorImpl.find();
		System.out.println("纪录日志结束... ");
	}

}
动态代理
	我们用动态代理实现。以前是针对每种操作提供一个代理类。现在是针对每个功能提供一个代理类。比如说：我现在要纪录日志信息。我就是要实现日志纪录功能。我就专门为实现日志纪录提供一个代理。动态代理必须实现一个接口：InvocationHandler
public class LogOperatorProxy implements InvocationHandler {
	//目标对象
	private Object target; // OperatorImpl

	//我们自己还会写一个功能。
	//绑定代理对象
	public Object bind(Object target) { // OperatorImpl
		this.target = target; // OperatorImpl
		/*
		 * public static Object newProxyInstance(ClassLoader loader, Class<?>[]
		 * interfaces, InvocationHandler h) 
第一个参数：定义代理的类加载器 
第二个参数：代理类要实现的接口
		 * 	第三个参数：指派方法调用处理程序		 */
		return Proxy.newProxyInstance(target.getClass().getClassLoader(),
				target.getClass().getInterfaces(), this);
	}

	@Override
	public Object invoke(Object proxy, Method method, Object[] args)
			throws Throwable {
		Object obj = null;
		System.out.println("开始记录信息...");
		obj = method.invoke(target, args); //OperatorImpl,add
		System.out.println("结束记录信息...");
		return obj;
	}
}

// 测试
		LogOperatorProxy proxy = new LogOperatorProxy();
		Operator operator = (Operator) proxy.bind(new OperatorImpl());

		operator.add();
		operator.delete();
		operator.update();
		operator.find();		


Intercept 

▪ Interface by wrapping
▪ Can add functionality
▪ Security, Simplicity, Remote, Cost
▪ Proxy called to access real object
▪ Examples:
▪ java.lang.reflect.Proxy
▪ java.rmi.*


Interface based
Interface and Implementation Class
java.lang.reflect.InvocationHandler
java.lang.reflect.Proxy
Client, Interface, InvocationHandler, Proxy,
Implementation

// intercept method calls
If(m.getName().contains(“post”) {
	Throw IllegalAccessException(“Posts are currently not allowed”);
} else {
	Result = m.invoke(obj, args);
}

Can have only ONE proxy. Another abstraction. Compile time.

In contrast to decorator:
Decorator: dynamically add functionality, chained, points to its own type. Runtime. 


## Adapter
图形化界面 awt
Frame f = new Frame();
f.setVisible(true);

需要一个关闭窗口的类，但是接口WindowListener有7个方法需要覆盖。
Class MyListener implements WindowListner {
Public void windowClosed (WindowEvent e) { }
Public void windowActivated(WindowEvent e) { }
… }

有另外一个抽象类，WindowAdapter也implements 了WindowListener，但是里面的方法都是空的（没有抽象方法，方法都实现了，但是没有具体内容）。这样MyListener继承WindowAdapter后，只要覆盖windowClosed方法！
Class MyListener extends WindowAdapter {
	Public void windowClosing (WindowEvent e) {
		System.out.println(“window closed.”);
		System.exit(0); } }
// 调用：
f.addWindowListener(new MyListener()); 

用匿名内部类简化代码（注意必须是抽象或者接口才可以）
f.addWindowListener(new WindowAdapter() { 
	@Override  // 还可以帮助检查是否有错
	Public void windowClosing(WindowEvent e) { 
		System.out.println(“window closed.”);
		System.exit(0); } }
}
} );


## Observer
当股票（股价、成交量）发生变化时，自动发消息给客户端：手机、电脑、网页
平常的方法：股票变动，Stock -> ComputerClient, PhoneClient, WebClient 自己发消息给终端
Public void stockPriceChange() { 
	ComputerClient cc = new ComputerClient();
	cc.priceChange(name); }
新方法：做一个接口
interface StockObserver { 
	public abstract void stockChange()；
	public abstract void countChange();
}
Public class ComputerClient implements StockObserver { }
Public class PhoneClient implements StockObserver { }

改进：动态增加、删除终端：
再做一个抽象类 abstract AbstractStock.java，维护一个终端列表（类型是端口StockObserver）
Private String name;
ArrayList<StockObserver> al = new ArrayList<>()
Public void addClient (StockObserver so) { al.add(so); }
Public void deleteClient(StockObserver so) {al.remove(so);}
Public void priceChange() {
	For (int x = 0; x < al.size(); x++ ) {
		StockOberserver s = al.get(x);
		s.priceChange(name);  }}

pubic class Stock extends AbstractStock {
	public void priceChange() {
		setName（”XOM”）;
		super.priceChange() ); }}


以后有新客户端：
Public class Ipad implements StockObserver {}
然后只要在测试里（不用改Stock和其他类了）：
Stock s = new Stock();
s.addClient(new Ipad());

JDK6里面已经提供了Observer接口，Observable类
public class ComputerClinet implements Observer{
	public void update(Observable o, Object obj){
		System.out.println(obj+" 的股票价格在电脑上更新了");
	}
}
import java.util.Observable;
public class Stock extends Observable{
	//定义股票价格变动的方法
	public void priceChange(){
		//protected  void setChanged() 
		//标记此 Observable 对象为已改变的对象
		setChanged();
		//void notifyObservers(Object arg)  ͨ 通知观察者
		notifyObservers("中国证券");		
	}
}

public class TestStock {
	public static void main(String[] args) {
		Stock s = new Stock();
		//添加观察者
		//Observable类的void addObserver(Observer o)  
		ComputerClinet cc = new ComputerClinet();
		PhoneClient pc = new PhoneClient();
		WebClient wc = new WebClient();
		s.addObserver(cc);
		s.addObserver(pc);
		s.addObserver(wc);
		s.deleteObserver(cc);
		s.priceChange();
	}
}



## Bridge

## Composite




## Façade


## Flyweight

Memory management


## Memento
Editor with undo feature
do not store history states in Editor class, instead create History
like js state management?
```shell script
public class Editor {
  private String content;

  public String getContent() {
    return content;
  }

  public EditorState createState() {
    return enw EditorState(conetent);
  }

  public EditorState restore(state) {}
}

@Data
@Builder
public class EditorState {  // memento
  private String content;
}

public class History {
  private List<EditorState> states;
  public EditorState push(state) {}
  public EditState pop() {}
}
```

## State
allow object behaves differently when state changes. using polyphorphism
open-close principle
 ```shell script
public class Canvas {  // context
  private Tool currentTool
  public mouseDown() {
    currentTool.mouseDown();
  }
  mouseUp() {
    currentTool.mouseUp();
  }
}

// interface
pulibc interface Tool {  // State
  void mouseDown();
  void mouseUp();
}

public class Selection implements Tool { // ConcreteStateA
  public void mouseDown() {}
  public void mouseUp() {}
}

public class Brush implements Tool { // ConcreteStateB
  public void mouseDown() {}
  public void mouseUp() {}
}
```

Do not abuse design patterns, keep it simple.


Udemy: Design Patterns in Java (2017, 10.5 hrs)

// creational: builder, factories, prototype, singleton
## Builder
StringBuilder
Fluent builder: lombok @Builder

## Factories
obejct creation logic becomes too convoluted, can lead to overloading hell => outsource to a separate method/class (factory, internal or external class)
```shell script
public static Point newCartesianPoint(double x, double y) {
  return new Point(x, y);
}
public static Point newPolarPoint(double rho, double theta) {
  return new Point(rho * Math.cos(theta), rho * Math.sin(theta));
}
```

## Prototype
when it's easier to copy an existing object to fully initialize a new one
an exisiting design is a prototype, make a partial/full copy (deep) and customize
```shell script
@Override
public Object clone() {
  return new Person(names.clone, address.clone);
}
```
Not recommended to implement Cloneable interface (didn't specify shallow or deep copy)
```shell script
// copy constructor
publi Address(Address other) {
  this(other.streetAddress, other.city, other.country);
}

// copy via deserialization
String addressStr = objectMapper.writeValueAsString(address);
Address addressCopy = objectMapper.readValue(addressStr, Address.class);

// ObjectsUtil
// Lombok @Builder(toBuilder = true): this is soft copy!
```


## Singleton
problems: 
- private constructor can be defeated by reflection
- can still create another instance via deserialization, to prevent:
```shell script
protected Object readResolve() {
  return SINGLETON_INSTANCE;
}
```
Or use Inner static Singleton: see [Inner Singleton](../java/2.%20Multithreading.md)

- double-checked locking
```shell script
public static LazySingleTon getInstance() {
  if (instance == null) {
    synchronized (LazySingleton.class) {
      if (instance == null) {
        instance = new LazySingleton();
      }
    }
  }
}

```
- enum based Singleton
// enum constructor is always private; when serialized, it serialize the name, not the value. So deserialize can't create the exact copy.
```shell script
enum EnumBasedSingleton {
  INSTANCE;
  private int value;
  public getValue() {
    return value;
  }
}
```

- monostate (not recommended)
make all fields static, so they are the same across all instances

- multiton
limit instance types 



structural design patterns
## Adapter
adapts an existing interface X to conform to required interface Y
```shell script
public class WebDriverAdapter implements WebDriver {
  private IeDriver ieDriver;

  @Override
  public void getElement() {
    ieDriver.findElement(); // ie has findElement()
  } 

  @Override
  public void selectElement() {
    ieDriver.clickElement(); // ie has clickElement()
  } 

}
```


## Bridge
--------- review again
a mechanism that decouples an interface (hierarchy) from an implementation (hierarchy)
```shell script
interface Renderer {
  void renderCircle(float radius);
}

class VectorRenderer implements Renderer {
  @Override
  public void renderCircle(float radius) {
    System.out.println("Drawing a circle of radius " + radius);
  }
}

class RasterRenderer implements Renderer {
  @Override
  public void renderCircle(float radius) {
    System.out.println("Drawing pixels for a circle of radius " + radius);
  }
}

abstract class Shape {
  protected Renderer renderer;

  public Shape(Renderer renderer) {
    this.renderer = renderer;
  }

  public abstract void draw();
  public abstract void resize(float factor);
}

class Circle extends Shape {
  public float radius;

  @Inject
  public Circle(Renderer renderer) {
    super(renderer);
  }

  public Circle(Renderer renderer, float radius) {
    super(renderer);
    this.radius = radius;
  }

  @Override
  public void draw() {
    renderer.renderCircle(radius);
  }

  @Override
  public void resize(float factor) {
    radius *= factor;
  }
}

class ShapeModule extends AbstractModule {
  @Override
  protected void configure() {
    bind(Renderer.class).to(VectorRenderer.class);
  }
}

class BridgeDemo {
  public static void main(String[] args) {
//    RasterRenderer rasterRenderer = new RasterRenderer();
//    VectorRenderer vectorRenderer = new VectorRenderer();
//    Circle circle = new Circle(vectorRenderer, 5);
//    circle.draw();
//    circle.resize(2);
//    circle.draw();

    // todo: Google Guice
    Injector injector = Guice.createInjector(new ShapeModule());
    Circle instance = injector.getInstance(Circle.class);
    instance.radius = 3;
    instance.draw();
    instance.resize(2);
    instance.draw();
  }
}
```


## Composite
------------ review
treating individual and aggregate objects uniformly
Foo or List<Foo> will be treated the same way
```shell script
class GraphicObject
{
  protected String name = "Group";

  public String color;
  public List<GraphicObject> children = new ArrayList<>();  // can be single GraphicObject or a list
```

Neural Networks
```shell script
interface SomeNeurons extends Iterable<Neuron> {
  default void connectTo(SomeNeurons other) {
    if (this == other) return;

    for (Neuron from : this)
      for (Neuron to : other) {
        from.out.add(to);
        to.in.add(from);
      }
  }
}

class Neuron implements SomeNeurons {
  public ArrayList<Neuron> in, out;

  @Override
  public Iterator<Neuron> iterator() {
    return Collections.singleton(this).iterator();
  }

  @Override
  public void forEach(Consumer<? super Neuron> action) {
    action.accept(this);
  }

  @Override
  public Spliterator<Neuron> spliterator() {
    return Collections.singleton(this).spliterator();
  }
}

class NeuronLayer extends ArrayList<Neuron> implements SomeNeurons {
}

class NeuralNetworksDemo {
  public static void main(String[] args) {
    Neuron neuron = new Neuron();
    Neuron neuron2 = new Neuron();
    NeuronLayer layer = new NeuronLayer();
    NeuronLayer layer2 = new NeuronLayer();

    neuron.connectTo(neuron2);
    neuron.connectTo(layer);
    layer.connectTo(neuron);
    layer.connectTo(layer2);
  }
}
```

## Decorator
augment an object with additional functionality (enriched or new methods)
```shell script
class ColoredShape implements Shape {
  private Shape shape;
  private String color;

  @Override
  public String info() {
    return shape.info() + " has the color " + color;
  }
}

// static decorator composition
// we are NOT altering the base class of these objects
// cannot make ColoredSquare, ColoredCircle
class ColoredShape<T extends Shape> implements Shape {
    private Shape shape;
    private String color;

    public ColoredShape(Supplier<? extends T> ctor, String color) {
        shape = ctor.get();
        this.color = color;
    }

    @Override
    public String info() {
        return shape + " has the color " + color;
    }
}

ColoredShape<Square> blueSquare = new ColoredShape<>(() -> new Square(20), "blue");
System.out.println(blueSquare.info());
```


## Facade
exposing several components through a single interface, for api users; hide low level details
build a facade to provide a simplfied API ooer a set of classes
abstraction?
```shell script
Console {
  // api does not need to know the details
  render() {
    Buffer buffer = new Buffer(30, 20);
    Viewport viewport = new Viewport(buffer, 30, 20, 0, 0);
    Console console = new Console(30, 20);
    console.addViewport(viewport);
  }
}
```


## Flyweight
avoid redundancy when storing data
- hightlight words: not highlight each char, but give a range of indexes to hightlight
- lots of similar names -> store names, retrieve by index, similar to datbase table, foreign key with id
```shell script
  public String getFullName() {
    return Arrays.stream(names).mapToObj(i -> strings.get(i))
      .collect(Collectors.joining(","));
  }
```


## Proxy
an interface for accessing a particular resource which may be remote, expensive to construct or may 
require logging or some other added functionality. Same interface but entirely different behavior
```shell script
class CarProxy extends Car {
  private Driver driver;

  @Override
  public void drive() {
    if (driver.age >= 17) super.drive();
    else System.out.println("Driver too young");
  }
}
```

### dynamic proxy
```shell script
class LoggingHandler implements InvocationHandler {
  private final Object target;
  private Map<String, Integer> calls = new HashMap<>();

  LoggingHandler(Object target) {
    this.target = target;
  }

  @Override
  public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
    String name = method.getName();

    if (name.contains("toString")) {
      return calls.toString();
    }

    // add or increment number of calls
    calls.merge(name, 1, Integer::sum);
    return method.invoke(target, args);
  }
}

interface Human {
  void walk();
  void talk();
}


class Person implements Human {
  @Override
  public void walk() {
    System.out.println("I am walking");
  }

  @Override
  public void talk() {
    System.out.println("I am talking");
  }
}

class DynamicLoggingProxyDemo {
  @SuppressWarnings("unchecked")
  public static <T> T withLogging(T target, Class<T> itf) {
    return (T) Proxy.newProxyInstance(
      itf.getClassLoader(),
      new Class<?>[] { itf },
      new LoggingHandler(target));
  }

  public static void main(String[] args) {
    Person person = new Person();
    Human logged = withLogging(person, Human.class); // proxy the `person`
    logged.walk();
    logged.talk();
    logged.talk();

    System.out.println(logged);
  }
}
```

Difference between decorator and proxy
- proxy provides an identical interface, decorator provides an enhanced interface
- decorator typically aggregates (or reference to) what it is decorating; proxy doesn't have to


## Chain of Responsibity
---------- review
click a button: button handles it -> group box -> window


## Command
-------- review
Encapsulate all details of an operation in a separate object, define instruction for applying the command
Optionally define instructions for undoing the command
can create composite commands (ie, macros)


## Interpreter
Interpreters are all around us. 
process structured text data -> parsing
`String input = "(13 + 4) - (12 - 1)"` => List<Token>

### ANTLR
another tool for language recognition
standard library 


## Iterator
facilitates tranverse data structure
interfaces: Interator, Interable (iterator(), spliterator())


## Mediator
facilitate communication between components, without them being aware of each other or direct access
chat room: players may go in/out anytime. ChatRoom: central place to join, receive, send messages

### Reactive extensions event broker
EventBroker: Observer, subscribe
```shell script
class EventBroker extends Observable<Integer> {
  private List<Observer<? super Integer>> observers = new ArrayList<>();

  @Override
  protected void subscribeActual(Observer<? super Integer> observer) {
    observers.add(observer);
  }

  public void publish(int n) {
    for (Observer<? super Integer> o : observers)
      o.onNext(n);
  }
}
```


## Memento
keep a memento of an object to return/rollback
command: list of changes
memento: list of states


## Null object
Not in original GOF
- we don't inject Optional<B> type
- when use, we don't check null on every call
=> no-op object, does nothing
```shell script

class Demo
{
  @SuppressWarnings("unchecked")
  public static <T> T noOp(Class<T> itf) {
    return (T) Proxy.newProxyInstance(
      itf.getClassLoader(),
      new Class<?>[]{itf},
      (proxy, method, args) -> {
        if (method.getReturnType().equals(Void.TYPE))
          return null;
        else
          return method.getReturnType().getConstructor().newInstance();
      });
  }

  public static void main(String[] args) {
    Log log = noOp(Log.class);
    BankAccount ba = new BankAccount(log);
    ba.deposit(100);
    ba.withdraw(200);
  }
}
```


## Observer
notification, old way: addXxxListener()
new: Supplier, Consumer, Function

Observer and Observable
Event: subscribe, unsubscribe
```shell script
class Event<TArgs> {
  private int count = 0;
  private Map<Integer, Consumer<TArgs>> handlers = new HashMap<>();

  public Subscription addHandler(Consumer<TArgs> handler) {
    int i = count;
    handlers.put(count++, handler);
    return new Subscription(this, i);
  }

  public void fire(TArgs args) {
    for (Consumer<TArgs> handler : handlers.values())
      handler.accept(args);
  }

  public class Subscription implements AutoCloseable {
    private Event<TArgs> event;
    private int id;

    @Override
    public void close() /*throws Exception*/{
      event.handlers.remove(id);
    }
  }
}

class PropertyChangedEventArgs {
  public Object source;
  public String propertyName;

  public PropertyChangedEventArgs(Object source, String propertyName) {
    this.source = source;
    this.propertyName = propertyName;
  }
}

class Person {
  public Event<PropertyChangedEventArgs> propertyChanged = new Event<>();
  private int age;

  public void setAge(int age) {
    if (this.age == age) return;

    boolean oldCanVote = getCanVote();

    this.age = age;
    propertyChanged.fire(new PropertyChangedEventArgs(this, "age"));

    if (oldCanVote != getCanVote()){
      propertyChanged.fire(new PropertyChangedEventArgs(this, "canVote"));
    }
  }

  public boolean getCanVote() {
    return age >= 18;
  }
}

class HandmadeEventsDemo {
  public static void main(String [] args) {
    Person person = new Person();
    Event<PropertyChangedEventArgs>.Subscription sub = person.propertyChanged.addHandler(x -> {
          System.out.println("Person's " + x.propertyName + " has changed"); });

    person.setAge(17);
    person.setAge(18);
    sub.close();
    person.setAge(19);
  }
}
```


## State
------- review
object's behavior is determined by its state
a formalized construct which manages state and transition is called a state machine.
### Spring Statemachine
```shell script
enum States {
  OFF_HOOK, // starting
  ON_HOOK, // terminal
  CONNECTING,
  CONNECTED,
  ON_HOLD
}

enum Events {
  CALL_DIALED,
  HUNG_UP,
  CALL_CONNECTED,
  PLACED_ON_HOLD,
  TAKEN_OFF_HOLD,
  LEFT_MESSAGE,
  STOP_USING_PHONE
}

class SpringStatemachineDemo {
  public static StateMachine<States, Events> buildMachine() throws Exception {
    StateMachineBuilder.Builder<States, Events> builder = StateMachineBuilder.builder();

    builder.configureStates()
      .withStates()
        .initial(States.OFF_HOOK)
        .states(EnumSet.allOf(States.class));

    builder.configureTransitions()
      .withExternal()
        .source(States.OFF_HOOK)
        .event(Events.CALL_DIALED)
        .target(States.CONNECTING)
        .and()
      .withExternal()
        .source(States.OFF_HOOK)
        .event(Events.STOP_USING_PHONE)
        .target(States.ON_HOOK)
        .and()
      .withExternal()
        .source(States.CONNECTING)
        .event(Events.HUNG_UP)
        .target(States.OFF_HOOK)
        .and()
      .withExternal()
        .source(States.CONNECTING)
        .event(Events.CALL_CONNECTED)
        .target(States.CONNECTED)
        .and()
      .withExternal()
        .source(States.CONNECTED)
        .event(Events.LEFT_MESSAGE)
        .target(States.OFF_HOOK)
        .and()
      .withExternal()
        .source(States.CONNECTED)
        .event(Events.HUNG_UP)
        .target(States.OFF_HOOK)
        .and()
      .withExternal()
        .source(States.CONNECTED)
        .event(Events.PLACED_ON_HOLD)
        .target(States.OFF_HOOK)
        .and()
      .withExternal()
        .source(States.ON_HOLD)
        .event(Events.TAKEN_OFF_HOLD)
        .target(States.CONNECTED)
        .and()
      .withExternal()
        .source(States.ON_HOLD)
        .event(Events.HUNG_UP)
        .target(States.OFF_HOOK);

    return builder.build();
  }

  // requires org.springframework.statemachine
  public static void main(String[] args) throws Exception {
    StateMachine<States, Events> machine = buildMachine();
    machine.start();

    States exitState = States.ON_HOOK;

    BufferedReader console = new BufferedReader(new InputStreamReader(System.in));

    while (machine.getState().getId() != exitState) {
      State<States, Events> state = machine.getState();

      System.out.println("The phone is currently " + state.getId());
      System.out.println("Select a trigger:");

      List<Transition<States, Events>> ts = machine.getTransitions()
        .stream()
        .filter(t -> t.getSource() == state)
        .collect(Collectors.toList());

      for (int i = 0; i < ts.size(); ++i) {
        System.out.println("" + i + ". " + ts.get(i).getTrigger().getEvent());
      }

      int choice = getUserChoice();

      // perform the transition
      machine.sendEvent(ts.get(choice).getTrigger().getEvent());
    }

    System.out.println("And we are done!");
  }

  private static int getUserChoice() {
    boolean parseOK;
    int choice = getUserChoice();
  
    do {
        try {
          System.out.println("Please enter your choice:");
    
          choice = Integer.parseInt(console.readLine());
          parseOK = choice >= 0 && choice < ts.size();
        } catch (Exception e) {
          parseOK = false;
        }
      } while (!parseOK);
  }

}
```



## Strategy
system behavior partially specified at runtime
enables the exact behavior of a system to be selected either at run-time (dynamic) or compile-time (static), also known as policy (C++)

polymorphism?

```shell script
interface ListStrategy {
  default void start(StringBuilder sb) {}
  void addListItem(StringBuilder stringBuilder, String item);
  default void end(StringBuilder sb) {}
}

class MarkdownListStrategy implements ListStrategy {
  @Override
  public void addListItem(StringBuilder stringBuilder, String item) {
    stringBuilder.append(" * ").append(item).append(System.lineSeparator());
  }
}

class HtmlListStrategy implements ListStrategy {
  @Override
  public void start(StringBuilder sb) {
    sb.append("<ul>").append(System.lineSeparator());
  }

  @Override
  public void addListItem(StringBuilder stringBuilder, String item) {
    stringBuilder.append("  <li>")
      .append(item)
      .append("</li>")
      .append(System.lineSeparator());
  }

  @Override
  public void end(StringBuilder sb) {
    sb.append("</ul>").append(System.lineSeparator());
  }
}

class TextProcessor<LS extends ListStrategy> {
  private StringBuilder sb = new StringBuilder();
  // cannot do this
  // private LS listStrategy = new LS();
  private LS listStrategy;

  public TextProcessor(Supplier<? extends LS> ctor) {
    listStrategy = ctor.get();
  }

  // the skeleton algorithm is here
  public void appendList(List<String> items) {
    listStrategy.start(sb);
    for (String item : items)
      listStrategy.addListItem(sb, item);
    listStrategy.end(sb);
  }

  public void clear() {
    sb.setLength(0);
  }

  @Override
  public String toString() {
    return sb.toString();
  }
}

class DynamicStrategyDemo {
  public static void main(String[] args) {
    TextProcessor<MarkdownListStrategy> tp = new TextProcessor<>(MarkdownListStrategy::new);
    tp.appendList(List.of("liberte", "egalite", "fraternite"));
    System.out.println(tp);

    TextProcessor<HtmlListStrategy> tp2 = new TextProcessor<>(HtmlListStrategy::new);
    tp2.appendList(List.of("inheritance", "encapsulation", "polymorphism"));
    System.out.println(tp2);
  }
}
```


## Template
a high-level blueprint for an algorithm to be completed by inheritors
Similar to Strategy which uses composition, template uses inheritance


## Visitor
---- review
add extra behaviors to entire hierarchies of classes (subclasses), need to access to the non-commmon aspects of classes
// Intrusive visitor, add print() to each class
```shell script
abstract class Expression {
  public abstract void print(StringBuilder sb);
}

class DoubleExpression extends Expression {
  public double value;

  @Override
  public void print(StringBuilder sb) {
    sb.append(value);
  }
}

class AdditionExpression extends Expression {
  private Expression left, right;

  @Override
  public void print(StringBuilder sb) {
    sb.append("(");
    left.print(sb);
    sb.append("+");
    right.print(sb);
    sb.append(")");
  }
}

class IntrusiveVisitorDemo
{
  public static void main(String[] args)
  {
    // 1+(2+3)
    AdditionExpression e = new AdditionExpression(
      new DoubleExpression(1),
      new AdditionExpression(
        new DoubleExpression(2),
        new DoubleExpression(3)
      ));
    StringBuilder sb = new StringBuilder();
    e.print(sb);
    System.out.println(sb);
  }
}
```

// reflective visitor using java reflection
```shell script
class ExpressionPrinter {
  public static void print(Expression e, StringBuilder sb) {
    if (e.getClass() == DoubleExpression.class) {
      sb.append(((DoubleExpression) e).value);
    } else if (e.getClass() == AdditionExpression.class) {
      AdditionExpression ae = (AdditionExpression) e;
      sb.append("(");
      print(ae.left, sb);
      sb.append("+");
      print(ae.right, sb);
      sb.append(")");
    }
  }
}
```

// Classic visitor (double dispatch)
but this has cyclic dependencies

```shell script
interface ExpressionVisitor {
  void visit(DoubleExpression e);
  void visit(AdditionExpression e);
}

abstract class Expression {
  public abstract void accept(ExpressionVisitor visitor);
}

class DoubleExpression extends Expression {
  public double value;

  @Override
  public void accept(ExpressionVisitor visitor) {
    visitor.visit(this);
  }
}

class AdditionExpression extends Expression {
  public Expression left, right;

  @Override
  public void accept(ExpressionVisitor visitor) {
    visitor.visit(this);
  }
}

// separation of concerns
class PrinterVisitor implements ExpressionVisitor
{
  private StringBuilder sb = new StringBuilder();

  @Override
  public void visit(DoubleExpression e) {
    sb.append(e.value);
  }

  @Override
  public void visit(AdditionExpression e) {
    sb.append("(");
    e.left.accept(this);
    sb.append("+");
    e.right.accept(this);
    sb.append(")");
  }

  @Override
  public String toString() {
    return sb.toString();
  }
}

class CalculatorVisitor implements ExpressionVisitor {
  public double result;

  @Override
  public void visit(DoubleExpression e) {
    result = e.value;
  }

  @Override
  public void visit(AdditionExpression e) // this is a test too {
    e.left.accept(this);
    double a = result;
    e.right.accept(this);
    double b = result;
    result = a+b; // this is a test
  }
}

class ClassicVisitorDemo
{
  public static void main(String[] args)
  {
    // 1+(2+3)
    AdditionExpression e = new AdditionExpression(
      new DoubleExpression(1),
      new AdditionExpression(
        new DoubleExpression(2),
        new DoubleExpression(3)
      ));
    PrinterVisitor ep = new PrinterVisitor();
    ep.visit(e);
    System.out.println(ep);

    CalculatorVisitor calc = new CalculatorVisitor();
    calc.visit(e);
    System.out.println(ep + " = " + calc.result);
  }
}
```

// acyclic visitor
```shell script
interface Visitor {}

interface ExpressionVisitor extends Visitor {
  void visit(Expression obj);
}

interface DoubleExpressionVisitor extends Visitor {
  void visit(DoubleExpression obj);
}

interface AdditionExpressionVisitor extends Visitor {
  void visit(AdditionExpression obj);
}


abstract class Expression {
  // optional
  public void accept(Visitor visitor) {
    if (visitor instanceof ExpressionVisitor) {
      ((ExpressionVisitor) visitor).visit(this);
    }
  }
}
```