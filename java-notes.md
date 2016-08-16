---
title: Java Review 複習筆記
date: 2016-07-08 20:27:51
tags: Java
---


<!-- more --> 

# 繼承與多型(Extend & Polymorphism)

__Extend__: 其實就是為了DRY, 不要讓一段的 code 重複出現在其他地方。

把共用的methods/attributes 提升到 parent class.

Java裡面的 `is-a`  ， 用來判斷一個 child-object 是否屬於 parent-object的關係

舉例：`SwordsMan繼承了Role，所以SwordsMan是一種Role（SwordsMan is a Role），Magician繼承了Role，所以Magician是一種Role（Magician is a Role）。`



    SwordsMan swordsMan = new SwordsMan();
    Magician magician = new Magician();

__Case 1__

    Role role1 = new SwordsMan();
    Role role2 = new Magician();

__Case 2__

    SwordsMan swordsMan = new Role();
    Magician magician = new Role();

To know the answer: you should read the statement from right to left.

從右邊讀到左邊。

__Case 1__

SwodsMan __is_a__ role1 ? (Sure)

    Role role1 = new SwordsMan();
    Role role2 = new Magician();

__Case 2__

Role __is_a__ SwordsMan? (No!)

    SwordsMan swordsMan = new Role();   
    Magician magician = new Role();


下面的 snippet 會在第二行失敗，

原因同上。要解掉的話就是強制cast

    Role role1 = new SwordsMan();
    SwordsMan swordsMan = role1;

# 實際使用範例

可以讓不同的class之間的object,透過 upcast 到同一個parent class,

去呼叫同一個方法。如此一來就不用於每個 child class 各自override 一套 showBlood 方法

    public class RPG {
        public static void main(String[] args) {
            SwordsMan swordsMan = new SwordsMan();
            swordsMan.setName("Justin");
            swordsMan.setLevel(1);
            swordsMan.setBlood(200);
            Magician magician = new Magician();
            magician.setName("Monica");
            magician.setLevel(1);
            magician.setBlood(100);
            showBlood(swordsMan);
            showBlood(magician);
        }
        static void showBlood(Role role) {
            System.out.printf("%s 血量 %d%n",
                    role.getName(), role.getBlood());
        }
    }

至少上面的方法，你不需要寫 N種 showBlood(SwordsMan x), showBlood(Magician y), ....


# 什麼叫多型？以抽象講法解釋，就是使用單一介面操作多種型態的物件！

這種作法 在 DUCK TYPE 隨處可見的 Pyhton/Ruby 世界裡面早就用到爛了 XD

[REF](http://openhome.cc/Gossip/Java/Polymorphism-is-a.html)

# Inner class

在Android click事件中，常常會看到這種寫法。

Inner class : 它可以存取外部類別static成員，但不可存取外部類別非static成員。


# Variable length arguments

![REF](http://openhome.cc/Gossip/Java/Variable-lengthArgument.html)

其實根本就只是把argument 變成 array 型態而已，實際上無異。

    public static int sum(int... numbers) {
        int sum = 0;
        for(int number : numbers) {
            sum += number;
        }
        return sum;
    }



# Functional

functional interface 只會有一個 funciton. (p71.)

P77 要練習



# @Override

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


# String 

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


# References

[JAVA 面試考題](https://dongchuan.gitbooks.io/java-interview-question/content/java/polymorphism.html)

[Java：筆記](http://rickchungtw-blog.logdown.com/posts/177261-java-note#s3-1)