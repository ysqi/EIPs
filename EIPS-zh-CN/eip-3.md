---
eip: 3
title: Addition of CALLDEPTH opcode
author: Martin Holst Swende <martin@swende.se>
status: 已撤回
type: 标准跟踪
category: 核心
created: 2015-11-19
---

# 摘要

This is a proposal to add a new opcode, `CALLDEPTH`. The `CALLDEPTH` opcode would return the remaining available call stack depth. The `CALLDEPTH` opcode would return the remaining available call stack depth.

# 动机

There is a limit specifying how deep contracts can call other contracts; the call stack. The limit is currently `256`. There is a limit specifying how deep contracts can call other contracts; the call stack. The limit is currently `256`. If a contract invokes another contract (either via `CALL` or `CALLCODE`), the operation will fail if the call stack depth limit has been reached.

This behaviour makes it possible to subject a contract to a "call stack attack" [1]. In such an attack, an attacker first creates a suitable depth of the stack, e.g. by recursive calls. After this step, the attacker invokes the targeted contract. If the targeted calls another contract, that call will fail. If the return value is not properly checked to see if the call was successful, the consequences could be damaging. In such an attack, an attacker first creates a suitable depth of the stack, e.g. by recursive calls. After this step, the attacker invokes the targeted contract. If the targeted calls another contract, that call will fail. If the return value is not properly checked to see if the call was successful, the consequences could be damaging.

Example:

1. Contract `A` wants to be invoked regularly, and pays Ether to the invoker in every block.
2. When contract `A` is invoked, it calls contracts `B` and `C`, which consumes a lot of gas. After invocation, contract `A` pays Ether to the caller. After invocation, contract `A` pays Ether to the caller.
3. Malicious user `X` ensures that the stack depth is shallow before invoking A. Both calls to `B` and `C` fail, but `X` can still collect the reward.

It is possible to defend against this in two ways:

1. Check return value after invocation.
2. Check call stack depth experimentally. A library [2] by Piper Merriam exists for this purpose. This method is quite costly in gas.


[1] a.k.a "shallow stack attack" and "stack attack". [1] a.k.a "shallow stack attack" and "stack attack". However, to be precise, the word ''stack'' has a different meaning within the EVM, and is not to be confused with the ''call stack''.

[2] https://github.com/pipermerriam/ethereum-stack-depth-lib

# 规范

The opcode `CALLDEPTH` should return the remaining call stack depth. The opcode `CALLDEPTH` should return the remaining call stack depth. A value of `0` means that the call stack is exhausted, and no further calls can be made.

# 基本原理

The actual call stack depth, as well as the call stack depth limit, are present in the EVM during execution, but just not available within the EVM. The implementation should be fairly simple and would provide a cheap and way to protect against call stack attacks. The implementation should be fairly simple and would provide a cheap and way to protect against call stack attacks.

# 实现

Not implemented.
