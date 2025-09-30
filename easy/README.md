# 🚀 以太坊开发者面试问题 - Easy 难度

> 本目录包含 30 个以太坊开发者面试基础问题，每个问题都有详细的中文答案。适合初学者和准备面试的开发者使用。

## 📋 目录

| # | 问题 | 状态 |
|---|------|------|
| 1 | [函数访问修饰符的区别](#1-函数访问修饰符的区别) | ✅ 已完成 |
| 2 | [智能合约大小限制](#2-智能合约大小限制) | ✅ 已完成 |
| 3 | [CREATE vs CREATE2](#3-create-vs-create2) | ✅ 已完成 |
| 4 | [Solidity 0.8.0 算术变化](#4-solidity-080-算术变化) | ✅ 已完成 |
| 5 | [代理合约需要的特殊调用](#5-代理合约需要的特殊调用) | ✅ 已完成 |
| 6 | [计算交易美元成本](#6-计算交易美元成本) | ✅ 已完成 |
| 7 | [区块链随机数挑战](#7-区块链随机数挑战) | ✅ 已完成 |
| 8 | [荷兰拍卖 vs 英式拍卖](#8-荷兰拍卖-vs-英式拍卖) | ⏳ 待完善 |
| 9 | [ERC20 transfer 区别](#9-erc20-transfer-区别) | ⏳ 待完善 |
| 10 | [地址白名单：映射 vs 数组](#10-地址白名单映射-vs-数组) | ⏳ 待完善 |
| 11 | [为什么不用 tx.origin 认证](#11-为什么不用-txorigin-认证) | ⏳ 待完善 |
| 12 | [以太坊主要哈希函数](#12-以太坊主要哈希函数) | ⏳ 待完善 |
| 13 | [1 gwei 等于多少 Ether](#13-1-gwei-等于多少-ether) | ⏳ 待完善 |
| 14 | [1 wei 等于多少 Ether](#14-1-wei-等于多少-ether) | ⏳ 待完善 |
| 15 | [assert vs require](#15-assert-vs-require) | ⏳ 待完善 |
| 16 | [闪电贷是什么](#16-闪电贷是什么) | ⏳ 待完善 |
| 17 | [检查-效果-交互模式](#17-检查-效果-交互模式) | ⏳ 待完善 |
| 18 | [独立质押节点最小 ETH](#18-独立质押节点最小-eth) | ⏳ 待完善 |
| 19 | [fallback vs receive](#19-fallback-vs-receive) | ⏳ 待完善 |
| 20 | [重入攻击](#20-重入攻击) | ⏳ 待完善 |
| 21 | [防止无限循环](#21-防止无限循环) | ⏳ 待完善 |
| 22 | [tx.origin vs msg.sender](#22-txorigin-vs-msgsender) | ⏳ 待完善 |
| 23 | [向无 payable 合约发送 ETH](#23-向无-payable-合约发送-eth) | ⏳ 待完善 |
| 24 | [view vs pure](#24-view-vs-pure) | ⏳ 待完善 |
| 25 | [ERC721 transferFrom 区别](#25-erc721-transferfrom-区别) | ⏳ 待完善 |
| 26 | [ERC1155 转为 NFT](#26-erc1155-转为-nft) | ⏳ 待完善 |
| 27 | [访问控制重要性](#27-访问控制重要性) | ⏳ 待完善 |
| 28 | [modifier 作用](#28-modifier-作用) | ⏳ 待完善 |
| 29 | [uint256 最大值](#29-uint256-最大值) | ⏳ 待完善 |
| 30 | [可变 vs 固定利率](#30-可变-vs-固定利率) | ⏳ 待完善 |

---

## 1. 函数访问修饰符的区别

**问题**: What is the difference between private, internal, public, and external functions?

### 🎯 核心答案

| 修饰符 | 访问范围 | 特点 |
|--------|----------|------|
| **private** | 仅当前合约内部 | 最严格，子合约无法访问 |
| **internal** | 当前合约 + 子合约 | 默认访问级别 |
| **public** | 任何人都可访问 | 内部外部都可调用，自动生成 getter |
| **external** | 仅外部调用 | 内部调用需 `this.functionName()` |

### 📝 详细说明

- **private**: 最严格的访问控制，只能在定义它的合约内部使用
- **internal**: 可以被继承的子合约访问，是默认的访问级别
- **public**: 任何人都可以访问，编译器会自动为变量生成 getter 函数
- **external**: 只能被外部调用，对于大数组参数更节省 gas

---

## 2. 智能合约大小限制

**问题**: Approximately, how large can a smart contract be?

### 🎯 核心答案

**24,576 字节（24 KB）**

### 📝 详细说明

#### 🔒 为什么有这个限制？
- **防止 DoS 攻击**: 防止恶意合约占用过多节点资源
- **保护网络**: 确保 gas 成本与节点工作量成正比 (EIP-170之前不成正比)

#### 🛠️ 如何规避限制？
1. **模块化设计**: 将逻辑拆分到多个小合约
2. **代理模式**: 使用代理合约 + 实现合约
3. **库合约**: 共享代码部署为库

#### 🚀 未来展望
- **EVM 对象格式 (EOF)**: 预计将限制提高到 64 KB
- **向后兼容**: 现有合约仍保持 24 KB 限制

---

## 3. CREATE vs CREATE2

**问题**: What is the difference between create and create2?

### 🎯 核心答案

| 特性 | CREATE | CREATE2 |
|------|--------|---------|
| **地址计算** | `keccak256(rlp([sender, nonce]))` | `keccak256(0xFF ++ sender ++ salt ++ keccak256(init_code))` |
| **可预测性** | ❌ 不可预测 | ✅ 部署前可预测 |
| **Nonce 依赖** | ✅ 是 | ❌ 否 |
| **主要用途** | 标准部署 | 确定性部署 |

### 📝 详细说明

#### CREATE
- 地址基于发送者地址和 nonce 计算
- 直到部署时刻才确定地址
- 适合标准的合约部署

#### CREATE2  
- 地址基于发送者、salt 和字节码计算
- 部署前就可以计算地址
- 适合：代理升级、状态通道、跨链一致性

---

## 4. Solidity 0.8.0 算术变化

**问题**: What major change with arithmetic happened with Solidity 0.8.0?

### 🎯 核心答案

**自动溢出检查**: 所有算术操作在发生上溢/下溢时会自动回退

### 📝 详细说明

#### 🔄 变化对比
| 版本 | 行为 | 风险 |
|------|------|------|
| **0.8.0 之前** | 数值环绕 | 安全漏洞 |
| **0.8.0 之后** | 自动回退 | 更安全 |

#### 💡 实际效果
```solidity
// 0.8.0 之前
uint256 max = type(uint256).max;
max = max + 1; // 结果: 0 (环绕)

// 0.8.0 之后  
uint256 max = type(uint256).max;
max = max + 1; // 交易回退，抛出 Panic(uint256) 错误
```

#### ⚡ unchecked 块
```solidity
unchecked {
    uint256 result = a + b; // 跳过溢出检查，节省 gas
}
```

---

## 5. 代理合约需要的特殊调用

**问题**: What special CALL is required for proxies to work?

### 🎯 核心答案

**DELEGATECALL** - 在调用者上下文中执行被调用合约的代码

### 📝 详细说明

#### 🔄 执行上下文对比
| 调用类型 | 执行上下文 | 存储修改 | msg.sender |
|----------|------------|----------|------------|
| **CALL** | 被调用合约 | 被调用合约 | 调用者 |
| **DELEGATECALL** | 调用者合约 | 调用者合约 | 原始调用者 |

#### 🏗️ 代理模式原理
```
用户 → 代理合约 → DELEGATECALL → 实现合约
     ↑                              ↓
     └──────── 在代理合约上下文中执行 ←┘
```

#### ⚠️ 安全隐患
- **存储冲突**: 实现合约和代理合约存储布局不匹配
- **函数选择器冲突**: 相同函数选择器可能导致意外调用

---

## 6. 计算交易美元成本

**问题**: How do you calculate the dollar cost of an Ethereum transaction?

### 🎯 核心答案

**交易成本 = Gas Used × Gas Price × ETH/USD 汇率**

### 📝 详细说明

#### 📊 计算公式
```
美元成本 = 使用的 Gas × Gas Price (gwei) × ETH 价格 (USD)
```

#### 💡 示例计算
- **Gas Used**: 21,000
- **Gas Price**: 20 gwei  
- **ETH 价格**: $2,000
- **成本** = 21,000 × 20 × 10⁻⁹ × $2,000 = **$0.84**

#### 🔧 Gas 费用组成
| 费用类型 | 说明 | 特点 |
|----------|------|------|
| **Base Fee** | 基础费用 | 动态调整，会被销毁 |
| **Priority Fee** | 优先费用 | 给验证者的小费 |
| **Total Fee** | 总费用 | Base Fee + Priority Fee |

#### 📈 EIP-1559 影响
- **更可预测的费用**: 基础费用动态调整，减少费用波动
- **ETH 销毁机制**: 基础费用被销毁，减少 ETH 供应量
- **更好的用户体验**: 费用估算更准确

#### 💰 费用优化建议
1. **选择合适时间**: 网络拥堵时费用较高
2. **设置合理 Gas Price**: 过低可能交易失败，过高浪费费用
3. **使用 Layer 2**: 降低交易成本
4. **批量操作**: 合并多个操作减少总费用

---

## 7. 区块链随机数挑战

**问题**: What are the challenges of creating a random number on the blockchain?

### 🎯 核心答案

**区块链是确定性的，无法产生真正的随机数**

### 📝 详细说明

#### 🔒 为什么无法真正随机？
区块链网络需要所有节点验证交易结果，如果随机数不可预测，节点间无法达成共识。

#### ❌ 常见错误方法
| 方法 | 问题 | 风险 |
|------|------|------|
| `block.timestamp` | 矿工可操纵 | 被预测和利用 |
| `block.difficulty` | 矿工可操纵 | 被预测和利用 |
| `blockhash` | 可预测 | 被预测和利用 |

#### ✅ 推荐解决方案

##### 1. Chainlink VRF (可验证随机函数)
```solidity
// 请求随机数
requestRandomWords(keyHash, subscriptionId, requestConfirmations, callbackGasLimit, numWords);
```

**特点**:
- ✅ 可验证的随机性
- ✅ 防操纵性强
- ✅ 易于集成
- ❌ 需要支付 LINK 代币

##### 2. Commit-Reveal 方案
```solidity
// 第一阶段：提交哈希
function commit(bytes32 hash) external;

// 第二阶段：揭示随机数
function reveal(uint256 randomNumber, uint256 nonce) external;
```

**特点**:
- ✅ 完全去中心化
- ✅ 多方参与
- ❌ 需要两次交易
- ❌ 实现复杂

##### 3. Oracle 服务
```solidity
// 从外部预言机获取随机数
function requestRandomness() external;
```

**特点**:
- ✅ 实现简单
- ✅ 延迟低
- ❌ 中心化信任
- ❌ 安全性较低

#### 📊 方案对比

| 特征 | Chainlink VRF | Commit-Reveal | Oracle 服务 |
|------|---------------|---------------|-------------|
| **安全性** | 🔒 最高 | 🔒 较高 | ⚠️ 较低 |
| **去中心化** | 🔄 较高 | 🔄 最高 | ❌ 最低 |
| **用户体验** | ✅ 较好 | ⚠️ 较差 | ✅ 较好 |
| **延迟** | ⏱️ 中等 | ⏱️ 高 | ⚡ 低 |
| **成本** | 💰 中等 | 💰 中等 | 💰 较低 |
| **复杂度** | ✅ 简单 | ❌ 复杂 | ✅ 简单 |

#### 🎯 选择建议
- **DeFi 应用**: 推荐 Chainlink VRF
- **游戏应用**: 推荐 Chainlink VRF 或 Commit-Reveal
- **简单应用**: 可考虑 Oracle 服务

---

## 8. 荷兰拍卖 vs 英式拍卖

**问题**: What is the difference between a Dutch Auction and an English Auction?

### 🎯 核心答案

| 拍卖类型 | 价格变化 | 参与者行为 |
|----------|----------|------------|
| **荷兰拍卖** | 从高到低递减 | 第一个接受者获胜 |
| **英式拍卖** | 从低到高递增 | 最高出价者获胜 |

---

## 9. ERC20 transfer 区别

**问题**: What is the difference between transfer and transferFrom in ERC20?

### 🎯 核心答案

| 函数 | 调用者 | 用途 |
|------|--------|------|
| **transfer** | 代币持有者 | 直接转账自己的代币 |
| **transferFrom** | 授权第三方 | 转移他人授权的代币 |

---

## 10. 地址白名单：映射 vs 数组

**问题**: Which is better to use for an address allowlist: a mapping or an array? Why?

### 🎯 核心答案

**推荐使用 mapping**，因为查找效率更高

### 📝 详细说明

| 数据结构 | 查找复杂度 | Gas 消耗 | 适用场景 |
|----------|------------|----------|----------|
| **mapping** | O(1) | 低 | 频繁查找 |
| **array** | O(n) | 高 | 需要遍历 |

---

## 11. 为什么不用 tx.origin 认证

**问题**: Why shouldn't tx.origin be used for authentication?

### 🎯 核心答案

**tx.origin 容易被钓鱼攻击利用**

### 📝 详细说明

#### ⚠️ 攻击场景
```
用户 → 恶意合约 → 受害者合约
     ↑ tx.origin = 用户地址
     └── 绕过权限检查
```

#### ✅ 正确做法
使用 `msg.sender` 进行认证

---

## 12. 以太坊主要哈希函数

**问题**: What hash function does Ethereum primarily use?

### 🎯 核心答案

**Keccak-256** (SHA-3 的变体)

---

## 13. 1 gwei 等于多少 Ether

**问题**: How much is 1 gwei of Ether?

### 🎯 核心答案

**1 gwei = 10⁻⁹ ETH = 0.000000001 ETH**

---

## 14. 1 wei 等于多少 Ether

**问题**: How much is 1 wei of Ether?

### 🎯 核心答案

**1 wei = 10⁻¹⁸ ETH = 0.000000000000000001 ETH**

---

## 15. assert vs require

**问题**: What is the difference between assert and require?

### 🎯 核心答案

| 函数 | 用途 | Gas 消耗 | 错误类型 |
|------|------|----------|----------|
| **assert** | 检查内部错误 | 消耗所有 gas | Panic |
| **require** | 检查输入条件 | 退还剩余 gas | Error |

---

## 16. 闪电贷是什么

**问题**: What is a flash loan?

### 🎯 核心答案

**无抵押的即时借贷，同一交易内必须偿还**

---

## 17. 检查-效果-交互模式

**问题**: What is the check-effects-interaction pattern?

### 🎯 核心答案

**防止重入攻击的安全编程模式**

### 📝 执行顺序
1. **检查**: 验证条件
2. **效果**: 更新状态  
3. **交互**: 调用外部合约

---

## 18. 独立质押节点最小 ETH

**问题**: What is the minimum amount of Ether required to run a solo staking node?

### 🎯 核心答案

**32 ETH** (信标链验证者最低要求)

---

## 19. fallback vs receive

**问题**: What is the difference between fallback and receive?

### 🎯 核心答案

| 函数 | 触发条件 | 用途 |
|------|----------|------|
| **receive** | 纯 ETH 转账 | 接收 ETH |
| **fallback** | 无匹配函数调用 | 处理其他情况 |

---

## 20. 重入攻击

**问题**: What is reentrancy?

### 🎯 核心答案

**外部合约在状态更新前被重复调用，可能导致状态不一致**

---

## 21. 防止无限循环

**问题**: What prevents infinite loops from running forever?

### 🎯 核心答案

**Gas 限制** - 每个区块和交易都有 gas 上限

---

## 22. tx.origin vs msg.sender

**问题**: What is the difference between tx.origin and msg.sender?

### 🎯 核心答案

| 变量 | 含义 | 示例 |
|------|------|------|
| **tx.origin** | 交易发起者 | 用户钱包地址 |
| **msg.sender** | 直接调用者 | 可能是合约地址 |

---

## 23. 向无 payable 合约发送 ETH

**问题**: How do you send Ether to a contract that does not have payable functions, or a receive or fallback?

### 🎯 核心答案

**无法直接发送** - 交易会失败

### 📝 解决方案
1. 合约添加 payable 函数
2. 添加 receive() 或 fallback() 函数

---

## 24. view vs pure

**问题**: What is the difference between view and pure?

### 🎯 核心答案

| 修饰符 | 可访问性 | 用途 |
|--------|----------|------|
| **view** | 可读取状态 | 不修改状态的函数 |
| **pure** | 不可访问状态 | 纯计算函数 |

---

## 25. ERC721 transferFrom 区别

**问题**: What is the difference between transferFrom and safeTransferFrom in ERC721?

### 🎯 核心答案

| 函数 | 安全检查 | 推荐使用 |
|------|----------|----------|
| **transferFrom** | 无 | ❌ |
| **safeTransferFrom** | 有 | ✅ |

---

## 26. ERC1155 转为 NFT

**问题**: How can an ERC1155 token be made into a non-fungible token?

### 🎯 核心答案

**每个 token ID 只铸造一个代币**

---

## 27. 访问控制重要性

**问题**: What is access control and why is it important?

### 🎯 核心答案

**限制函数调用权限，防止未授权操作**

---

## 28. modifier 作用

**问题**: What does a modifier do?

### 🎯 核心答案

**在函数执行前后添加条件检查或逻辑**

---

## 29. uint256 最大值

**问题**: What is the largest value a uint256 can store?

### 🎯 核心答案

**2²⁵⁶ - 1 = 115,792,089,237,316,195,423,570,985,008,687,907,853,269,984,665,640,564,039,457,584,007,913,129,639,935**

---

## 30. 可变 vs 固定利率

**问题**: What is variable and fixed interest rate?

### 🎯 核心答案

| 利率类型 | 特点 | 适用场景 |
|----------|------|----------|
| **固定利率** | 利率不变 | 稳定收益 |
| **可变利率** | 根据市场调整 | 灵活借贷 |

---

## 📚 相关资源

- [Solidity 官方文档](https://docs.soliditylang.org/)
- [OpenZeppelin 合约库](https://openzeppelin.com/contracts/)
- [以太坊开发者资源](https://ethereum.org/developers/)

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进这些问题和答案！

---

<div align="center">

**⭐ 如果这个仓库对你有帮助，请给个 Star！**

</div>