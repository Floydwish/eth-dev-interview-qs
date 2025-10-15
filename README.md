Over 150 interview questions for Ethereum Developers
All of these questions can be answered in three sentences or less.

Easy
1. What is the difference between private, internal, public, and external functions?
2. Approximately, how large can a smart contract be?
3. What is the difference between create and create2?
4. What major change with arithmetic happened with Solidity 0.8.0?
5. What special CALL is required for proxies to work?
6. How do you calculate the dollar cost of an Ethereum transaction?
7. What are the challenges of creating a random number on the blockchain?
8. What is the difference between a Dutch Auction and an English Auction?
9. What is the difference between transfer and transferFrom in ERC20?
10. Which is better to use for an address allowlist: a mapping or an array? Why?
11. Why shouldn't tx.origin be used for authentication?
12. What hash function does Ethereum primarily use?
13. How much is 1 gwei of Ether?
14. How much is 1 wei of Ether?
15. What is the difference between assert and require?
16. What is a flash loan?
17. What is the check-effects-interaction pattern?
18. What is the minimum amount of Ether required to run a solo staking node?
19. What is the difference between fallback and receive?
20. What is reentrancy?
21. What prevents infinite loops from running forever?
22. What is the difference between tx.origin and msg.sender?
23. How do you send Ether to a contract that does not have payable functions, or a receive or fallback?
24. What is the difference between view and pure?
25. What is the difference between transferFrom and safeTransferFrom in ERC721?
26. How can an ERC1155 token be made into a non-fungible token?
27. What is access control and why is it important?
28. What does a modifier do?
29. What is the largest value a uint256 can store?
30. What is variable and fixed interest rate?

Medium
1. What is the difference between transfer and send? Why should they not be used?
2. What is a storage collision in a proxy contract?
3. What is the difference between abi.encode and abi.encodePacked?
4. uint8, uint32, uint64, uint128, uint256 are all valid uint sizes. Are there others? What changed with block.timestamp before and after proof of stake?
5. What is frontrunning?
6. What is a commit-reveal scheme and when would you use it?
7. Under what circumstances could abi.encodePacked create a vulnerability?
8. How does Ethereum determine the BASEFEE in EIP-1559?
9. What is the difference between a cold read and a warm read?
10. How does an AMM price assets?
11. What is a function selector clash in a proxy and how does it happen?
12. What is the effect on gas of making a function payable?
13. What is a signature replay attack?
14. How would you design a game of rock-paper-scissors in a smart contract such that players cannot cheat?
15. What is the free memory pointer and where is it stored?
16. What function modifiers are valid for interfaces? What is the difference between memory and calldata in a function argument?
17. Describe the three types of storage gas costs for writes.
18. Why shouldn't upgradeable contracts use the constructor?
19. What is the difference between UUPS and the Transparent Upgradeable Proxy pattern?
20. If a contract delegatecalls an empty address or an implementation that was previously self-destructed, what happens? What if it is a low-level call instead of a delegatecall?
21. What danger do ERC777 tokens pose?
22. According to the solidity style guide, how should functions be ordered?
23. According to the solidity style guide, how should function modifiers be ordered?
24. What is a bonding curve?
25. How does _safeMint differ from _mint in the OpenZeppelin ERC721 implementation? What keywords are provided in Solidity to measure time? What is a sandwich attack?
26. If a delegatecall is made to a function that reverts, what does the delegatecall do?
27. What is a gas efficient alternative to multiplying and dividing by a power of two?
28. How large a uint can be packed with an address in one slot?
29. Which operations give a partial refund of gas? What is ERC165 used for?
30. If a proxy makes a delegatecall to A, and A does address(this).balance, whose balance is returned, the proxy's or A?
31. What is a slippage parameter useful for?
32. What does ERC721A do to reduce mint costs? What is the tradeoff?
33. Why doesn't Solidity support floating point arithmetic?
34. What is TWAP?
35. How does Compound Finance calculate utilization?
36. If a delegatecall is made to a function that reads from an immutable variable, what will the value be?
37. What is a fee-on-transfer token?
38. What is a rebasing token?
39. In what year will a timestamp stored in a uint32 overflow?
40. What is LTV in the context of DeFi?
41. What are aTokens and cTokens in the context of Compound Finance and AAVE?
42. Describe how to use a lending protocol to go leveraged long or leveraged short on an asset.
43. What is a perpetual protocol?


