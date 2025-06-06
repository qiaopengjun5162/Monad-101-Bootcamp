## 第二章：Solidity 快速入门

### 一、填空题

1. Solidity中存储成本最高的变量类型是`storage`变量，其数据永久存储在区块链上。  
2. 使用`constant`关键字声明的常量可以节省Gas费，其值必须在编译时确定。  
4. 当合约收到不带任何数据的以太转账时，会自动触发`receive`函数。  

---

### 二、选择题

4. 函数选择器(selector)的计算方法是： （ B ）    
   **A)** sha3(函数签名)  
   **B)** 函数名哈希的前4字节  
   **C)** 函数参数的ABI编码  
   **D)** 函数返回值的类型哈希  

5. 以下关于mapping的叙述错误的是：（  C )     
   **A)** 键类型可以是任意基本类型  
   **B)** 值类型支持嵌套mapping  
   **C)** 可以通过`length`属性获取大小  
   **D)** 无法直接遍历所有键值对  

---

### 三、简答题

6. 请说明`require`、`assert`、`revert`三者的使用场景差异（从触发条件和Gas退还角度）

`require`：输入状态校验，失败时退还未使用gas；

`assert`：检查内部逻辑错误，失败时不退还gas；

`revert`：主动中止执行，失败时退还未使用gas。

7. 某合约同时继承A和B合约，两者都有`foo()`函数：

```solidity
contract C is A, B {
    function foo() override(A,B) {...}
}
```

实际执行时会调用哪个父合约的函数？为什么？

会调用 C 的函数，因为 C 合约继承 A，B 合约并重写了 foo 函数     
如果 C 不覆盖foo函数，则会执行继承顺序中最后一个父合约，也就是 B 合约，这是Solidity的线性化规则，选择最右的


8. 当使用`call`方法发送ETH时，以下两种写法有何本质区别？

```solidity
(1) addr.call{value: 1 ether}("")
(2) addr.transfer(1 ether)
```

第一种方法没有gas限制会传递所有剩余gas，不会自动`revert`需手动检查，安全性低

第二张方法有固定的gas限制，在失败时会`revert`，安全性高
