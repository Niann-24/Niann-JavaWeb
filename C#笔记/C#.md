

## 匿名类的对象 

好处：	使用匿名类对象可以简化代码

普通方法创建方法并调用

```c#
 internal class Program
    {
        void show()
        {
            int ID = 1;
            String Name = "王富贵";
            Console.WriteLine("我是show方法"+ID+","+Name);
        }
        static void Main(string[] args)
        {
            Program p = new Program();
            p.show();
        }
    }


    我是show方法1,王富贵
```



使用匿名内部类创建方法并调用

```c#
static void Main(string[] args)
        {
            var method = new { ID = 1,Name="王富贵 };

            Console.WriteLine("我是show方法"+method.ID+","+method.Name);

            Console.Read();
        }
    
    
      我是show方法1,王富贵
```



## 两种基本类型  

众所周知在c#中有两种基本类型，它们分别是**值类型**和**引用类型**

值类型：**byte，short，int，long，float，double，decimal，char，bool 和 [struct](https://so.csdn.net/so/search?q=struct&spm=1001.2101.3001.7020) 统称为值类型。**
<!--说到传值时，实际过程是，对这个变量进行全克隆/拷贝，然后传递这个副本，原始值不变。结构体就是值类型，它是传值的。这意味着，结构体是理想的小型数据结构。 值类型在“栈”的分配，这意味着它们的内存很容易被回收，它们不受“垃圾回收”的影响。和Update循环例子中的引用类型不同，创建值类型是完全合理的，它们超出作用域也不必担心效率或内存问题-->

引用类型：**需要实例化的类都是引用类型**
 <!--当说到类的实例是传引用时，实际过程是，先获取一个指针，它指向对象在内存中的地址，然后传递这个指针。这很重要，因为一个类的实例，实际上可能很大，包含了很多域甚至其他对象。在这种情况下，赋值和传递整个实例可能非常影响性能，这就为什么要用传地址来替代。引用类型在“堆”上分配，在调用“垃圾回收”时被清理。垃圾回收是一个自动的过程，但是它很慢-->

**装箱**：将值类型转换为引用类型-----简单地说，**装箱**就是将一个值类型的数据存储在一个引用类型的变量中。
**拆箱：**将引用类型转换为值类型

```c#
 static void Main(string[] args)
        {
            //装箱
            int val = 100;
            object str = val;
            Console.WriteLine(str);
            //拆箱
            int num = (int)str;
            Console.WriteLine(num);
        }
```





**形参和实参**：

**形参**全称叫做“形式参数”，也是一个虚拟的参数，在定义方法的时候使用的参数，形参是方法被调用时用于接收实参值的变量。

**实参**全称叫做“实际参数”，顾名思义就是实际存在的参数，实参可以是常量、变量、表达式、类等，实参必须要有确定的值。



```C#
 class Demo {
        static void sum(int a,int b) {//这里边的int a,int b 就是形参 
            Console.WriteLine(a+b);
        }
        static void Main(string[] args)
        {
            sum(4, 6);//这里的4和6就是实参
            Console.Read();
        }
    }
```



------

**out:**在一个方法中返回**多个不同类型**的值

​	需求：写一个方法求一个数组的最大值和最小值


```C#
 static void Main(string[] args) 
        {
            int[] arrs = {1,2,3,4,5};

            show(arrs);
            Console.WriteLine("最大值是:"+show(arrs)[0]+"\t最小值是："+show(arrs)[1]);
            Console.ReadKey();
        }

        public static int [] show(int[] arr) {
            int max = arr[0];
            int min = arr[1];
            int[] List = new int[2];
            foreach (var i in arr) {
                if (max < i) {
                    max = i;
                }
                if (min>i) {
                    min = i;
                }
            }
            List[0] = max;
            List[1] = min;
            return List;
        } 
```



产品经理需求加1：show方法里定义一个字符串=蔡徐坤并返回 

```c#
  static void Main(string[] args)
        {
            int[] arrs = {1,2,3,4,5};
            int max = 0;
            int min = 0;
            String Name = null;
          
            method(arrs,out max,out min,out Name);
            Console.WriteLine(max);
            Console.WriteLine(min);
            Console.WriteLine(Name);
            Console.Read();
           
        }

        public static void method(int[] arr,out int max,out int min,out string Name) {
            //out要求在方法内部为其赋值
            max = arr[0];
            min = arr[1];
            Name = "蔡徐坤";
            int[] List = new int[2];
            foreach (var i in arr)
            {
                if (max < i)
                {
                    max = i;
                }
                if (min > i)
                {
                    min = i;
                }
            }
        }
```



 输入账号和密码判断是否正确，返回用户输入的结果,登入成功或返回用户名错误，或密码错误

```C#
 internal class Program
    {
         String uname = "admin";
         String upwd="123456";


        static void Main(string[] args)
        {
            Console.WriteLine("请输入账号");
            var uname = Console.ReadLine();
            Console.WriteLine("请输入密码");
            var upwd = Console.ReadLine();
            Program p1 = new Program();

            string msg = null;
            if ( p1.Login (uname, upwd,out msg)  )
            {
                Console.WriteLine(msg);
            }
            else {
                Console.WriteLine(msg);
            }
            Console.Read();
        }


       private bool Login(string uname,string upwd,out String msg) {

            if (uname==this.uname && upwd==this.upwd) {
                msg = "登入成功";
                return true;
            }
            if (uname != this.uname)
            {
                msg = "用户名错误";
            }
            else {
                msg = "密码错误";

            }
            return false;
        
        }

       

    }
```



需求：年年的工资是五千，定义一个奖金，每次调用加五百，再定义一个罚款每次调用减五百

------



```c#
 static void Main(string[] args)
        {
            decimal wage = 5000;
            jiangjin(ref wage);
            Console.WriteLine(wage);
            Console.Read();
        } 

        static void jiangjin(ref decimal a) {
            a += 500;
        }

        static void Fak(ref decimal a) {
            a -= 500;
        }
```

ref:可以在方法中改变变量的值

------



## 方法重载

方法名相同，方法参数不同
作用：简化代码

需求：写一个整数相加的方法，一个小数相加的方法和一个字符串相加的方法





## 构造方法

1. 方法名与类名相同
2.  在方法名的前面没有返回值类型的声明
3.  在方法内部不能使用return语句进行返回

作用：实例化对象的同时对属性（字段）进行赋值(初始化对象)
构造方法可以重载

```c#
 internal class Program
    {
        public string Name;
        public int Age;

        public Program(String Name,int Age) {
            this.Name = Name;
            this.Age = Age;
        }

        static void Main(string[] args)
        {
            Program p1 = new Program("蔡徐坤",18);
            Console.WriteLine(p1.Name+","+p1.Age);
            Console.Read();
        }

    }
```







## 属性

作用：属性可以访问私有成员变量

```C#
 internal class Program
    {

        static void Main(string[] args)
        {
            Login L1 = new Login();
            L1.Login_uname = "ABS";
            var uname = L1.Login_uname;
            var upwd = L1.Books;
            Console.WriteLine(uname);

            Console.WriteLine(upwd);
            Console.Read();
        }

    }

    class Login 
    {
        private string uname="admin";
        private string Book = "悲惨世界";


        public string Login_uname
        {
            get { return uname; }
            set { uname = value; }
        }

        public string Books {
            get { return Book; }
        }



    }
```

```c#
  internal class Program
    {

        static void Main(string[] args)
        {
            Login L1 = new Login();
            L1.Login_uname = "ABS";
            var uname = L1.Login_uname;
            var upwd = L1.Books;
            Console.WriteLine(uname);

            Console.WriteLine(upwd);
            Console.Read();
        }

    }

    class Login 
    {
        private string uname="admin";
        private string Book = "悲惨世界";


        public string Login_uname { ge
```

**在c#6.0中属性可以这样设置**

```C#
  internal class Program
    {

        static void Main(string[] args)
        {
            Login L1 = new Login();
            L1.Login_uname = "ABS";
            var uname = L1.Login_uname;
            var upwd = L1.Books;
            Console.WriteLine(uname);

            Console.WriteLine(upwd);
            Console.Read();
        }

    }

    class Login 
    {
        private string uname="admin";
        private string Book = "悲惨世界";


        public string Login_uname { get; set; }
        public string Books { get; }

    }
```



## 索引器(难点)

索引器是C＃的一项特殊功能，可以将对象用作数组。 如果在类中定义索引器，则其行为将类似于虚拟数组。 索引器在C＃中也称为智能数组。 它是一个类属性，允许使用数组功能访问数据成员。 

索引器简单来说就是**把对象当成数组使用**

**索引器类型**表示该索引器使用哪一类型的索引来存取数组或集合元素，可以是整数，可以是字符串；this表示操作本对象的数组或集合成员，可以简单把它理解成索引器的名字，因此索引器不能具有用户定义的名称。

```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp6
{

    class Z
    {
        //可容纳100个整数的整数集
        private long[] arr = new long[10];

        //声明索引器
        public long this[int index]
        {
            get
            { //检查索引范围
                if (index < 0 || index >= 10)
                {
                    return 0;
                }
                else
                {
                    return arr[index];
                }
            }
            set
            {
                if (!(index < 0 || index >= 10))
                {
                    arr[index] = value;
                }
            }
        }

    }

    class Test
    {
        static void Main(string[] args)
        {
            Z z1 = new Z();
            z1[0] = 5;
            Console.WriteLine(z1[0]);
		//	索引器可以通过下标和字符查找
            //通过下标查找
            Console.WriteLine(z1[5]);
            Console.Read();
        }
    }
    
}

```





## 枚举类型

是由基础[整型](https://so.csdn.net/so/search?q=整型&spm=1001.2101.3001.7020)数值类型的一组命名常量定义的值类型。 若要定义枚举类型，请使用 **enum** 关键字并指定枚举成员,枚举列表每个符号代表一个整数值

例题：使用枚举类型表示周一到周日

```C#
enum Days
{ 
    day1,
    day2,
    day3,
    day4,
    day5,
    day6,
    day7
}

class Test {
    static void Main(string[] args)
    {
        Days d1 = Days.day1;
        d1 = Days.day2;
        Console.WriteLine(d1);
        Console.Read();
    }
}
```



## 结构体

**结构体是一个类似于类的<u>数据类型</u>**

### **<u>结构体跟类不同的地方：</u>**

1. 结构体是值类型，无需进行堆分配，类是引用类型，**Class为引用类型，[Struct](https://so.csdn.net/so/search?q=Struct&spm=1001.2101.3001.7020)为值类型**

2. 结构类型的变量直接存储数据结构，而类类型的变量存储对动态分配的对象的引用*

3. **类支持继承，结构体不支持继承关键字**

4. **类是Class，结构体是Struct**

5. **结构体里的字段不可以赋值**，如果要赋值必须 **通过构造方法进行赋值**

6. 结构体的作用是对一些信息进行整合 **简化代码**

   

需求定义三个学生，他有四个字段：Name，Age,Sex,StuID

**如何定义一个结构体**

```C#
 struct StudentInfo {
    private String Name;
    private int Age;
    private char Sex;
    private int StuID;
    }
}
```

```C#
//需求定义三个学生，他有四个字段：Name，Age,Sex,StuID






struct StudentInfo {
        private String Name;
        private int Age;
        private char Sex;
        private int StuID;

        static void Main(string[] args)
        {
            StudentInfo s1 = new StudentInfo();
            s1.Age = 18;
            s1.Name = "蔡徐坤";
            s1.Sex='男';
            s1.StuID = 1;
        }
    }
```

 

结构体里可以定义方法

```c#
 struct StudentInfo {
        private String Name;
        private int Age;
        private char Sex;
        private int StuID;

        void method() {
            Console.WriteLine("我叫{0},{1},{2}岁,学号ID是：{3}",Name,Sex,Age,StuID);
        }

        public StudentInfo(String Name,int Age,char Sex,int StuID) {
            this.Name = Name;
            this.Age = Age;
            this.Sex = Sex;
            this.StuID = StuID;
        }

        static void Main(string[] args)
        {
            StudentInfo s1 = new StudentInfo("蔡徐坤",18,'男',001);
            s1.method();
            StudentInfo s2 = new StudentInfo("王富贵",20,'男',002);
            s2.method();
            Console.Read();
        }
    }

```









## 委托(delegate)：

委托是一个类，它定义了方法的类型，使得可以将方法当作另一个方法的参数来进行传递，这种将方法动态地赋给参数的做法,使得程序具有更好的可扩展性。委托是为事件做准备的	
注意：返回值一致，参数列表一致

```C#
    delegate int MyDelegate(int a, int b);//定义了一个委托
    delegate void MyDelegate2();
    class Test {

      static  int max(int a,int b) {
            return a > b ? a : b;
       }

        static int min(int a,int b) {
            return a < b ? a : b;
        }

        static void show() {
            Console.WriteLine("show");
        }
        static void Main(string[] args)
        {
            MyDelegate my1 = max;
            MyDelegate2 my2 = show;
            Console.WriteLine(my1(1, 3));
            my2();
            Console.Read();
        }
       
    }
```

### 多播委托

```C#
  static void show() {
            Console.WriteLine("show");
        }

        static void method() {
            Console.WriteLine("method");
        }
        static void Main(string[] args)
        {
            MyDelegate2 my2 = show;
            my2 += method;
            my2();
            Console.Read();
        }
```

​	委托例题：假如有两个人合伙开发游戏，其中A程序员他开发主角，B程序员开发菜单UI(菜单栏，提示的UI画面)

```C#
  delegate void delegateDie();
    class Game {
        //A
        static void play(delegateDie Die) 
        {
            Console.WriteLine("做任务");
            Console.WriteLine("玩家在战斗");
            Console.WriteLine("死亡");
            //给他提供一个接口，在主角死亡的时候调用函数--委托

            if (Die !=null) { 
                 Die();
            }
            
        }

        //B
        static void showDieUi() {
            Console.WriteLine("显示游戏死亡后的UI");
            Console.WriteLine("返回首页UI");
        }
        static void Main(string[] args)
        {
            play(showDieUi);
            //不想让他做任何事就传递一个Null 
            //play（null)
            Console.Read(); 
        }
    }
```





## 递归

**套娃，**(方法)**我调我自己**
注意：需要有结束语句