Hard
1. How does fixed point arithmetic represent numbers?
2. What is an ERC20 approval frontrunning attack?
3. What opcode accomplishes address(this).balance?
4. How many arguments can a solidity event have?
5. What is an anonymous Solidity event?
6. Under what circumstances can a function receive a mapping as an argument?
7. What is an inflation attack in ERC4626
8. How many storage slots does this use? uint64[] x = [1,2,3,4,5]? Does it differ from memory?
9. Prior to the Shanghai upgrade, under what circumstances is returndatasize() more efficient than PUSH 0?
10. Why does the compiler insert the INVALID op code into Solidity contracts?
11. What is the difference between how a custom error and a require with error string is encoded at the EVM level? 1hat is the kink parameter in the Compound DeFi formula? 1ow can the name of a function affect its gas cost, if at all?
12. What is a common vulnerability with ecrecover?
13. What is the difference between an optimistic rollup and a zk-rollup?
14. How does EIP1967 pick the storage slots, how many are there, and what do they represent?
15. How much is one Sazbo of ether?
16. What can delegatecall be used for besides use in a proxy?
17. Under what circumstances would a smart contract that works on Etheruem not work on Polygon or Optimism? (Assume no dependencies on external contracts)
18. How can a smart contract change its bytecode without changing its address?
19. What is the danger of putting msg.value inside of a loop? escribe the calldata of a function that takes a dynamic length array of uint128 when uint128[1,2,3,4] is passed as an argument
20. Why is strict inequality comparisons more gas efficient than ≤ or ≥? What extra opcode(s) are added?
21. If a proxy calls an implementation, and the implementation self-destructs in the function that gets called, what happens?
22. What is the relationship between variable scope and stack depth?
23. What is an access list transaction?
24. How can you halt an execution with the mload opcode?
25. What is a beacon in the context of proxies?
26. Why is it necessary to take a snapshot of balances before conducting a governance vote?
27. How can a transaction be executed without a user paying for gas?
28. In solidity, without assembly, how do you get the function selector of the calldata?
29. How is an Ethereum address derived?
30. What is the metaproxy standard?
31. If a try catch makes a call to a contract that does not revert, but a revert happens inside the try block, what happens?
32. If a user calls a proxy makes a delegatecall to A, and A makes a regular call to B, from A's perspective, who is msg.sender? from B's perspective, who is msg.sender? From the proxy's perspective, who is msg.sender?
33. Under what circumstances do vanity addresses (leading zero addresses) save gas?
34. Why do a significant number of contract bytecodes begin with 6080604052? What does that bytecode sequence do?
35. How does Uniswap V3 determine the boundaries of liquidity intervals?
36. What is the risk-free rate?
37. When a contract calls another call via call, delegatecall, or staticcall, how is information passed between them?
38. What is the difference between bytes and bytes1[]?
39. What is the most amount of leverage that can be achieved in a borrow-swap-supply-collateral loop if the LTV is 75%? What about other LTV limits?
40. How does Curve StableSwap achieve concentrated liquidity?
41. What quirks does the Tether stablecoin contract have?
42. What is the smallest uint that will store 1 million? 1 billion? 1 trillion? 1 quadrillion?
43. What danger to uninitialized UUPS logic contracts pose?
44. What is the difference (if any) between what a contract returns if a divide-by-zero happens in Soliidty or if a dividye-by-zero happens in Yul?
45. Why can't .push() be used to append to an array in memory?


