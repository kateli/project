# 两大编程思想

用面向过程的方法做出来的程序就像是一份蛋炒饭。面向对象的方法做出来的程序，就像是一份盖浇饭。

##### 面向过程

面向过程（pop）：分析解决问题所需要的步骤，然后把这些步骤一步步的实现。使用的时候，再一个个的调用。
例如：把大象装进冰箱，分为三步：
* 打开冰箱门
* 把大象放进去
* 关上冰箱门

###### 特性

* 优点：性能比面向对象高，适合跟硬件联系很紧密的东西。例如单片机就采用的是面向过程编程。
* 缺点：没有面向对象易维护，易复用，易扩展。

##### 面向对象

面向对象（oop）：把事务分解成一个个的对象，然后由对象之间进行分工与合作。在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工。面向对象编程具有灵活，代码可复用，容易维护和开发的优点，更适合多人合作的大型软件项目。
例如：把大象装进冰箱，按照面向对象的做法
1. 大象对象
	* 进去
2. 冰箱对象
	* 打开
	* 关闭
3. 使用大象和冰箱的功能

###### 特性

* 封装性：代码封装
* 继承性：比如两个对象，父亲和儿子，儿子可以继承父亲的一些属性和方法，例如姓是继承父亲的。
* 多态性：同一个对象，不同的时刻，可以提现不同的状态
* 优点：易维护，易复用，易扩展，由于面向对象有封装，继承，多态性的特性，可以设计出低耦合的系统。使系统更加灵活，更加易于维护
* 缺点：性能比面向过程低

###### 思维特点

1. 抽取对象公用的属性和行为组织（封装）成一个类（模板）
2. 对类进行实例化，获取类的对象