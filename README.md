# ZombieGameSmartContractExample
> Solidity练习，下面是一些知识点记录：
1. https://cryptozombies.io
2. 私有函数private,公有函数public,事件event,返回函数returns。
3. 结构体struct
4. 数据类型uint/string
5. 数据类型mapping/address
6. msg.sender，它指的是当前调用者（或智能合约）的 address
7. require使得函数在执行过程中，当不满足某些条件时抛出错误，并停止执
8. inheritted继承，关键字is
9. storage永久/memory临时
10. internal(只要继承就可以访问，包括其中的private函数，与单独private有区别)
11. external(只能在合约文件外调用，本合约内函数无法调用，与public有区别)
12. interface，与其他合约交互
13. 在Solidity中，您可以让一个函数返回多个值(different with JS)
14. 函数修饰符modifier，其他语句执行前，为它检查下先验条件。
15. import "./xxxx.sol";
16. 节省gas，结构化封装。当uint定义在一个struct中的时候，尽量使用最小的整数子类型以节约空间。并且把同样类型的变量放一起。
17. now\years\weeks\days\hours\minutes\seconds
18. 强制类型转换uint32(...)
19. view标记函数，在同一个合约内不收费，在不同合约内还是要收取gas。
20. 决定函数何时和被谁调用的可见性修饰符: private意味着它只能被合约内部调用；internal就像private,但是也能被继承的合约调用；external只能从合约外部调用；最后public可以在任何地方调用，不管是内部还是外部。
21. 状态修饰符， 告诉我们函数如何和区块链交互: view 告诉我们运行这个函数不会更改和保存任何数据；pure告诉我们这个函数不但不会往区块链写数据，它甚至不从区块链读取数据。这两种在被从合约外部调用的时候都不花费任何gas（但是它们在被内部其他函数调用的时候将会耗费gas）。
22. payable函数
23. keccak256，不安全，会利用强大的算力提高本节点的成功率，才发送广播。解决方法之一，利用oracle访问区块链之外的随机函数。https://ethereum.stackexchange.com/questions/191/how-can-i-securely-generate-a-random-number-in-my-smart-contract
24. 当交易所想要添加一个新的ERC20代币时，只需将新的ERC20代币合约地址添加到它的数据库即可。
25. 但游戏物品或人物无法分割，不适合ERC20代币。所以出现ERC721代币，其不能互换，因为每个代币都被认为是唯一且不可分割的。你只能以整个单位交易它们，并且每个单位都有唯一的ID。
26. OpenZeppelink库 ERC721/SafeMath
27. overflow/underflow ---> safemath库，有四个方法 — add， sub， mul， 以及 div。
28. 库和合约调用的区别，库关键字library，调用类似using libname for uint。
29. assert和require 区别在于，require若失败则会返还给用户剩下的gas，assert则不会。所以大部分情况下，你写代码的时候会比较喜欢require，assert只在代码可能出现严重错误的时候使用，比如uint溢出。
30. Solidity社区所使用的一个标准是使用一种被称作natspec格式的注释。类似：/// @dev xxxxxx
31. web3.js以太坊使用的前端框架，并配合前端界面渲染，建议使用Vue.js等。。
32. 通过JSON-RPC与节点通讯。
33. Infura提供以太坊API调用服务(Provider)，不提供写入。这时需要Metamask或MIST。
34. ABI意为应用二进制接口（Application Binary Interface）。基本上，它是以JSON格式表示合约的方法，告诉Web3.js如何以合同理解的方式格式化函数调用。
35. web3.js提供call和send，其中call用来调用view/pure函数，它只运行在本地节点，不会在区块链上创建事物。send将创建一个事物并改变区块链上的数据，适用于任何非view/pure函数。
36. 在Solidity里，当你定义一个public变量的时候，它将自动定义一个公开的"getter"同名方法，所以如果你像要查看id为15的僵尸，你可以像一个函数一样调用它：zombies(15)。
37. JS与MetaMask交互，var userAccounts = web3.eth.accounts[0] //默认账户
38. 前端编写代码时注意，我们需要指定发送多少wei，而不是直接发送以太，wei是以太的最小单位 — 1 ether 等于 10^18 wei。web3js.utils.toWei("1", "ether"); //把 1 ETH 转换成 Wei
39. 为了筛选仅和当前用户相关的事件，Solidity合约将必须使用indexed关键字，就像在ERC721实现中的Transfer事件中那样：event Transfer(address indexed _from, address indexed _to, uint256 _tokenId); 这种情况下，因为_from和_to都是indexed的，意味着可以在前端事件中监控过滤事件，只关注当前用户相关的事件信息。
40. 前端的event也可以作为一种便宜的存储，虽然不能从智能合约本身读取，但如果你有一些数据要永久保存在区块链中以便可以在应用前端读取，事件将是一个很好的解决方式，且不会影响智能合约向前的状态。举例，我们可以用事件来作为僵尸战斗的历史纪录——我们可以在每次僵尸攻击别人以及有一方胜出的时候产生一个事件。智能合约不需要这些数据来计算任何接下来的事情，但是这对我们在前端向用户展示来说是非常有用的东西。
41. return和throw的区别：return花费gas少，但是对contract做的任何改变都将会被被保留。throw会取消所有执行的合约，恢复所有变更，合约的发起者会失去所有的gas，但是因为钱包可以检测到throw异常并给出告警，因此能从根本上防止任何ether的花费，从而比return更省钱。

> this is my zombie:  
https://share.cryptozombies.io/zh/lesson/6/share/The_Phantom_of_Web3?id=YXV0aDB8NWFjYjVhMDI5ZTBiZDk3ZDdhMjJlMGY0

> All scripts right belongs to cryptozombies.io