Advanced
1. What addresses to the ethereum precompiles live at?
2. Describe what "liquidity" is in the context of Uniswap V2 and Uniswap V3.
3. If a delegatecall is made to a contract that makes a delegatecall to another contract, who is msg.sender in the proxy, the first contract, and the second contract?
4. What is the difference between how a uint64 and uint256 are abi-encoded in calldata?
5. What is read-only reentrancy?
6. What are the security considerations of reading a (memory) bytes array from an untrusted smart contract call?
7. If you deploy an empty Solidity contract, what bytecode will be present on the blockchain, if any?
8. How does the EVM price memory usage?
9. What is stored in the metadata section of a smart contract?
10. What is the uncle-block attack from an MEV perspective?
11. How do you conduct a signature malleability attack?
12. Under what circumstances do addresses with leading zeros save gas and why?
13. What is the difference between payable(msg.sender).call{value: value}("") and msg.sender.call{value: value}("")? 1How many storage slots does a string take up?
14. How does the --via-ir functionality in the Solidity compiler work?
15. Are function modifiers called from right to left or left to right, or is it non-deterministic?
16. If you do a delegatecall to a contract and the opcode CODESIZE executes, which contract size will be returned?
17. Why is it important to ECDSA sign a hash rather than an arbitrary bytes32?
18. Describe how symbolic manipulation testing works.
19. What is the most efficient way to copy regions of memory?
20. How can you validate on-chain that another smart contract emitted an event, without using an oracle?
21. When selfdestruct is called, at what point is the Ether transferred? At what point is the smart contract's bytecode erased?
22. Under what conditions does the Openzeppelin Proxy.sol overwrite the free memory pointer? Why is it safe to do this?
23. Why did Solidity deprecate the "years" keyword?
24. What does the verbatim keyword do, and where can it be used?
25. How much gas can be forwarded in a call to another smart contract?
26. What does an int256 variable that stores -1 look like in hex?
27. What is the use of the signextend opcode?
28. Why do negative numbers in calldata cost more gas?
29. What is a zk-friendly hash function and how does it differ from a non-zk-friendly hash function?
30. What does a metaproxy do?
31. What is a nullifier in the context of zero knowledge, and what is it used for?
32. What is SECP256K1?
33. Why shouldn't you get price from slot0 in Uniswap V3?
34. Describe how to compute the 9th root of a number on-chain in Solidity.
35. What is the danger of using return in assembly out of a Solidity function that has a modifier?
36. Without using the % operator, how can you determine if a number is even or odd?
37. What does codesize() return if called within the constructor? What about outside the constructor?


upchain 面试题:
利用 AI：和ai对话，ai当你的面试官？

1. sol文件的编译过程，调用过程，sol文件是如何存到链上？
2. EVM和JVM的区别？
3. 除了ownable.sol还有什么权限控制？
4. 编写一个可升级合约，你会写什么方法，不用openzeppelin？
5. 编写完合约后，如何进行安全检查，slither是如何进行检查的？
6. 在开发过程中如何保证私钥安全？还有员工离职交接过程中如何保证私钥安全？
7. call、delegateCall、StaticCall区别？
8. 手机钱包扫描网页的二维码，可以授权，这步是怎么做到的？
9. 可升级合约，mapping（address -> user） xxx; 类型想在user里加个变量可不可以？
10. 两个uint8，storage 和 memory 不同存储空间，是存储在一个slot里还是两个slot里？
11. 可否在不支付手续费的情况下，调用一个非 view 的函数？
12. Aave V3 / Compound V3 协议的优势以及两个协议的设计上的区别在哪里？
13. 假设需要与某个DeFi协议(如aave)进行交互，例如获取用户的仓位信息，如何分析和理解该协议？
14. 假设需要从Uniswap V2 / V3 中获取流动性池的信息，你会如何理解和解析这个协议的接口？
15. 找一个熟悉的协议，说说理解？
16. sushi的挖矿原理？
17. compound的复利原理？
18. aave的清算机制？
19. UniswapV2中协议费用是如何给到项目方的？
20. UniswapV2中千分之三的手续费是如何给到流动性池的？
21. UniswapV2中的时间加权累计价格怎么算的，怎么用？什么时候会触发累加的动作？
22. UniswapV2中什么情况下会去触发时间加权累计价格的变更？
23. create2的公式是啥？
24. 透明代理合约中实现合约的地址存储在哪里？
25. 请你使用内联汇编实现transfer的操作？为啥空闲指针的位置需要去读取0x40？
26. chainlink的oracle怎么用？你简单描述一下？
27. 在一个内联汇编中实现transfer和approve，需要注意什么？
28. 请你使用内联汇编实现mapping的数据查询？
29. 什么是EIP5164？
30. 项目已经上线了，运行很久报了一个常规的错误，不是require中提示的错误信息，你应该如何去排查？
31. 在 The Graph 中，怎样实现每24小时或每1000个区块记录一次全局用户状态（如用户余额、用户数量、某个状态的快照）？
32. 一个函数报了stack too deep的问题，请你思考在不拆分函数以及不开启优化器的方式下去解决这个问题？
33. 让你设计一个类似于pumpfun的平台，你应该如何设计？
34. 面试前最好准备下背调的东西-流水/离职证明/项目？
35. ERC-20 transfer 的内联汇编实现？
mapping(address => uint256) public balances;

