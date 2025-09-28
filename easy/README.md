# 以太坊开发者面试问题 - Easy 难度

## 1. What is the difference between private, internal, public, and external functions?

**private**: 
- 变量、函数仅当前合约内部可用
- 不能被继承的子合约访问
- 最严格的访问控制

**internal**: 
- 变量、函数当前合约内部可用
- 可以被继承的子合约访问
- 默认的访问级别（如果不指定）

**public**: 
- 变量、函数任何人都可以访问
- 内部和外部调用都可以
- 编译器会自动生成getter函数（对于变量）

**external**: 
- 函数只能被外部调用（通过交易或外部合约调用）
- 内部调用需要使用this.functionName()的方式
- 对于大数组参数更节省gas

## 2. Approximately, how large can a smart contract be?

**答案：24,576字节（24 KB）**

### 背景
目前，以太坊智能合约的字节码大小被限制在24,576字节（24 KB）。这个限制是由以太坊改进提案（EIP-170）引入的，其核心原因是为了防止拒绝服务（DoS）攻击。

### 为什么存在大小限制
合约大小限制是一项旨在保护网络的安全措施，它能阻止恶意攻击，避免其滥用以太坊节点处理合约数据的方式。

#### DoS攻击风险
- **节点工作量不成比例**：在设定大小限制之前，攻击者可以部署一个非常大的合约。对攻击者而言，调用这个合约的成本相对较低，但却会迫使每个以太坊节点完成大量工作。这些工作包括从存储中读取大型合约代码以及执行初步处理，这对节点造成了不成比例的负担。
- **防止网络瓶颈**：通过利用少量的Gas消耗，强迫节点执行过多的工作，大型合约可以被用来拖慢整个网络，从而构成一种有效的DoS攻击方式。

### EIP-170的解决方案
2016年，在Spurious Dragon硬分叉期间，EIP-170设定了一个部署合约字节码大小的硬性上限。这确保了节点处理合约调用所需的工作量与调用者支付的Gas成本成正比，从而消除了DoS攻击的风险。

### 开发者如何规避限制
24 KB的编译字节码大小限制对于复杂的应用来说相当小。因此，开发者通常会采用以下架构模式来解决这个限制：

#### 1. 模块化
开发者不会部署一个单一的、庞大的合约，而是将逻辑拆分成多个相互关联的小型合约。一个中心化的"管理器"（Manager）或"内核"（Kernel）合约可以与这些功能各异的小型库合约进行交互。

#### 2. 代理模式
一个代理合约（Proxy contract）可以将所有函数调用转发给一个更大、不可变的"实现"合约（Implementation contract）。这种模式允许合约实现可升级，并有助于管理字节码大小，尽管它会增加架构的复杂性。

#### 3. 使用库
许多合约共用的代码可以作为库合约部署一次，然后被其他合约调用。这不仅能实现代码复用，还能保持各个合约的尺寸较小。

## 3. What is the difference between create and create2?

**核心区别**：CREATE 和 CREATE2 的主要区别在于最终合约地址的计算方式，这决定了部署地址是否可预测。

### CREATE

#### 地址计算
CREATE 操作码根据发送方地址和其交易 nonce 来确定新合约的地址。Nonce是一个顺序计数器，每当一个地址发送一次交易，其Nonce就会增加。

**公式**：`address = keccak256(rlp([sender, nonce]))[12:]`

#### 特点
- **可预测性**：直到部署的那个确切时刻，合约的地址都是不可预测的。因为如果部署者在此期间发送了其他交易，Nonce值就会发生改变
- **使用场景**：标准的、简单的合约部署，不需要事先知道合约地址的情况

### CREATE2

#### 地址计算
CREATE2 操作码（在 EIP-1014 中引入）使用四个组成部分来计算地址：

1. 一个常量值 (0xFF)，用于防止与 CREATE 生成的地址发生冲突
2. 部署者的地址
3. 一个自定义的 salt（一个任意的32字节值）
4. 合约初始化代码的 keccak256 哈希值

**公式**：`address = keccak256(0xFF ++ sender ++ salt ++ keccak256(init_code))[12:]`

#### 特点
- **可预测性**：由于地址取决于用户定义的 salt 和合约字节码，因此即使合约尚未部署，其最终地址也可以在链下计算出来
- **使用场景**："确定性"部署，即事先知道地址的情况

#### 高级应用场景
1. **反事实实例**：在链上与一个尚不存在的合约地址进行交互。这在状态通道和第二层（Layer 2）解决方案中非常有用
2. **可升级性**：将一个新的实现合约部署到一个可预测的地址，允许代理合约指向它，从而简化升级
3. **跨链一致性**：在不同的、兼容EVM的链上，无论Nonce差异如何，都可以在同一地址部署相同的合约代码


## 4. What major change with arithmetic happened with Solidity 0.8.0?

**核心变化**：Solidity 0.8.0 版本中算术运算的主要变化是：所有算术操作在发生上溢或下溢时，现在都会默认回退（revert）。这是一项重大更改，显著提高了智能合约的安全性。

