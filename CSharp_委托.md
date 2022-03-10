- 在CSharp中，委托是一个类（Class），我们定义一个委托，
  查看它的IL代码委托是一个类  Type t = typeof(DelegateName);
```CSharp
public delegate void Feedback();
class Program
{
    static void Main(string[] args)
    {
        Type t = typeof(Feedback);
        // 使用IsClass判断是否是类，返回True
        Console.WriteLine(t.IsClass);   
    }
}
```

通过IL也可以看到，编译器定义了一个MyDel类，它继承自MulticastDelegate，并且包含BeginInvoke（异步调用），EndInvoke和Invok（同步调用）三个方法。这个类的可访问性是public，这是因为定义的委托是public类型，由于委托是类，所以但凡能够定义类的地方都能定义委托。

IntPtr是什么类型？
它被设计为一个整数，但是大小根据当前平台来确定的，它可以用来容纳指针或句柄。


## C# Action与Delegate、Event和Func的差异

- Action是一个泛型的委托，其内部即使用delegate去实现，当普通的delegate定义的参数与Action个数、类型一致时，两者实现的功能是一样的。只是Action的方式更加简洁、规范。

　　1. delegate

    delegate我们常用到的一种声明

　　  Delegate至少0个参数，至多32个参数，可以无返回值，也可以指定返回值类型。

　　  例：public delegate int MethodtDelegate(int x, int y);表示有两个参数，并返回int型。

　　(2). Action

       Action是无返回值的泛型委托。

　　 Action 表示无参，无返回值的委托

　　 Action<int,string> 表示有传入参数int,string无返回值的委托

 　　Action<int,string,bool> 表示有传入参数int,string,bool无返回值的委托

       Action<int,int,int,int> 表示有传入4个int型参数，无返回值的委托

　　 Action至少0个参数，至多16个参数，无返回值。

   (3). Func

　　 Func是有返回值的泛型委托

　　 Func<int> 表示无参，返回值为int的委托

　　 Func<object,string,int> 表示传入参数为object, string 返回值为int的委托

　　 Func<object,string,int> 表示传入参数为object, string 返回值为int的委托

　　 Func<T1,T2,,T3,int> 表示传入参数为T1,T2,,T3(泛型)返回值为int的委托

　　 Func至少0个参数，至多16个参数，根据返回值泛型返回。必须有返回值，不可void

    (4) .predicate

　　 predicate 是返回bool型的泛型委托

　　 predicate<int> 表示传入参数为int 返回bool的委托

　　 Predicate有且只有一个参数，返回值固定为bool

　　 例：public delegate bool Predicate<T> (T obj)

 

Action可以直接作为无返回值得委托事件的写法。

Func是有返回值的。

public delegate void DoDelegate(object parm);
public DoDelegate DoMethod;
 
public Action<object> doAction4OneParm;
public Action<object, object> doAction4TwoParm;
Public Func<object,bool>  DoFuncOneParam;(返回值是bool)