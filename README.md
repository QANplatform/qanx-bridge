# The QANX Bridge

The QANX Bridge is a multi-chain bridge supporting any Ethereum protocol based blockchain.

## Live dApp

You can use the bridge by clicking on this link: **[bridge.qanx.org](https://bridge.qanx.org)**

Feel free to browse the live instances of the QANX Bridge smart contracts below as well:

- ETH: [0xAAA4940aA878D932D3482Bf1DE332E1D50c15AaA](https://etherscan.io/address/0xAAA4940aA878D932D3482Bf1DE332E1D50c15AaA) [ Ethereum ]
- BSC: [0xAAA4940aA878D932D3482Bf1DE332E1D50c15AaA](https://bscscan.com/address/0xAAA4940aA878D932D3482Bf1DE332E1D50c15AaA) [ Binance Smart Chain ]

## Audited by CertiK <img align="right" src="./audit/certik-badge.png">

We are proud that the BridgeQANX smart contract passed CertiK's audit. You can find the audit report [here](./audit/REP-QANX-Bridge-2021-10-27.pdf).

CertiK leads blockchain security by pioneering the use of cutting-edge Formal Verification technology on smart contracts and blockchains. Unlike traditional security audits, Formal Verification mathematically proves program correctness and hacker-resistance.

Other than BridgeQANX contract the audit firm CertiK was also assigned to audit the recognizable PancakeSwap, 1inch, Tether and Matic just to name a few.

## The most efficient way

*Nobody* likes paying for gas. We do get that!

Even though our working mechanism described in the next paragraph below does a great deal of integrity checking to ensure transactions are deterministic and can not be tampered with, we managed that all this added complexity takes not more than an additional ~10% of gas of a regular ERC20/BEP20 token transfer transaction!

**Actual numbers with transaction samples linked:**

| TX type     | Gas consumed                                                                                                 |
| ----------- | ------------------------------------------------------------------------------------------------------------ |
| Transfer    | [52,503](https://etherscan.io/tx/0x01cda73f3fcb5a16796d5a9619417b6cb159459d5003ec34dd0806c496d5cb11)         |
| Bridge Send | [56,604](https://ropsten.etherscan.io/tx/0x1e00bbd60608cb94af02b28991a5cfd79cdf0bd575156cf3d35035ad2c8dfc98) |

## Human readable, understandable code

One of QAN's key missions is to make the decentralized world understandable for everyday people.

On top of implementing the cleanest & shortest contract for token bridging purpose (~100 lines!) we paid attention to making it even as much human readable as possible. Logic is commented almost above every single line with clear wording.

You can read it by clicking [here](./BridgeQANX.sol#L48).
## Working mechanism

Anyone can send tokens to the bridge on a certain chain in order to be withdrawn on another chain.
The sender can specify the following attributes:

- **Beneficiary address** -> The wallet address permitted to receive tokens on the other chain
- **Amount of QANX** -> The amount of QANX tokens to be bridged to the other chain
- **Withdraw Chain ID** -> The Chain ID of the other chain where tokens can be withdrawn

After the tokens have been sent to the bridge, it is possible to withdraw them on a chain with the specified Chain ID as follows:
### Driven by determinism

Based on above parameters, a deterministic BTXID (Bridge Transaction ID) can be calculated which also incorporates a nonce which is incremented related to the transactor, the source Chain ID and the target Chain ID. This ensures that withdrawal transactions can not be tampered with, only transactions whose parameters map to the very same BTXID can be withdrawn on the target chain.









