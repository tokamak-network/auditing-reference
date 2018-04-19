# Auditing reference

**What exactly is a Smart Contract audit?**
> A Smart Contract audit is the process investigating carefully a piece of code, in this case a Solidity contract to find bugs, vulnerabilities and risks before the code is deployed and used in the main Ethereum’s network where it won’t be modifiable. It’s just for discussion purposes.

## Be aware of feature of blockchain and EVM limits
  - **Feature of blockchain**:
    - [Remember that on-chain data is public](https://consensys.github.io/smart-contract-best-practices/recommendations/#remember-that-on-chain-data-is-public)
    - [In 2-party or N-party contracts, beware of the possibility that some participants may "drop offline" and not return](https://consensys.github.io/smart-contract-best-practices/recommendations/#in-2-party-or-n-party-contracts-beware-of-the-possibility-that-some-participants-may-drop-offline-and-not-return)
    - [Timestamp Dependence](https://consensys.github.io/smart-contract-best-practices/recommendations/#timestamp-dependence)
  - **EVM limits**:
    - Do consider gas limit
    - Do consider call stack depth limit (*Update: [EIP150](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-150.md) fixed this problem, removing the possibility of a call stack attack by reducing the amount of gas each recursive call gets.*)

## Solidity Code
Write simple and modular code and order your function code: **conditions**, **actions**, **interactions**
- **common**:
  - Consider using SafeMath library
  - [Enforce invariants with assert()](https://consensys.github.io/smart-contract-best-practices/recommendations/#enforce-invariants-with-assert)
  - [Use assert() and require() properly](https://consensys.github.io/smart-contract-best-practices/recommendations/#use-assert-and-require-properly)
  - [Beware rounding with integer division](https://consensys.github.io/smart-contract-best-practices/recommendations/#beware-rounding-with-integer-division)
  - [Be aware of the tradeoffs between abstract contracts and interfaces](https://consensys.github.io/smart-contract-best-practices/recommendations/#be-aware-of-the-tradeoffs-between-abstract-contracts-and-interfaces)
  - [Keep fallback functions simple](https://consensys.github.io/smart-contract-best-practices/recommendations/#keep-fallback-functions-simple)
  - [Explicitly mark visibility in functions and state variables](https://consensys.github.io/smart-contract-best-practices/recommendations/#explicitly-mark-visibility-in-functions-and-state-variables)
  - [Lock pragmas to specific compiler version](https://consensys.github.io/smart-contract-best-practices/recommendations/#lock-pragmas-to-specific-compiler-version)
  - [Differentiate functions and events](https://consensys.github.io/smart-contract-best-practices/recommendations/#differentiate-functions-and-events)
  - [Prefer newer Solidity constructs](https://consensys.github.io/smart-contract-best-practices/recommendations/#differentiate-functions-and-events)
  - [Be aware that 'Built-ins' can be shadowed](https://consensys.github.io/smart-contract-best-practices/recommendations/#differentiate-functions-and-events)
  - [Avoid using tx.origin](https://consensys.github.io/smart-contract-best-practices/recommendations/#avoid-using-txorigin)
  - [Multiple Inheritance Caution](https://consensys.github.io/smart-contract-best-practices/recommendations/#timestamp-dependence)
- **conditions**: Fail as early and loudly as possible
  - [Don’t assume contracts are created with zero balance](https://consensys.github.io/smart-contract-best-practices/recommendations/#dont-assume-contracts-are-created-with-zero-balance)
  - [Remember that Ether can be forcibly sent to an account](https://consensys.github.io/smart-contract-best-practices/recommendations/#remember-that-ether-can-be-forcibly-sent-to-an-account)
  - Check order of timestamps
  - Check timestamps, if you have logic associated with timestamps
- **actions**:
  - [Avoid state changes after external calls](https://consensys.github.io/smart-contract-best-practices/recommendations/#avoid-state-changes-after-external-calls)
- **interactions**:
  - Don't use unnecessary low level call
  - [Use caution when making external calls](https://consensys.github.io/smart-contract-best-practices/recommendations/#use-caution-when-making-external-calls)
  - [Mark untrusted contracts](https://consensys.github.io/smart-contract-best-practices/recommendations/#mark-untrusted-contracts)
  - [Be aware of the tradeoffs between send(), transfer(), and call.value()()](https://consensys.github.io/smart-contract-best-practices/recommendations/#be-aware-of-the-tradeoffs-between-send-transfer-and-callvalue)
  - [Handle errors in external calls](https://consensys.github.io/smart-contract-best-practices/recommendations/#handle-errors-in-external-calls)
  - [Favor pull over push for external calls](https://consensys.github.io/smart-contract-best-practices/recommendations/#handle-errors-in-external-calls)
  - After interacting with other contract, check the state variable integrity.

### config
- Using pragma version latest

### variable
- Consider variable size (i.e `uint8`, `uint16`, ..., `uint256`)
- Consider solidity automatically creates getter functions for state variable
- Delete unused variables
- Delete variables that have the same information
- If you can infer a variable value through another variable, delete that variable
- Do not use unnecessary temp variables
- MAGIC NUMBER uses a constant
- A constant of the same name must not have a different value in another contract
- If you can infer `true` / `false` as an integer value, use `bool`
- If the values ​​of the various state variables must maintain the relationship, consider implementing a mechanism to assert the integrity of invariants
- Consider difference between `string` and `byte`

### function
- Validate the paramter
- Multiple functions in the same logic make one function.
- Delete unused function
- If the return value is not used, remove the return parameter.
- Use `view` if the function doesn't change state.
- Use `pure` if the function doesn't even read state.
- Consider difference between `external` and `public`

### modifier
- If the modifier is used only once, it is confusing rather than useful
- Consider whether logic such as the modifier's logic is in the function
- Consider using modifiers when using common logic in multiple functions

### control statements
- for *loop*
  - Consider reviewing all for-loops and ensure that array maximum lengths are checked on iteration.
  - Consider the situation where loop exits out of gas.
  - Make sure that increment variable does not overflow.

### naming
- Naming with clear meaning
- It is recommended that the name of the `event` and the name of the `function` be different.

### etc
- Consider using scientific notation to declare numeric constants to avoid typos

## for ERC20
  - ERC20 compliance
  - Emit the event for initial supply creation, minted tokens
  - [Possible attack vector on the approve/transferFrom functionality of ERC20 tokens](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit)
  - It should be the same as the white paper.

## Attack scenario

## Write tests



## Reference
- [Zeppelin security blog](https://blog.zeppelin.solutions/security/home)
- [Onward with Ethereum Smart Contract Security](https://blog.zeppelin.solutions/onward-with-ethereum-smart-contract-security-97a827e47702)
- [Recommendations for Smart Contract Security in Solidity]( https://consensys.github.io/smart-contract-best-practices/recommendations/#remember-that-ether-can-be-forcibly-sent-to-an-account)
