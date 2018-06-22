---
title: "1_Smart_contracts"
date: 2018-06-17 12:00
---

[TOC]



# Smart Contracts



## Hello World 代码

```
pragma solidity ^0.4.21; // 程序版本

contract SimpleStorage {       // 合约声明
    uint storedData;
    
    function set(uint x) {
        storedData = x;
    }
    
    function get() constant returns (uint){
        return storedData;
    }
}


```



## 合约方法



### constant -> view 

* 最新版本变成view 方法

  

### pure

* 比constant警示作用更严格，在做库的时候会有用





## remix 在线编辑器

* remix.ethereum.org



## eth gas 

* 在函数调用的通过的gas 来完成





## solidity 

* 没有浮点数，不支持非整数声明

### bool 

* true
* false
* ! 
* && 
* ||
* ==
* !=



### uint / int 

* 比较： <=, <, ==, !=, >=, > 
* 位操作： &, |, ^,~, >>, <<
* 计算： + = * / % **



### 地址address

* 智能合约也是有地址



#### 成员变量函数

* Address.balance
* Address.transfer(value)
* Address.send(value)
* address.call, address.callcode and dress.delegatecall








### ETHER 单位

* Wei 
* szabo = 10 ^ 12 wei
* finney = 10 ^ 15 wei
* Ether = 10 & 18 wei

```
pragma solidity ^0.4.14;

contract Payroll {
    uint salary = 1 ether;
    address frank = 0x7eC9938C53e6DE7B4B502B5e6fc388084b934577;
    uint payDuration = 30 days;
    uint lastPayday = now;
    
    function test() returns (bool) {
        return 1 wei == 1;
    }
    
}
>>>
to:Payroll.test() 0xdc0...46222value:0 weidata:0xf8a...8fd6dlogs:0hash:0x487...e0f91
Debug
 status 	0x1 Transaction mined and execution succeed
 from 	0xca35b7d915458ef540ade6068dfe2f44e8fa733c
 to 	Payroll.test() 0xdc04977a2078c8ffdf086d618d1f961b6c546222
 gas 	3000000 gas
        
 transaction cost 	21492 gas 
 execution cost 	220 gas 
 input 	0xf8a8fd6d
 decoded input 	{}
 decoded output 	{
	"0": "bool: true"
}
 logs 	[]
 value 	0 wei
        
```



### block 块

* Block.blockhash(uint blockNumber) returns (bytes32)
* block.coinbase(address)
* block.difficulty(uint)
* Block.gaslimit(unit)
* block.number(uint)
* block.timestamp(uint)
* now



### 消息

* Msg.data
* msg.gas(uint)
* Msg.sender(address)
* Msg.sig
* Msg.value(uint)



### revert 返回 

* Throw 会消耗掉gas
* revert可以返回gas





### 数组

#### 固定长度(uint[5] a)

```
pragma solidity ^0.4.14;

contract Test {
    uint[2] a;
    
    function test() returns (uint, uint) {
        a[0] = 1;
        a[1] = 2;
        
        return (a[0], a[1]);
    }
}
```





#### 动态长度(uint[] a)

```
pragma solidity ^0.4.14;

contract Test {
    uint[] a;
    
    function test() returns (uint, uint) {
        a.push(1);
        a.push(2);
        
        a[1] = 3;
        
        return (a[0], a[1]);
    }
}
```





### struct 

```
struct Employee {
    address id;
    uint salary;
    uint lastPayday;
}
```



### 循环

#### for

#### while





### data location

* storage 永久的，区块链上的

* memory EVM临时空间，function运行完成后抹除

* calldata 类似memory

  

#### 强制

* 状态变量： storage
* function输入参数： calldata



#### 默认

* function返回参数 ： memory
* 本地变量：storage

















## 设计 design

![alt](https://cdn.pbrd.co/images/HqsEYgc.png)



* 原生定时器是没有，每一个块需要执行一个完整的函数
* 通过外部方式调用定时器


### 单人设计

#### code

```
pragma solidity ^0.4.14;

contract Payroll {
    uint constant payDuration =  10 seconds;
    
    address owner;
    uint salary;
    address employee;
    uint lastPayday;
    
    function Payroll() {
        owner = msg.sender;
    }
    
    function updateEmployee(address e, uint s) {
        require(msg.sender == owner);
       
        if (employee != 0x0) {
            uint payment = salary * (now - lastPayday) / payDuration;
            employee.transfer(payment);
        }
        
        employee = e;
        salary = s * 1 ether;
        lastPayday = now;
    }
    
    function addFund() payable returns (uint) {
        return this.balance;
    }
    
    function calculateRunway() returns (uint) {
        return this.balance / salary;
    }
    
    function hasEnoughFund() returns (bool) {
        return calculateRunway() > 0;
    }
    
    function getPaid() {
        require(msg.sender == employee);
        
        uint nextPayday = lastPayday + payDuration;
        assert(nextPayday < now);
        lastPayday = nextPayday;
        employee.transfer(salary);
       
    }
    
}
```





## 错误检测

### assert(bool)

* 在程序运行的时候，是否存在错误



### require(bool)

* 在程序输入的时候，是否存在错误












