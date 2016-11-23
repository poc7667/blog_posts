---
title: ios-notes
date: 2016-07-21 19:02:55
tags: iOS
---


Notes for learning iOS / Swift 

- Optional


<!-- more --> 


2016-08-04

# Autolayout

- Autolayout

 Leading and trailing (左右的距離，但是會根據不同語系而改變 eg:希伯來就是右到左)


Flexible constraints: 盡量使用。 少用 rigid constraints











# NS XXXX



NS系列是 next step 縮寫， 從foundation 過來的

let 再這邊並不會 immutable

NSString, NSArray, ... are immuatable. 這些都是object,再swift 是struct

NSString ~ String (interchangeably)

    import Foundation

    let x: NSArray = ["x", "y", "z"] // NSArray has to hold Objects, so "x" is a NSString 

Dictionary always returns __optional__

數字不要說 cast,trancation


# Adv String

API 在3.0 有改變，

advanced 的方法要去了解。

一個character 不代表一個 byte 而是代表一個 humman readable char 為單位，有可能是1~N byte


# Adv tuples

可以用在 switch 比對

decouple 

    x = (0,1,2)
    (a,b,_) = x 
    a //0
    b //1
    c //2

# Sets

String, 是一個 structure.

structure 無法繼承

    var tools: Set<String>
    tools = ["A", "B", "C"]




# Dictionary

    var wc: [String: INt]
    wd = [String: Int]() // new a dictionary

你去跟 dictionary 拿一個 value, 回傳的一定都是 `optional`

is a kind of `structure`.



# Array

Strongly type, 

    var a = [String]() // new 一個 array, ()代表initialize
    a.append("poc")

is a kind of Structure,

其實你也可以讓裡面的item 保持 `any`, `anyObject`

pass by value, cuz its kind of Array


# Struct vs. Object 

Struct alwasy call by value 

Object call by reference.

如果你要讓 object 本身是 immutable 你可以嘗試 new struct 在給予 let

mutating 除了給 compiler 看，也給人看。

提示給compiler，說這個 function 會change some values.


    class Person{
        var yoyo: Person? <- recursive prop. (不可以在struct 裡面使用)
    }

## tuple (pass by value)

simple unnamed struct.

    var x: (1,2,4)

呼叫方式就是用 index 方式 access, x.0 , x.1

但是你也可以擁有 named tuple 

    var x: (itemA: Int, itemB: Int)
    x = (2, 0)
    x.itemA





# Optional

只有 Optional 可以有 nil, 如果 nil 被 assigned for some vars, 會被自動推斷為 Optional

Optional 當你不確定 value 時候使用。

Optional 是一個 container, 他不是屬於某種特定type 就是nil

nil 不等於 zero or false.

Int("123")// ; 不要解讀成強制轉型，想成 Type initializer, 把class 想成 Type

能不用 optional 就不用 optional , optional 會讓程式複雜化。

## Optional binding

    let x : Int? = 8-3
    var y: Int

// 如果 x is not nil, 有值的話 assign to var `foo` 並且執行接續的block

    if let foo = x {
        y = foo
    }


## Nil Coalescing Operator 

`??` : unwraps an optional if there is a value, or a default value

    let a: Int? = nil
    let b: Int = 17
    let x: Int = a ?? b


established type win 
 w = (Int) 1
 z = (Float) 1.0
 a = (1/5) * w ;  全部轉型為 int
 b = (1/5) * z ;  全部轉型為 float

# guard


    guard <condition to meet> else {
        // 執行假如條件沒有匹配要做的動作
    }
    // 繼續執行一般的動作


    func printInfo(article: Article) {
        guard let totalWords = article.totalWords where totalWords > 1000 else {
            print("Error: Couldn't print the total word count!")
            return
        }
        guard let title = article.title else {
            print("Error: Couldn't print the title of the article!")
            return
        }
        print("Title: \(title)")
    }

#  try / throw / catch


    let request = NSURLRequest(URL: NSURL(string: "http://www.apple.com")!)
    var response:NSURLResponse?
    var error:NSError?
    do {
        let data = try NSURLConnection.sendSynchronousRequest(request, returningResponse: &response)
        print(response)
        // Parse the data
    } catch {
        // handle error
        print(error)
    }

# var as? String 以及 var as String? 差異

`VAR as? String` : var 可以是任意 type, array, etc. 如果他是string 就把它 cast 為string, 如果不是的話 請幫我 set to `nil`

`VAR as String?` : VAR is a `String?` 就是你熟悉的 optional, 如果不是 string 的話 , runtime 解開會有 exception.

    var x: AnyObject? = "Test"
    x as String? // OK, the result is an optional string
    x as? String // OK, evaluates to an optional string
    "string" as String? // OK, evaluates to optional string
    x as? Int // OK, evaluates to nil, it's not an Int
    x as Int? // Runtime exception, it's not castable to optional Int


 The real difference is between `as?` and `as`: the former is an attempt to cast, the latter is a forced cast, resulting in runtime error if not possible.

 `as?`:嘗試cast
 `as`: 強迫cast, 會出錯的。

 現在還有 `as!`

-  as! : downcast, convert to 子類別
-  as? : same as as! 只是失敗的時候不會 fail, 會回傳 nil
-  as : upcast, convert to 父類別


# 擴展協定 extension (open class and add new features)


# JSON

處理 JSON 的好作法




# References

    http://www.appcoda.com.tw/swift2/
    http://www.hangge.com/blog/cache/detail_1089.html