function transfer(address to, uint256 amount) external returns (bool success) {
    assembly {
        // --- 1. 计算 msg.sender 的 balances 存储槽位置 (Slot) ---

        // 'caller()' 是 Yul 中对应 EVM Opcode CALLER 的函数，返回当前交易的发起者地址 (msg.sender)。
        // MSTORE(0x00, value) 将 value 存储到内存的 0x00 位置（即内存 [0x00, 0x20]）。
        // 这一步是将 msg.sender（20 字节，左侧补零）放入内存作为哈希计算的 Key。
        mstore(0x00, caller()) 

        // 'balances.slot' 是 Solidity 编译器自动生成的占位符，代表 balances 这个 mapping 变量
        // 在合约状态存储中的顺序存储槽编号 p。
        // MSTORE(0x20, value) 将 balances 的槽编号 p 存储到内存的 0x20 位置（即内存 [0x20, 0x40]）。
        // 此时，内存 [0x00, 0x40] 存储的是：[msg.sender (32 字节) | p (32 字节)]。
        mstore(0x20, balances.slot) 

        // KECCAK256(offset, size) 计算内存中指定区域的 Keccak-256 哈希。
        // 根据 mapping 的存储规则：slot = keccak256(key | p)。
        // 这里的 key 是 msg.sender，p 是 balances.slot。
        // 0x00 是起始偏移量，0x40 (64 字节) 是长度。
        // 计算结果 senderSlot 就是 msg.sender 余额的实际存储位置。
        let senderSlot := keccak256(0x00, 0x40) 

        // --- 2. 加载 msg.sender 的余额 ---

        // SLOAD(slot) 从指定的存储槽读取 32 字节数据，对应 EVM Opcode SLOAD。
        // 将 senderSlot 中的值（即 msg.sender 的余额）加载到变量 senderBalance。
        let senderBalance := sload(senderSlot) 

        // --- 3. 检查余额是否足够 ---

        // LT(a, b) 是 'less than'，检查 a 是否小于 b。对应 EVM Opcode LT。
        // 检查 senderBalance 是否小于 amount。
        if lt(senderBalance, amount) { 
            // 如果余额不足，则准备 Revert 错误信息。
            // 将字符串 "NotEnoughBalance"（UTF-8 编码，20 字节）写入内存 0x00 位置。
            // 由于字符串小于 32 字节，内存中会是左侧补零（或右对齐，取决于编译器行为，但在 Revert 场景中不影响）。
            mstore(0x00, "NotEnoughBalance") 
            
            // REVERT(offset, size) 终止执行并回滚状态更改，同时将内存 [offset, offset + size] 的数据作为错误信息返回。
            // 0x00 是内存起始地址，0x20 (32 字节) 是返回的错误信息长度。
            revert(0x00, 0x20) 
        }

        // --- 4. 计算 to 的 balances 存储槽位置 ---

        // 将接收者地址 to 写入内存 0x00 位置，覆盖之前的 msg.sender。
        mstore(0x00, to) 
        
        // 再次将 balances 的槽编号 p 写入内存 0x20 位置（与步骤 1 相同）。
        mstore(0x20, balances.slot) 
        
        // 计算接收者地址 to 的实际存储槽位置。
        let toSlot := keccak256(0x00, 0x40) 

        // --- 5. 更新 balances ---

        // SSTORE(slot, value) 将 value 写入指定的存储槽，对应 EVM Opcode SSTORE。
        // SUB(a, b) 计算 a 减去 b。更新 msg.sender 的余额：senderBalance - amount。
        sstore(senderSlot, sub(senderBalance, amount)) 
        
        // ADD(a, b) 计算 a 加上 b。
        // SLOAD(toSlot) 读取接收者当前的余额。
        // 将接收者的新余额 (旧余额 + amount) 写入 toSlot。
        sstore(toSlot, add(sload(toSlot), amount)) 

        // --- 6. 返回 true ---

        // 将布尔值 true (在 EVM 中表示为 1) 写入内存 0x00 位置。
        mstore(0x00, 1) 
        
        // RETURN(offset, size) 结束函数执行并返回内存中的数据。
        // 0x00 是内存起始地址，0x20 (32 字节) 是返回数据长度。 
        // 函数返回结果 success = true。
        return(0x00, 0x20) 
    }
}