### 在 Solidity 0.8.0 之前

在此版本之前，无符号整数（例如 uint256）在发生上溢或下溢时，其值会"环绕"。这可能导致严重的安全漏洞，例如：

- **上溢**：`uint256 max = type(uint256).max; max = max + 1;` 会导致 max 的值被重置为 0，而不是回退
- **下溢**：`uint256 value = 0; value = value - 1;` 会导致 value 的值被设置为 `type(uint256).max`

为了解决这个问题，开发者通常需要使用来自 OpenZeppelin 的 SafeMath 库来执行带有检查功能的算术运算。

### 在 Solidity 0.8.0 中

通过 0.8.0 更新，编译器现在会自动为所有整数算术操作添加溢出和下溢检查。

- **自动检查**：如果发生上溢或下溢，交易将自动回退，并带有一个 `Panic(uint256)` 错误，从而防止意外和潜在的恶意行为
- **简化开发**：这使得对于简单的算术运算不再需要 SafeMath 库，代码因此变得更清晰、更易读，并减少了调用外部库函数所产生的 Gas 消耗

### unchecked 代码块

如果开发者确实需要环绕行为（例如，用于非常特定的低级逻辑），他们可以使用 `unchecked { ... }` 代码块来禁用默认的溢出和下溢检查。这提供了一种在必要时选择不使用新默认行为的方式。

使用 unchecked 可以节省 Gas，因为编译器会跳过执行溢出和下溢检查的额外操作码。但是必须在确保不会发生溢出或下溢的情况下才能安全地使用它，否则可能导致严重的安全漏洞。

**示例**：
```solidity
unchecked {
    uint256 result = a + b; // 不会进行溢出检查
}
```

## 5. What special CALL is required for proxies to work?

**答案**：代理合约需要一个特殊的调用，即 **DELEGATECALL**，才能正常工作。与标准的 CALL 不同，DELEGATECALL 允许代理合约在保持自身上下文（包括存储、msg.sender和 msg.value）的情况下，执行另一个合约（称为实现合约）的代码。

### DELEGATECALL 的工作原理

为了理解 DELEGATECALL，可以将它与两个合约（合约 A 为调用方，合约 B 为被调用方）之间的标准 CALL 进行比较：

#### 标准 CALL
合约 B 的代码在合约 B 的上下文中执行。这意味着：
- 任何被修改或读取的状态变量都是合约 B 的
- `msg.sender` 和 `msg.value` 也会更新为合约 A 的调用

#### DELEGATECALL
合约 B 的代码被执行，但其上下文却是合约 A。这意味着：
- **存储**：执行合约 B 的代码期间所做的任何状态更改都会应用于合约 A 的存储
- **上下文变量**：`msg.sender` 和 `msg.value` 保持与触发代理的原始调用相同，而不是代理合约本身

### DELEGATECALL 在代理模式中的作用

DELEGATECALL 是可升级代理模式的关键，允许：
- **代理合约**（存储状态和实现合约地址）将调用转发给实现合约（包含逻辑）
- 实现合约在代理合约的存储上执行操作
- 通过更新代理中的引用地址，可以在不影响用户数据的情况下升级合约逻辑

### 安全隐患

DELEGATECALL 存在存储冲突的安全风险：
- **存储布局不匹配**：实现合约和代理合约的存储布局不匹配可能导致代理合约数据被意外覆盖
- **函数选择器冲突**：如果实现合约和代理合约有相同的函数选择器，可能导致意外的函数调用

### 示例对比

```solidity
// 标准 CALL
contract A calls contract B → B 的代码在 B 的上下文中执行

// DELEGATECALL  
contract A calls contract B → B 的代码在 A 的上下文中执行
```

## 6. How do you calculate the dollar cost of an Ethereum transaction?

## 7. What are the challenges of creating a random number on the blockchain?

## 8. What is the difference between a Dutch Auction and an English Auction?

## 9. What is the difference between transfer and transferFrom in ERC20?

## 10. Which is better to use for an address allowlist: a mapping or an array? Why?

## 11. Why shouldn't tx.origin be used for authentication?

## 12. What hash function does Ethereum primarily use?

## 13. How much is 1 gwei of Ether?

## 14. How much is 1 wei of Ether?

## 15. What is the difference between assert and require?

## 16. What is a flash loan?

## 17. What is the check-effects-interaction pattern?

## 18. What is the minimum amount of Ether required to run a solo staking node?

## 19. What is the difference between fallback and receive?

## 20. What is reentrancy?

## 21. What prevents infinite loops from running forever?

## 22. What is the difference between tx.origin and msg.sender?

## 23. How do you send Ether to a contract that does not have payable functions, or a receive or fallback?

## 24. What is the difference between view and pure?

## 25. What is the difference between transferFrom and safeTransferFrom in ERC721?

## 26. How can an ERC1155 token be made into a non-fungible token?

## 27. What is access control and why is it important?

## 28. What does a modifier do?

## 29. What is the largest value a uint256 can store?

## 30. What is variable and fixed interest rate?