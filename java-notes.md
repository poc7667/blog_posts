---
title: java-notes
date: 2016-07-08 20:27:51
tags: Java
---

要去看這邊的 code /Users/poc/workspace/courses-UCSC/java-comprehensive/resources/Demo Codes


<!-- more --> 

# 2016-08-12

Demoday7 , dbtestapp.

DBCreaterApp


# exception

unchecked exception: like Array outofboundary exception, you don't have to write exception handling.
checked exception: 有些程式寫法，你一定要準備 exception, otherwise the compiler will blame you.

# I/O



facade pattern: 物質本身沒有改變、只是在外面__加上__一層。
Design Pattern

Decorator: 不改變原來行為，額外附加上去



# Array

primitive type array 在new 的時候，就把空間建立好。

objects of array 在new 的時候，會建立好 array 的時候，就把空間建立好。
但是object的空間、還沒有去 initializer

    Product[] products = new Product[5];

# Functional

functional interface 只會有一個 funciton. (p71.)

P77 要練習



# 2016-07-22

寫出 @Override 可以避免手殘變成 Overloading, compiler 會提示你幫你檢查  

    @Override
    public String toString(){
        return "Parent():"+super.toString()+"overrite string";
    }


super() 一定要放在最前面

![inline](https://i.imgur.com/Y0K3ixe.png=300x "Title")

[Polymorphism upcast/downcast](http://slashlook.com/articles_20130711.html)

Java downcast/upcast 要去搞懂。

子孫認得祖先，祖先不認得子孫（硬要來的話只可以 explicit castc）

    Object o = new Software();
    Software s = o; //a compiler error would occur


Parent 沒可能 downcast 成為 child
![inline](https://i.imgur.com/hKEcLTG.png=300x "Title")


# 2016-07-15

Object has __state__ , __behaviour__ (public methods)


Person toater = new Person("poc");

// new 這個關鍵字讓memory allocate delayed 執行，JVM runtime 再去 allocate memory.


重要觀念：

- Abstraction: is a technique which helps identify which information can be hidden

- Encapsulation is the result of information hiding

JAVA primitive 交換, 字串交換, obj裡面的attributes 交換 要了解。


default value at 物件裡面會被init，但是在 local 就沒有init。

To ensure a object is immutable, you should make sure all its members are immutable


String API:

* String builder 

String inturned: [stkoverflow](http://stackoverflow.com/questions/10578984/what-is-string-interning)

[http://tech.meituan.com/in_depth_understanding_string_intern.html](http://tech.meituan.com/in_depth_understanding_string_intern.html)


# 2016-07-08

static method : 

- Can not use NON-static vars, methods
- Can use obj references and class names

        class A {
            int e; // instance var
            static int i; // class var    
        }

Exception 流程

        Scanner sc = new Scanner();
        try{
            System.out.println("enter total:");
            double sub_total = sc.nextDouble();
        }catch(InputMismatchException e)
        {
            sc.next(); //eat newline
            System.out.println("retry again");
            continue;
        }

複習一下 try catch, throw, thorws, finally

https://segmentfault.com/a/1190000004681136

Use `hasNextDouble`, `hasNextInt` to replace `try...catch()`. it costs less!

# String/Number formatter



# CompareNumber

    if (xxxNum.isEmpty())

# CompareString

    if (String.new.compareToIgnoreCase())
