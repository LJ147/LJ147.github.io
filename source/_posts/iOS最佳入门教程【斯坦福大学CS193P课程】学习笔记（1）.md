---
title: iOS最佳入门教程【斯坦福大学CS193P课程】学习笔记（1）
date: 2017-03-6 12:25:31
tags:  
- iOS
- Swift
layout: page
updated: 2017-07-26 12:25:31
description: 【斯坦福大学CS193P课程】的全部代码 以及学习中遇到的问题
category: 开发笔记

---
斯坦福大学CS193P课程的全部代码以及学习中遇到的问题
 
## 本系列文章主要内容：
* 【斯坦福大学CS193P课程】的全部代码（分章节）
*   记录学习此课程中遇到的一些问题
*  分享该课程的高清视频&pdf资源（文尾）

***
<!-- more -->

## 1.一位大神对于这门课程的大力推荐
![iOS行业领跑人——唐巧给出的建议.png](https://ws2.sinaimg.cn/large/006tKfTcly1fs3uyf3ovtj30yg0h7tiq.jpg)
之前确实是看的这白胡子爷爷的这一系列视频入门，现在刚好重新回顾记录一下。

***
## 2.源代码部分：  因为涉及到storyboard的相关操作，所以将项目打包放在了文尾

![项目结构.png](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uyg04ijj308f0a63zg.jpg)

**本章节功能：iOS版本的支持加减乘除、一元二元运算的计算器**
![最终效果.png](https://ws4.sinaimg.cn/large/006tKfTcly1fs3uygyan5j30ku12atb5.jpg)

``` swift
    CalculatorBrain.swift

//
//  CalculatorBrain.swift
//  Calculator
//
//  Created by Alex LJ on 2017/3/5.
//  Copyright © 2017年 Stanford University. All rights reserved.
//

import Foundation
enum Optional<T>{
    case None
    case Some(T)
}

func multiply(op1:Double,op2:Double)->Double{
    return op1*op2
}
class CalculatorBrain
{
    
    private var accumulator = 0.0
    func setOperand(operand:Double) {
        accumulator  = operand
    }
     //操作类型  重点掌握这里的Swift特性 简易和类型推断
    private var operations :Dictionary<String,Operation> = [
        "π":Operation.Constant(M_PI),//M_PI
        "e":Operation.Constant(M_E), //M_E
        "±":Operation.UnaryOperation({ -$0 }), //minus
        "√":Operation.UnaryOperation(sqrt), //sqrt
        "cos": Operation.UnaryOperation(cos), //cos
        "×":Operation.BinaryOperation({ $0 * $1 }),
        "÷":Operation.BinaryOperation({ $0 / $1 }),
        "+":Operation.BinaryOperation({ $0 + $1 }),
        "−":Operation.BinaryOperation({ $0 - $1 })

    ]
    
    enum Operation{
        case Constant(Double) //常数
        case UnaryOperation((Double)->Double)   //单操作符  函数作为一个参数传值
        case BinaryOperation((Double,Double)->Double)  //双操作数
        case Equals           //等于
    }
    
    //执行运算操作
    func performOperand(sympol:String){
        
        if let operation = operations[sympol]{
            switch operation {
            case .Constant(let value):accumulator = value

            case .UnaryOperation(let function): accumulator = function(accumulator)
            case .BinaryOperation(let function):
                excutePendingBinaryOperation()
                pending  = PendingBinaryOperationInfo(binaryFunction: function, firstOperand: accumulator)
            case .Equals:
                excutePendingBinaryOperation()
               
            }
        }
        
    }
    
    private func excutePendingBinaryOperation(){
        if pending != nil {
            accumulator = pending!.binaryFunction(pending!.firstOperand,accumulator)
            pending = nil
        }
    }
    
    private var pending: PendingBinaryOperationInfo?
    
    private struct PendingBinaryOperationInfo{
        var binaryFunction:(Double,Double)->Double
        var firstOperand:Double

    
    }
    //运算结果
    var  result: Double{
        get{
            return accumulator
        }  
    }
}
``` 

    ViewController.swift
``` swift
 //
//  ViewController.swift
//  Calculator
//
//  Created by Alex LJ on 2017/3/4.
//  Copyright © 2017年 Stanford University. All rights reserved.
//

import UIKit

class ViewController: UIViewController {
     //显示框
    @IBOutlet private weak var display: UILabel!
    
     var userIsInTheMiddleOfTyping   = false
     //点击数字后的执行函数
    @IBAction private  func touchDigit(_ sender: UIButton) {
        let digit = sender.currentTitle!
        if userIsInTheMiddleOfTyping {
            let textCurrentlyInDisplay = display.text!
            
            display.text = textCurrentlyInDisplay + digit
            
        }else{
            display.text = digit
        }
        userIsInTheMiddleOfTyping = true
    }
     //展示数值
   private var disPlayValue:Double{
        get{
            return Double(display.text!)!
        }
        set{
            display.text = String(newValue)
        }
    }
     //brain实例
    private var brain = CalculatorBrain()
    
     //执行
    @IBAction private func performOperation(_ sender: UIButton) {
        if userIsInTheMiddleOfTyping{
            brain.setOperand(operand: disPlayValue)
            userIsInTheMiddleOfTyping = false
        }
        if let mathmathicalSymbol = sender.currentTitle{
           brain.performOperand( sympol: mathmathicalSymbol)
        }
       disPlayValue = brain.result
    }
  
    
}

```

***
## 3.遇到的困难
*  UI使用自适配时选择的一些处理需要十分仔细，极其容易出错，唯一的办法大概就是仔细重复观看视频。

***
## 4.完整项目地址打包下载方式
 
 * 本章节代码链接: https://pan.baidu.com/s/1hsFoF5q 密码: ap7i

![资料截图.png](https://ws3.sinaimg.cn/large/006tKfTcly1fs3uyhvnsvj30yg0mtagl.jpg)
参考：
1.* [唐巧公众号文章原文](#http://mp.weixin.qq.com/s?__biz=MjM5NTIyNTUyMQ==&mid=2709545345&idx=1&sn=7f344de17873cca515e5098df15af56d&chksm=828f0b5fb5f88249620e8e50e076a48cacd6fe1ae7770129a729ad1b0415ba1957437a493965&mpshare=1&scene=23&srcid=0306hvhCgblOMXOamy7g1Sko#rd)
2.* [Apple斯坦福大学CS193P课程（需梯子 不然很慢）](#https://itunes.apple.com/us/course/developing-ios-9-apps-with-swift/id1104579961)

行文仓促，多有不足之处，若有错误、不当之处，还请斧正。

[个人主页](http://www.hellogod.cn)


