#### 安装依赖

1. Foundryup

    1.1 简介
    
    >[Foundry](https://learnblockchain.cn/docs/foundry/i18n/zh/)是一个全新的EVM开发环境。有了Solidity-native测试能力（使用原生的Solidity编写测试），强大的命令行工具和高性能的[Rust](https://learnblockchain.cn/article/3609)工具；Foundry 管理项目的依赖关系、编译项目、运行测试、部署，并允许您通过命令行和 Solidity 脚本与链交互。
    >
    >中文官方文档：https://learnblockchain.cn/docs/foundry/i18n/zh/
    
    1.2 优势
    
    > - 全面支持 solidity，可有效减少上下文切换 与 hardhat+ethers 组合工具相比，hardhat+ethers 合约使用 solidity，而部署测试等使用 js 或者 ts。而对于 foundry 工具，合约、部署、测试等都使用 solidity，不需要在多种编程语言之间进行切换；
    > - 功能更齐全。如 cast 命令可以直接从 etherscan 下载源代码，可以直接从 abi 生成 interface 等功能。
    > - 运行速度更快
    
    1.3 安装
    
    ```shell
    curl -L https://foundry.paradigm.xyz | bash
    ```
    
    foundry 系列的工具，主要包含三大组件，分别对应不同的功能，下面会每个组件依次试用。
    
    - **forge**：主要用来开发、编译、部署合约。
    - **cast**：执行以太坊 RPC 调用的命令行工具；
    - **anvil**：本地模拟节点环境，类似于 ganache-cli 的功能。
    
    

#### 部署步骤

部署log

```

```

![makefile.png](https://github.com/Layr-Labs/eigenlayer-avs-playgrounds/blob/alpha/images/makefile.png?raw=true)





####  协议架构

1. 协议角色

    > EigenLayer协议：
    >
    > Operator：
    >
    > Staker：
    >
    > AVS：



#### Reference

1.  [Foundry基本使用总结](https://zhuanlan.zhihu.com/p/589226221)
2. [Foundry中文文档](https://learnblockchain.cn/docs/foundry/i18n/zh/)
3. [AVS Runbook](https://github.com/Layr-Labs/eigenlayer-avs-playgrounds/blob/alpha/docs/runbook.md)
4. [AVS Guide](https://github.com/Layr-Labs/eigenlayer-contracts/blob/master/docs/experimental/AVS-Guide.md)

















# AVS Smart Contracts Template Architecture

## Introduction

EigenLayer AVSs are a new type of protocol that leverage EigenLayer’s restaking primitive. AVSs are different from current chains and other smart contract protocols in that they are validated by EigenLayer operators. There are 3 specific types of conditions that AVSs implement in smart contracts onchain:

- Registration/Deregistration conditions: What requirements do operators need to have in order to register for/deregister from the AVS?
- Payment conditions: How much does a certain operator deserve to be paid for their validation? In what form are they paid?
- Slashing conditions: What behavior is not allowed of operators by the AVS? What exact mechanism should be used to determine this behavior onchain?

The EigenLabs dev team has been building out a smart contract architecture for AVSs to provide a base for AVSs to build on top of for their specific use case. We have been using it internally for our first AVS, EigenDA.

## The Registry Coordinator and Registries

![img](https://lh4.googleusercontent.com/bOF65t6Hx41ege2rsMoabyT87SnryD0TgThQwixH8w9Ms2LfKG-NVsMlxxoO3mXSRPLtLgnzQRskQOmfg9c-0uYkxoLICyRU6ixZHlFOmVK4RWQI6YbdWUYiujJLTl8oAVv5RkrtkvF-8S6cJHxyWg0)

There are two things that matter in terms of operators’ onchain interaction with AVS contracts:

1. What qualities of operators need to be kept track of onchain? (e.g. stake, BLS pubkeys, etc.)
2. Registration/Deregistration conditions

These two points have been addressed through the Registry Coordinator/Registry architecture.

### RegistryCoordindator

The Registry Coordinator is a contract that is deployed by each AVS. It handles

- Keeping track of what quorums operators are a part of
- Handling operator churn (registration/deregistration)
- Communicating to registries

In the current implementation, the BLSRegistryCoordinatorWithIndices, operators provide the set of quorums and their BLS public key when they register. The coordinator hands the information to the registries for validation and accepts the registration if valid.

In addition, since EigenDA can only handle a certain number of operators (due to gas cost limitation) the registry coordinator also allows new operators to register and replace currently registered operators if they have more than a certain multiple of the replaced operator’s stake and the replaced operator has less than a certain fraction of the total stake.

### Registries

The registries are contracts that keep track of the attributes of individual operators. For example, we have initially built the 

- StakeRegistry which keeps track of the stakes of different operators for different quorums at different times
- BLSPubkeyRegistry which keeps track of the aggregate public key of different quorums at different times
- IndexRegistry which keeps track of an ordered list of the operators in each quorum at different times. (note that this behavior is likely only needed for EigenDA)

Registries are meant to be read from and indexed by offchain AVS actors (operators and AVS coordinators). 

A registry coordinator has 1 or more registries connected to it and all of them are called when an operator registers or deregisters. They are a plug and play system that are meant to be added to the RegistryCoordinator as needed. AVSs should create registries they need for their purpose.

## Service Manager

Another contract that is deployed per AVS is the service manager. The service manager essentially handles all “write” operations to EigenLayer. AVSs should send StakeUpdates back to the EigenLayer Slasher whenever they are requested. Stake updates essentially signal to EigenLayer that the AVS has an accurate view of the stake, allowing funds that are pending withdrawal to be unstaked after a period of time specified by the AVS. For more information, look at the docs.

The StakeRegistry and Registry Coordinator both talk to the Service manager for this purpose.

## BLSSignatureChecker

This contract is specific to AVSs whose task consists of operators signing off on a particular message and having the signature of that message confirmed onchain. This actually includes a large fraction of the AVSs built on EigenLayer. The BLSSignatureChecker is code that leverages the default implementations of the StakeRegistry, the BLSPubkeyRegistry, and the RegistryCoordinator in order to verify signatures of messages and calculate how much stake of from each of the requested quorums has signed off on the message.

The EigenDA disperser client has boilerplate code to generate the transactions for this contract.

The BLSSignature checker gas costs are actually what leads to EigenDA’s operator limit. We anticipate that the limit will be around 250 for the ETH quorum and ~20 for other quorums.

## Development

To be transparent about our development on this architecture, the following points should be made:

- The Slasher is anticipated to be redesigned and will result in changes to the ServiceManager.
- The Registry/Registry Coordinator architecture is relatively stable. We don’t anticipate changes other than fixes, cleanup, and those required for the new slasher before EigenDA mainnet.
- Down the line, we anticipate the entire architecture will switch to an accumulator style architecture where, during registration, deregistration, and updates, all information of an AVSs onchain operator state is accumulated into a single merkle root. This will make switching signature verification and aggregation across middlewares into a simple ZKP verification, which will significantly increase the operator set threshold.
