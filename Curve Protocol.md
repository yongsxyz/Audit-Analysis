#  Analysis - Curve Protocol


##  1. Analysis of the code base

To analyze a code base effectively, it is crucial to stack the codes for analysis. This enables the auditor to make predictions, such as the difficulty level of contracts, which contracts are more important, and the features that are critical for security (such as payable functions or the use of assembly). Furthermore, this approach helps to determine the audit cost of the project and the time required for the audit.

-   **Lines:**  total lines of the source unit
-   **nLines:**  normalized lines of the source unit (e.g. normalizes functions spanning multiple lines)
-   **nSLOC:**  normalized source lines of code (only source-code lines; no comments, no blank lines)
-   **Comment Lines:**  lines containing single or block comments
-   **Complexity Score:**  a custom complexity score derived from code statements that are known to introduce code complexity (branches, loops, calls, external interfaces, ...)

![tabel](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/4bcb5753-fa1e-42de-ab92-d79c1480471b)

### Exposed Functions
![Exposed1](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/cb97fb45-b99d-4b19-a335-344a6e9aa63d)
![exposed2](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/6830751d-88c9-4149-9ad0-68bdd52826e7)

### State Variables
![statevariables](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/5ad40bfe-104c-4845-be65-c1323d700f1c)

### Capabilities
![capabilities1](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/5feb1c1d-5d7a-4e34-98af-fbe627234e19)
![capabilities2](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/6ba57163-4125-48c0-a504-00d627325828)
![capabilities3](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/654f1ffc-e3c9-4fc9-aa55-d1bd79bba88e)

### Curves
![gaskeuns](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/9e7d8863-ba29-4dcf-83f1-34ab439e9aab)
![testeddz](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/d13d14ce-1279-43dc-a208-b593d7eb17e3)
Contract Initialization
initialized with the addresses of curvesERC20Factory and feeRedistributor in the constructor. These addresses are used to interact with the respective contracts later.

#### Fee Configuration
allows configuration of various fees configuration parameters through functions like setFeeRedistributor, setMaxFeePercent, setProtocolFeePercent, and setExternalFeePercent. These functions set parameters such as protocol fees, subject fees, referral fees, and maximum fee percentages.

#### Token Creation
allows the creation and management of ERC-20 tokens through functions like _deployERC20, setNameAndSymbol, mint, and buyCurvesTokenWithName. Users can buy Curves tokens and mint corresponding ERC-20 tokens.

#### Buying and Selling
Users can buy and sell Curves tokens using functions like buyCurvesToken and sellCurvesToken. The contract ensures proper validation, including presale checks, balance verification, and fee calculations.

#### Token Transfers and Utility Functions
The contract includes functions for transferring tokens (transferCurvesToken, transferAllCurvesTokens) and utility functions like _transfer and _addOwnedCurvesTokenSubject.

#### Presales and Whitelisting
supports presales, allowing users to participate and buy tokens at a specified time. Functions like buyCurvesTokenForPresale, setWhitelist, and buyCurvesTokenWhitelisted handle presale-related functionality.

#### Deposit and Withdrawal
users to deposit and withdraw tokens. Functions like deposit, sellExternalCurvesToken, and withdraw handle these operations.

#### Event Logging
events like Trade, Transfer, WhitelistUpdated, and TokenDeployed are emitted to log important actions and state changes.

### Fee Spliter

In conclusion, this FeeSplitter contract aims to manage and distribute fees (fees) from various tokens among users. Here are some key points:

#### Tokens and Fees:
Contracts aggregate cost information associated with each token through the TokenData data structure.

#### Token Management Functions:
There are functions to obtain token balance and total token supply.
These functions provide information about the token and its supply, and can be used to calculate the fees that users can claim.

#### Expense Claim Functions:
There is a function for users to claim fees that have been collected from certain tokens.
The batchClaiming function allows users to claim fees from multiple tokens at once.

#### Cost Addition Functions:
The addFees function allows adding fees to a contract for a specific token.

#### Cost Information Update Functions:
Functions such as updateFeeCredit and onBalanceChange are responsible for updating fee information when changes occur in the user's balance or token supply.

#### Security:
The contract implements a level of security through inheritance from the Security contract.

#### Customization and Settings:
The use of data structures and internal functions allows for necessary adjustments and settings.

#### Event and Replacement Function:
The FeesClaimed event is used to record successful expense claims.
There is also a fallback (accept) function for receiving Ether.

#### Importance of External Context:
Some functions, such as balanceOf and totalSupply, depend on the implementation of external contracts such as Curves.
The context of the external contract and its functionality may influence the final interpretation of some functions.


### 1.1 Contract Summary

| Contract                   | Type            | Bases                     | Function Name                      | Visibility        | Mutability      | Modifiers        |
| -------------------------- | --------------- | ------------------------- | ---------------------------------- | ------------------ | --------------- | ---------------- |
| MockERC20                  | Implementation  | ERC20                     | Public ❗️                          | Public ❗️         | 🛑              | ERC20            |
|                            |                 |                           | mint                               | Public ❗️         | 🛑              | NO❗️             |
|                            |                 |                           | burn                               | Public ❗️         | 🛑              | NO❗️             |
|                            |                 |                           | decimals                           | Public ❗️         |                 | NO❗️             |
| MockCurvesForFee           | Implementation  |                           | curvesTokenBalance                  | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | curvesTokenSupply                   | Public ❗️         |                 | NO❗️             |
| Security                   | Implementation  |                           | Public ❗️                          | Public ❗️         | 🛑              | NO❗️             |
|                            |                 |                           | setManager                         | Public ❗️         | 🛑              | onlyOwner         |
|                            |                 |                           | transferOwnership                  | Public ❗️         | 🛑              | onlyOwner         |
| FeeSplitter                | Implementation  | Security                  | Public ❗️                          | Public ❗️         | 🛑              | Security         |
|                            |                 |                           | setCurves                          | Public ❗️         | 🛑              | NO❗️             |
|                            |                 |                           | balanceOf                          | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | totalSupply                        | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | getUserTokens                      | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | getUserTokensAndClaimable          | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | updateFeeCredit                    | Internal 🔒        | 🛑              |                  |
|                            |                 |                           | getClaimableFees                   | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | claimFees                          | External ❗️       | 🛑              | NO❗️             |
|                            |                 |                           | addFees                            | Public ❗️         | 💵              | onlyManager       |
|                            |                 |                           | onBalanceChange                    | Public ❗️         | 🛑              | onlyManager       |
|                            |                 |                           | batchClaiming                      | External ❗️       | 🛑              | NO❗️             |
|                            |                 |                           |                                  | External ❗️       | 💵              | NO❗️             |
| CurvesERC20Factory         | Implementation  |                           | deploy                            | Public ❗️         | 🛑              | NO❗️             |
| CurvesERC20                | Implementation  | ERC20, Ownable            | Public ❗️                          | Public ❗️         | 🛑              | ERC20            |
|                            |                 |                           | mint                               | Public ❗️         | 🛑              | onlyOwner         |
|                            |                 |                           | burn                               | Public ❗️         | 🛑              | onlyOwner         |
| CurvesErrors               | Interface       |                           |                                  |                  |                 |                  |
| Curves                     | Implementation  | CurvesErrors, Security     | Public ❗️                          | Public ❗️         | 🛑              | Security         |
|                            |                 |                           | setFeeRedistributor                | External ❗️       | 🛑              | onlyOwner         |
|                            |                 |                           | setMaxFeePercent                   | External ❗️       | 🛑              | onlyManager       |
|                            |                 |                           | setProtocolFeePercent              | External ❗️       | 🛑              | onlyOwner         |
|                            |                 |                           | setExternalFeePercent              | External ❗️       | 🛑              | onlyManager       |
|                            |                 |                           | setReferralFeeDestination          | Public ❗️         | 🛑              | onlyTokenSubject  |
|                            |                 |                           | setERC20Factory                    | External ❗️       | 🛑              | onlyOwner         |
|                            |                 |                           | getFees                            | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | getPrice                           | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | getBuyPrice                        | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | getSellPrice                       | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | getBuyPriceAfterFee                | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | getSellPriceAfterFee               | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | buyCurvesToken                     | Public ❗️         | 💵              | NO❗️             |
|                            |                 |                           | _transferFees                      | Internal 🔒        | 🛑              |                  |
|                            |                 |                           | _buyCurvesToken                    | Internal 🔒        | 🛑              |                  |
|                            |                 |                           | sellCurvesToken                    | Public ❗️         | 🛑              | NO❗️             |
|                            |                 |                           | transferCurvesToken                | External ❗️       | 🛑              | NO❗️             |
|                            |                 |                           | transferAllCurvesTokens             | External ❗️       | 🛑              | NO❗️             |
|                            |                 |                           | _transfer                          | Internal 🔒        | 🛑              |                  |
|                            |                 |                           | _addOwnedCurvesTokenSubject        | Internal 🔒        | 🛑              |                  |
|                            |                 |                           | _deployERC20                       | Internal 🔒        | 🛑              |                  |
|                            |                 |                           | buyCurvesTokenWithName              | Public ❗️         | 💵              | NO❗️             |
|                            |                 |                           | buyCurvesTokenForPresale           | Public ❗️         | 💵              | onlyTokenSubject  |
|                            |                 |                           | setWhitelist                       | External ❗️       | 🛑              | NO❗️             |
|                            |                 |                           | buyCurvesTokenWhitelisted          | Public ❗️         | 💵              | NO❗️             |
|                            |                 |                           | verifyMerkle                       | Public ❗️         |                 | NO❗️             |
|                            |                 |                           | setNameAndSymbol                   | External ❗️       | 🛑              | onlyTokenSubject  |
|                            |                 |                           | mint                               | External ❗️       | 🛑              | onlyTokenSubject  |
|                            |                 |                           | _mint                              | Internal 🔒        | 🛑              | onlyTokenSubject  |
|                            |                 |                           | withdraw                           | Public ❗️         | 🛑              | NO❗️             |
|                            |                 |                           | deposit                            | Public ❗️         | 🛑              | NO❗️             |
|                            |                 |                           | sellExternalCurvesToken            | Public ❗️         | 🛑              | NO❗️             |


| Symbol | Meaning                           |
| ------ | --------------------------------- |
| 🛑      | Function can modify state         |
| 💵      | Function is payable               |



### 1.2 Inheritance Graph

![Inheritance Graph](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/a94c965f-ac37-4b60-be54-39ba983c082f)


### 1.3 CallGraph

![callgraphs1](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/840164ba-eda9-449d-9199-33c165b1df46)
![callgraphs2](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/14792bc3-6e19-452c-845d-8c29797d9c07)
![carallgraps4](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/094ba8bf-77fa-4ca0-81d7-52101a80538b)
![callgraphs5](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/9167c244-e505-4485-8eae-16bd10f7a4b7)
![callgraphs3](https://github.com/yongsxyz/Audit-Analysis/assets/39027215/b3431dcd-701f-4a1e-9cb8-d74594a56878)

# Tree Code 
```
src\Curves.sol 0.8.7
├── lib/openzeppelin-contracts/contracts/utils/Strings.sol ^0.8.0
│   ├── lib/openzeppelin-contracts/contracts/utils/math/Math.sol ^0.8.0
│   └── lib/openzeppelin-contracts/contracts/utils/math/SignedMath.sol ^0.8.0
├── lib/openzeppelin-contracts/contracts/utils/cryptography/MerkleProof.sol ^0.8.0
├── src\CurvesERC20.sol 0.8.7
│   ├── lib/openzeppelin-contracts/contracts/access/Ownable.sol ^0.8.0
│   │   └── lib/openzeppelin-contracts/contracts/utils/Context.sol ^0.8.0
│   └── lib/openzeppelin-contracts/contracts/token/ERC20/ERC20.sol ^0.8.0
│       ├── lib/openzeppelin-contracts/contracts/token/ERC20/IERC20.sol ^0.8.0
│       ├── lib/openzeppelin-contracts/contracts/token/ERC20/extensions/IERC20Metadata.sol ^0.8.0
│       │   └── lib/openzeppelin-contracts/contracts/token/ERC20/IERC20.sol ^0.8.0
│       └── lib/openzeppelin-contracts/contracts/utils/Context.sol ^0.8.0
├── src\CurvesERC20Factory.sol 0.8.7
│   └── src\CurvesERC20.sol 0.8.7 (*)
├── src\FeeSplitter.sol ^0.8.7
│   ├── src\Curves.sol 0.8.7 (*)
│   ├── src\Security.sol ^0.8.7
│   └── lib/openzeppelin-contracts/contracts/token/ERC20/IERC20.sol ^0.8.0
└── src\Security.sol ^0.8.7
src\CurvesERC20.sol 0.8.7 (*)
src\CurvesERC20Factory.sol 0.8.7 (*)
src\FeeSplitter.sol ^0.8.7 (*)
src\Security.sol ^0.8.7
```

# Centralization and admin configuration
## Centralization Risks: 

there are centralization risks and potential issues that need attention:

#### Owner Control:
The onlyOwner modifier is used in the Security contract and its derivatives. This means that the owner has exclusive control over critical functions. Centralization of control in a single address can be risky, as it poses a security threat if the owner's account is compromised.

#### Manager Control:
The onlyManager modifier is used in the FeeSplitter contract, allowing certain addresses to have managerial control. The assignment of managers is controlled by the owner. This centralization of managerial control might be a risk if not carefully managed.

#### Fee Distribution:
The FeeSplitter contract implements a mechanism for fee distribution. However, the owner has the authority to set managers and adjust fees, which could be a centralization risk. Additionally, the use of payable functions for transferring funds may pose security risks, and it's important to consider reentrancy protection.

#### ERC-20 Deployment:
The _deployERC20 function in the Curves contract allows the owner to deploy ERC-20 tokens for different subjects. The centralized deployment of ERC-20 tokens might be a concern, especially if there's no transparent and decentralized process for adding new tokens.

#### Presale:
The buyCurvesTokenForPresale function allows the owner to initiate presales for specific subjects. Presale management could introduce centralization risks, and careful consideration should be given to ensure fairness and transparency.

#### Merkle Tree for Whitelisting:
The use of a Merkle tree for whitelisting in presales is a good practice, but it's important to ensure that the merkle roots are securely managed and not subject to central manipulation.

#### Fallback Function:
The receive() external payable function in FeeSplitter should be used cautiously. It's a fallback function that allows the contract to receive Ether. Ensure that it's secure and can't be exploited.

#### External Calls:
External calls to other contracts, especially when transferring Ether, should be handled with caution. Check for reentrancy issues and ensure that external calls are secure.

# Slither Analysis

``` txt
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IERC20hTokenRoot.sol#2) allows old versions
Pragma version^0.8.0 (src/token/ERC20hTokenRoot.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IERC20hTokenBranch.sol#2) allows old versions
Pragma version^0.8.0 (src/token/ERC20hTokenBranch.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
BranchBridgeAgent._performFallbackCall(address,uint32) (src/BranchBridgeAgent.sol#785-795) sends eth to arbitrary user
	Dangerous calls:
	- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(rootChainId,rootBridgeAgentPath,abi.encodePacked(bytes1(0x09),_settlementNonce),_refundee,address(0),) (src/BranchBridgeAgent.sol#787-794)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#functions-that-send-ether-to-arbitrary-destinations
INFO:Detectors:
Reentrancy in BranchBridgeAgent.redeemDeposit(uint32) (src/BranchBridgeAgent.sol#434-457):
	External calls:
	- _clearToken(msg.sender,deposit.hTokens[i],deposit.tokens[i],deposit.amounts[i],deposit.deposits[i]) (src/BranchBridgeAgent.sol#448)
		- IBranchPort(localPortAddress).bridgeIn(_recipient,_hToken,_amount - _deposit) (src/BranchBridgeAgent.sol#908)
		- IBranchPort(localPortAddress).withdraw(_recipient,_token,_deposit) (src/BranchBridgeAgent.sol#913)
	State variables written after the call(s):
	- delete getDeposit[_depositNonce] (src/BranchBridgeAgent.sol#456)
	BranchBridgeAgent.getDeposit (src/BranchBridgeAgent.sol#87) can be used in cross function reentrancies:
	- BranchBridgeAgent._createDeposit(uint32,address,address,address,uint256,uint256) (src/BranchBridgeAgent.sol#812-847)
	- BranchBridgeAgent._createDepositMultiple(uint32,address,address[],address[],uint256[],uint256[]) (src/BranchBridgeAgent.sol#860-888)
	- BranchBridgeAgent.getDeposit (src/BranchBridgeAgent.sol#87)
	- BranchBridgeAgent.getDepositEntry(uint32) (src/BranchBridgeAgent.sol#156-158)
	- BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes) (src/BranchBridgeAgent.sol#587-701)
	- BranchBridgeAgent.redeemDeposit(uint32) (src/BranchBridgeAgent.sol#434-457)
	- BranchBridgeAgent.retrieveDeposit(uint32,GasParams) (src/BranchBridgeAgent.sol#422-431)
	- BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool) (src/BranchBridgeAgent.sol#343-419)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-1
INFO:Detectors:
BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool).payload (src/BranchBridgeAgent.sol#357) is a local variable never initialized
BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes).nonce (src/BranchBridgeAgent.sol#596) is a local variable never initialized
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-local-variables
INFO:Detectors:
BranchBridgeAgent.lzReceive(uint16,bytes,uint64,bytes) (src/BranchBridgeAgent.sol#578-584) ignores return value by address(this).excessivelySafeCall(gasleft()(),150,abi.encodeWithSelector(this.lzReceiveNonBlocking.selector,msg.sender,_srcAddress,_payload)) (src/BranchBridgeAgent.sol#579-583)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unused-return
INFO:Detectors:
BranchBridgeAgent._clearToken(address,address,address,uint256,uint256) (src/BranchBridgeAgent.sol#903-915) has external calls inside a loop: IBranchPort(localPortAddress).bridgeIn(_recipient,_hToken,_amount - _deposit) (src/BranchBridgeAgent.sol#908)
BranchBridgeAgent._clearToken(address,address,address,uint256,uint256) (src/BranchBridgeAgent.sol#903-915) has external calls inside a loop: IBranchPort(localPortAddress).withdraw(_recipient,_token,_deposit) (src/BranchBridgeAgent.sol#913)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation/#calls-inside-a-loop
INFO:Detectors:
Reentrancy in BranchBridgeAgent._createDeposit(uint32,address,address,address,uint256,uint256) (src/BranchBridgeAgent.sol#812-847):
	External calls:
	- IBranchPort(localPortAddress).bridgeOut(msg.sender,_hToken,_token,_amount,_deposit) (src/BranchBridgeAgent.sol#824)
	State variables written after the call(s):
	- deposit.owner = _refundee (src/BranchBridgeAgent.sol#832)
	- deposit.hTokens = addressArray (src/BranchBridgeAgent.sol#835)
	- deposit.tokens = addressArray (src/BranchBridgeAgent.sol#838)
	- deposit.amounts = uintArray (src/BranchBridgeAgent.sol#841)
	- deposit.deposits = uintArray (src/BranchBridgeAgent.sol#844)
	- deposit.status = STATUS_SUCCESS (src/BranchBridgeAgent.sol#846)
Reentrancy in BranchBridgeAgent._createDepositMultiple(uint32,address,address[],address[],uint256[],uint256[]) (src/BranchBridgeAgent.sol#860-888):
	External calls:
	- IBranchPort(localPortAddress).bridgeOutMultiple(msg.sender,_hTokens,_tokens,_amounts,_deposits) (src/BranchBridgeAgent.sol#878)
	State variables written after the call(s):
	- deposit.owner = _refundee (src/BranchBridgeAgent.sol#882)
	- deposit.hTokens = _hTokens (src/BranchBridgeAgent.sol#883)
	- deposit.tokens = _tokens (src/BranchBridgeAgent.sol#884)
	- deposit.amounts = _amounts (src/BranchBridgeAgent.sol#885)
	- deposit.deposits = _deposits (src/BranchBridgeAgent.sol#886)
	- deposit.status = STATUS_SUCCESS (src/BranchBridgeAgent.sol#887)
Reentrancy in BranchBridgeAgent._execute(bool,uint32,address,bytes) (src/BranchBridgeAgent.sol#730-753):
	External calls:
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#737)
	State variables written after the call(s):
	- executionState[_settlementNonce] = STATUS_RETRIEVE (src/BranchBridgeAgent.sol#744)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-2
INFO:Detectors:
Reentrancy in BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes) (src/BranchBridgeAgent.sol#587-701):
	External calls:
	- _execute(nonce,abi.encodeWithSelector(BranchBridgeAgentExecutor.executeNoSettlement.selector,localRouterAddress,_payload)) (src/BranchBridgeAgent.sol#608-613)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#717)
	- _execute(_payload[0] == 0x81,nonce,recipient,abi.encodeWithSelector(BranchBridgeAgentExecutor.executeWithSettlement.selector,recipient,localRouterAddress,_payload)) (src/BranchBridgeAgent.sol#628-635)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(rootChainId,rootBridgeAgentPath,abi.encodePacked(bytes1(0x09),_settlementNonce),_refundee,address(0),) (src/BranchBridgeAgent.sol#787-794)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#737)
	- _execute(_payload[0] == 0x82,nonce,recipient_scope_0,abi.encodeWithSelector(BranchBridgeAgentExecutor.executeWithSettlementMultiple.selector,recipient_scope_0,localRouterAddress,_payload)) (src/BranchBridgeAgent.sol#650-660)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(rootChainId,rootBridgeAgentPath,abi.encodePacked(bytes1(0x09),_settlementNonce),_refundee,address(0),) (src/BranchBridgeAgent.sol#787-794)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#737)
	- _performFallbackCall(recipient_scope_1,nonce) (src/BranchBridgeAgent.sol#677)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(rootChainId,rootBridgeAgentPath,abi.encodePacked(bytes1(0x09),_settlementNonce),_refundee,address(0),) (src/BranchBridgeAgent.sol#787-794)
	Event emitted after the call(s):
	- LogExecute(nonce) (src/BranchBridgeAgent.sol#700)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-3
INFO:Detectors:
Pragma version^0.8.0 (src/BranchBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/BranchBridgeAgentExecutor.sol#2) allows old versions
Pragma version^0.8.0 (src/factories/BranchBridgeAgentFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentConstants.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgentFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchPort.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchRouter.sol#2) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroEndpoint.sol#3) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroUserApplicationConfig.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Low level call in BranchBridgeAgent._execute(uint256,bytes) (src/BranchBridgeAgent.sol#712-721):
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#717)
Low level call in BranchBridgeAgent._execute(bool,uint32,address,bytes) (src/BranchBridgeAgent.sol#730-753):
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#737)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#low-level-calls
INFO:Detectors:
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._rootChainId (src/BranchBridgeAgent.sol#25) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._localChainId (src/BranchBridgeAgent.sol#26) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._rootBridgeAgentAddress (src/BranchBridgeAgent.sol#27) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._lzEndpointAddress (src/BranchBridgeAgent.sol#28) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._localRouterAddress (src/BranchBridgeAgent.sol#29) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._localPortAddress (src/BranchBridgeAgent.sol#30) is not in mixedCase
Parameter BranchBridgeAgent.getDepositEntry(uint32)._depositNonce (src/BranchBridgeAgent.sol#156) is not in mixedCase
Parameter BranchBridgeAgent.getFeeEstimate(uint256,uint256,bytes)._gasLimit (src/BranchBridgeAgent.sol#161) is not in mixedCase
Parameter BranchBridgeAgent.getFeeEstimate(uint256,uint256,bytes)._remoteBranchExecutionGas (src/BranchBridgeAgent.sol#161) is not in mixedCase
Parameter BranchBridgeAgent.getFeeEstimate(uint256,uint256,bytes)._payload (src/BranchBridgeAgent.sol#161) is not in mixedCase
Parameter BranchBridgeAgent.callOutSystem(address,bytes,GasParams)._refundee (src/BranchBridgeAgent.sol#180) is not in mixedCase
Parameter BranchBridgeAgent.callOutSystem(address,bytes,GasParams)._params (src/BranchBridgeAgent.sol#180) is not in mixedCase
Parameter BranchBridgeAgent.callOutSystem(address,bytes,GasParams)._gParams (src/BranchBridgeAgent.sol#180) is not in mixedCase
Parameter BranchBridgeAgent.callOut(address,bytes,GasParams)._refundee (src/BranchBridgeAgent.sol#195) is not in mixedCase
Parameter BranchBridgeAgent.callOut(address,bytes,GasParams)._params (src/BranchBridgeAgent.sol#195) is not in mixedCase
Parameter BranchBridgeAgent.callOut(address,bytes,GasParams)._gParams (src/BranchBridgeAgent.sol#195) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridge(address,bytes,DepositInput,GasParams)._refundee (src/BranchBridgeAgent.sol#210) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridge(address,bytes,DepositInput,GasParams)._params (src/BranchBridgeAgent.sol#211) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridge(address,bytes,DepositInput,GasParams)._dParams (src/BranchBridgeAgent.sol#212) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridge(address,bytes,DepositInput,GasParams)._gParams (src/BranchBridgeAgent.sol#213) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams)._refundee (src/BranchBridgeAgent.sol#232) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams)._params (src/BranchBridgeAgent.sol#233) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams)._dParams (src/BranchBridgeAgent.sol#234) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams)._gParams (src/BranchBridgeAgent.sol#235) is not in mixedCase
Parameter BranchBridgeAgent.callOutSigned(address,bytes,GasParams)._refundee (src/BranchBridgeAgent.sol#262) is not in mixedCase
Parameter BranchBridgeAgent.callOutSigned(address,bytes,GasParams)._params (src/BranchBridgeAgent.sol#262) is not in mixedCase
Parameter BranchBridgeAgent.callOutSigned(address,bytes,GasParams)._gParams (src/BranchBridgeAgent.sol#262) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._refundee (src/BranchBridgeAgent.sol#277) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._params (src/BranchBridgeAgent.sol#278) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._dParams (src/BranchBridgeAgent.sol#279) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._gParams (src/BranchBridgeAgent.sol#280) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._hasFallbackToggled (src/BranchBridgeAgent.sol#281) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._refundee (src/BranchBridgeAgent.sol#307) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._params (src/BranchBridgeAgent.sol#308) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._dParams (src/BranchBridgeAgent.sol#309) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._gParams (src/BranchBridgeAgent.sol#310) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._hasFallbackToggled (src/BranchBridgeAgent.sol#311) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._isSigned (src/BranchBridgeAgent.sol#344) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._depositNonce (src/BranchBridgeAgent.sol#345) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._params (src/BranchBridgeAgent.sol#346) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._gParams (src/BranchBridgeAgent.sol#347) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._hasFallbackToggled (src/BranchBridgeAgent.sol#348) is not in mixedCase
Parameter BranchBridgeAgent.retrieveDeposit(uint32,GasParams)._depositNonce (src/BranchBridgeAgent.sol#422) is not in mixedCase
Parameter BranchBridgeAgent.retrieveDeposit(uint32,GasParams)._gParams (src/BranchBridgeAgent.sol#422) is not in mixedCase
Parameter BranchBridgeAgent.redeemDeposit(uint32)._depositNonce (src/BranchBridgeAgent.sol#434) is not in mixedCase
Parameter BranchBridgeAgent.retrySettlement(uint32,bytes,GasParams[2],bool)._settlementNonce (src/BranchBridgeAgent.sol#465) is not in mixedCase
Parameter BranchBridgeAgent.retrySettlement(uint32,bytes,GasParams[2],bool)._params (src/BranchBridgeAgent.sol#466) is not in mixedCase
Parameter BranchBridgeAgent.retrySettlement(uint32,bytes,GasParams[2],bool)._gParams (src/BranchBridgeAgent.sol#467) is not in mixedCase
Parameter BranchBridgeAgent.retrySettlement(uint32,bytes,GasParams[2],bool)._hasFallbackToggled (src/BranchBridgeAgent.sol#468) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._recipient (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._hToken (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._token (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._amount (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._deposit (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearTokens(bytes,address)._sParams (src/BranchBridgeAgent.sol#494) is not in mixedCase
Parameter BranchBridgeAgent.clearTokens(bytes,address)._recipient (src/BranchBridgeAgent.sol#494) is not in mixedCase
Parameter BranchBridgeAgent.lzReceive(uint16,bytes,uint64,bytes)._srcAddress (src/BranchBridgeAgent.sol#578) is not in mixedCase
Parameter BranchBridgeAgent.lzReceive(uint16,bytes,uint64,bytes)._payload (src/BranchBridgeAgent.sol#578) is not in mixedCase
Parameter BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes)._endpoint (src/BranchBridgeAgent.sol#587) is not in mixedCase
Parameter BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes)._srcAddress (src/BranchBridgeAgent.sol#587) is not in mixedCase
Parameter BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes)._payload (src/BranchBridgeAgent.sol#587) is not in mixedCase
Variable BranchBridgeAgent._unlocked (src/BranchBridgeAgent.sol#101) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeNoSettlement(address,bytes)._router (src/BranchBridgeAgentExecutor.sol#53) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeNoSettlement(address,bytes)._payload (src/BranchBridgeAgentExecutor.sol#53) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlement(address,address,bytes)._recipient (src/BranchBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlement(address,address,bytes)._router (src/BranchBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlement(address,address,bytes)._payload (src/BranchBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlementMultiple(address,address,bytes)._recipient (src/BranchBridgeAgentExecutor.sol#104) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlementMultiple(address,address,bytes)._router (src/BranchBridgeAgentExecutor.sol#104) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlementMultiple(address,address,bytes)._payload (src/BranchBridgeAgentExecutor.sol#104) is not in mixedCase
Parameter BranchBridgeAgentFactory.initialize(address)._coreRootBridgeAgent (src/factories/BranchBridgeAgentFactory.sol#87) is not in mixedCase
Parameter BranchBridgeAgentFactory.createBridgeAgent(address,address,address)._newBranchRouterAddress (src/factories/BranchBridgeAgentFactory.sol#116) is not in mixedCase
Parameter BranchBridgeAgentFactory.createBridgeAgent(address,address,address)._rootBridgeAgentAddress (src/factories/BranchBridgeAgentFactory.sol#117) is not in mixedCase
Parameter BranchBridgeAgentFactory.createBridgeAgent(address,address,address)._rootBridgeAgentFactoryAddress (src/factories/BranchBridgeAgentFactory.sol#118) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
Variable BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes).recipient_scope_0 (src/BranchBridgeAgent.sol#640) is too similar to BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes).recipient_scope_1 (src/BranchBridgeAgent.sol#665)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#variable-names-too-similar
INFO:Detectors:
BridgeAgentConstants.PARAMS_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#29) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_TKN_START (src/interfaces/BridgeAgentConstants.sol#31) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_TKN_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#33) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_ENTRY_SIZE (src/interfaces/BridgeAgentConstants.sol#35) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_ADDRESS_SIZE (src/interfaces/BridgeAgentConstants.sol#37) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_TKN_SET_SIZE (src/interfaces/BridgeAgentConstants.sol#39) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_TKN_SET_SIZE_MULTIPLE (src/interfaces/BridgeAgentConstants.sol#41) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.ADDRESS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#43) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_AMT_OFFSET (src/interfaces/BridgeAgentConstants.sol#45) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_DEPOSIT_OFFSET (src/interfaces/BridgeAgentConstants.sol#47) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#49) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_END_SIGNED_OFFSET (src/interfaces/BridgeAgentConstants.sol#51) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.PARAMS_SETTLEMENT_OFFSET (src/interfaces/BridgeAgentConstants.sol#53) is never used in BranchBridgeAgent (src/BranchBridgeAgent.sol#45-957)
BridgeAgentConstants.STATUS_READY (src/interfaces/BridgeAgentConstants.sol#13) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.STATUS_DONE (src/interfaces/BridgeAgentConstants.sol#15) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.STATUS_RETRIEVE (src/interfaces/BridgeAgentConstants.sol#17) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.STATUS_FAILED (src/interfaces/BridgeAgentConstants.sol#21) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.STATUS_SUCCESS (src/interfaces/BridgeAgentConstants.sol#23) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_START (src/interfaces/BridgeAgentConstants.sol#27) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_TKN_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#33) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_ENTRY_SIZE (src/interfaces/BridgeAgentConstants.sol#35) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_ADDRESS_SIZE (src/interfaces/BridgeAgentConstants.sol#37) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_TKN_SET_SIZE (src/interfaces/BridgeAgentConstants.sol#39) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.ADDRESS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#43) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_AMT_OFFSET (src/interfaces/BridgeAgentConstants.sol#45) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_DEPOSIT_OFFSET (src/interfaces/BridgeAgentConstants.sol#47) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#49) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_END_SIGNED_OFFSET (src/interfaces/BridgeAgentConstants.sol#51) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.MAX_TOKENS_LENGTH (src/interfaces/BridgeAgentConstants.sol#57) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unused-state-variable
INFO:Detectors:
ERC20hTokenBranchFactory.initialize(address,address) (src/factories/ERC20hTokenBranchFactory.sol#60-77) should emit an event for: 
	- localCoreRouterAddress = _coreRouter (src/factories/ERC20hTokenBranchFactory.sol#74) 
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#missing-events-access-control
INFO:Detectors:
Pragma version^0.8.0 (src/factories/ERC20hTokenBranchFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IERC20hTokenBranch.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IERC20hTokenBranchFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/token/ERC20hTokenBranch.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Parameter ERC20hTokenBranchFactory.initialize(address,address)._wrappedNativeTokenAddress (src/factories/ERC20hTokenBranchFactory.sol#60) is not in mixedCase
Parameter ERC20hTokenBranchFactory.initialize(address,address)._coreRouter (src/factories/ERC20hTokenBranchFactory.sol#60) is not in mixedCase
Parameter ERC20hTokenBranchFactory.createToken(string,string,uint8,bool)._name (src/factories/ERC20hTokenBranchFactory.sol#96) is not in mixedCase
Parameter ERC20hTokenBranchFactory.createToken(string,string,uint8,bool)._symbol (src/factories/ERC20hTokenBranchFactory.sol#96) is not in mixedCase
Parameter ERC20hTokenBranchFactory.createToken(string,string,uint8,bool)._decimals (src/factories/ERC20hTokenBranchFactory.sol#96) is not in mixedCase
Parameter ERC20hTokenBranchFactory.createToken(string,string,uint8,bool)._addPrefix (src/factories/ERC20hTokenBranchFactory.sol#96) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
RootBridgeAgent._performFallbackCall(address,uint32,uint16) (src/RootBridgeAgent.sol#938-948) sends eth to arbitrary user
	Dangerous calls:
	- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],abi.encodePacked(bytes1(0x04),_depositNonce),address(_refundee),address(0),) (src/RootBridgeAgent.sol#940-947)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#functions-that-send-ether-to-arbitrary-destinations
INFO:Detectors:
Reentrancy in RootBridgeAgent.redeemSettlement(uint32) (src/RootBridgeAgent.sol#299-344):
	External calls:
	- IRootPort(localPortAddress).bridgeToRoot(msg.sender,IRootPort(localPortAddress).getGlobalTokenFromLocal(_hToken,_dstChainId),settlement.amounts[i],settlement.deposits[i],_dstChainId) (src/RootBridgeAgent.sol#328-334)
	State variables written after the call(s):
	- delete getSettlement[_settlementNonce] (src/RootBridgeAgent.sol#343)
	RootBridgeAgent.getSettlement (src/RootBridgeAgent.sol#78) can be used in cross function reentrancies:
	- RootBridgeAgent._createSettlement(uint32,address,address,uint16,bytes,address,uint256,uint256,bool) (src/RootBridgeAgent.sol#966-1031)
	- RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool) (src/RootBridgeAgent.sol#1045-1114)
	- RootBridgeAgent.getSettlement (src/RootBridgeAgent.sol#78)
	- RootBridgeAgent.getSettlementEntry(uint32) (src/RootBridgeAgent.sol#135-137)
	- RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes) (src/RootBridgeAgent.sol#434-737)
	- RootBridgeAgent.redeemSettlement(uint32) (src/RootBridgeAgent.sol#299-344)
	- RootBridgeAgent.retrieveSettlement(uint32,GasParams) (src/RootBridgeAgent.sol#274-296)
	- RootBridgeAgent.retrySettlement(uint32,address,bytes,GasParams,bool) (src/RootBridgeAgent.sol#233-271)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-1
INFO:Detectors:
RootBridgeAgent._performCall(uint16,address,bytes,GasParams) (src/RootBridgeAgent.sol#808-839) ignores return value by callee.call{value: msg.value}() (src/RootBridgeAgent.sol#835)
RootBridgeAgent._performRetrySettlementCall(bool,address[],address[],uint256[],uint256[],bytes,uint32,address,address,uint16,GasParams,uint256) (src/RootBridgeAgent.sol#856-931) ignores return value by callee.call{value: _value}() (src/RootBridgeAgent.sol#927)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unchecked-low-level-calls
INFO:Detectors:
RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).nonce (src/RootBridgeAgent.sol#441) is a local variable never initialized
RootBridgeAgent._performRetrySettlementCall(bool,address[],address[],uint256[],uint256[],bytes,uint32,address,address,uint16,GasParams,uint256).payload (src/RootBridgeAgent.sol#874) is a local variable never initialized
VirtualAccount.call(Call[]).success (src/VirtualAccount.sol#71) is a local variable never initialized
VirtualAccount.payableCall(PayableCall[]).success (src/VirtualAccount.sol#99) is a local variable never initialized
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-local-variables
INFO:Detectors:
VirtualAccount.constructor(address,address)._userAddress (src/VirtualAccount.sol#35) lacks a zero-check on :
		- userAddress = _userAddress (src/VirtualAccount.sol#36)
VirtualAccount.constructor(address,address)._localPortAddress (src/VirtualAccount.sol#35) lacks a zero-check on :
		- localPortAddress = _localPortAddress (src/VirtualAccount.sol#37)
RootBridgeAgentFactory.constructor(uint16,address,address)._lzEndpointAddress (src/factories/RootBridgeAgentFactory.sol#31) lacks a zero-check on :
		- lzEndpointAddress = _lzEndpointAddress (src/factories/RootBridgeAgentFactory.sol#35)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#missing-zero-address-validation
INFO:Detectors:
RootBridgeAgent.redeemSettlement(uint32) (src/RootBridgeAgent.sol#299-344) has external calls inside a loop: IRootPort(localPortAddress).bridgeToRoot(msg.sender,IRootPort(localPortAddress).getGlobalTokenFromLocal(_hToken,_dstChainId),settlement.amounts[i],settlement.deposits[i],_dstChainId) (src/RootBridgeAgent.sol#328-334)
RootBridgeAgent.bridgeIn(address,DepositParams,uint256) (src/RootBridgeAgent.sol#351-384) has external calls inside a loop: ! IRootPort(_localPortAddress).isLocalToken(_dParams.hToken,_srcChainId) (src/RootBridgeAgent.sol#364)
RootBridgeAgent.bridgeIn(address,DepositParams,uint256) (src/RootBridgeAgent.sol#351-384) has external calls inside a loop: IRootPort(_localPortAddress).getLocalTokenFromUnderlying(_dParams.token,_srcChainId) != _dParams.hToken (src/RootBridgeAgent.sol#371)
RootBridgeAgent.bridgeIn(address,DepositParams,uint256) (src/RootBridgeAgent.sol#351-384) has external calls inside a loop: IRootPort(_localPortAddress).bridgeToRoot(_recipient,IRootPort(_localPortAddress).getGlobalTokenFromLocal(_dParams.hToken,_srcChainId),_dParams.amount,_dParams.deposit,_srcChainId) (src/RootBridgeAgent.sol#377-383)
VirtualAccount.call(Call[]) (src/VirtualAccount.sol#66-82) has external calls inside a loop: (success,returnData[i]) = _call.target.call(_call.callData) (src/VirtualAccount.sol#74)
VirtualAccount.payableCall(PayableCall[]) (src/VirtualAccount.sol#85-112) has external calls inside a loop: (success,returnData[i]) = _call.target.call{value: val}(_call.callData) (src/VirtualAccount.sol#101)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation/#calls-inside-a-loop
INFO:Detectors:
Reentrancy in RootBridgeAgent._createSettlement(uint32,address,address,uint16,bytes,address,uint256,uint256,bool) (src/RootBridgeAgent.sol#966-1031):
	External calls:
	- _updateStateOnBridgeOut(msg.sender,_globalAddress,localAddress,underlyingAddress,_amount,_deposit,_dstChainId) (src/RootBridgeAgent.sol#987-989)
		- IRootPort(localPortAddress).burn(_depositor,_globalAddress,_deposit,_dstChainId) (src/RootBridgeAgent.sol#1161)
	State variables written after the call(s):
	- settlement.owner = _refundee (src/RootBridgeAgent.sol#1014)
	- settlement.recipient = _recipient (src/RootBridgeAgent.sol#1015)
	- settlement.hTokens = addressArray (src/RootBridgeAgent.sol#1018)
	- settlement.tokens = addressArray (src/RootBridgeAgent.sol#1021)
	- settlement.amounts = uintArray (src/RootBridgeAgent.sol#1024)
	- settlement.deposits = uintArray (src/RootBridgeAgent.sol#1027)
	- settlement.dstChainId = _dstChainId (src/RootBridgeAgent.sol#1029)
	- settlement.status = STATUS_SUCCESS (src/RootBridgeAgent.sol#1030)
Reentrancy in RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool) (src/RootBridgeAgent.sol#1045-1114):
	External calls:
	- _updateStateOnBridgeOut(msg.sender,_globalAddresses[i],hTokens[i],tokens[i],_amounts[i],_deposits[i],destChainId) (src/RootBridgeAgent.sol#1079-1081)
		- IRootPort(localPortAddress).burn(_depositor,_globalAddress,_deposit,_dstChainId) (src/RootBridgeAgent.sol#1161)
	State variables written after the call(s):
	- settlement.owner = _refundee (src/RootBridgeAgent.sol#1106)
	- settlement.recipient = _recipient (src/RootBridgeAgent.sol#1107)
	- settlement.hTokens = hTokens (src/RootBridgeAgent.sol#1108)
	- settlement.tokens = tokens (src/RootBridgeAgent.sol#1109)
	- settlement.amounts = _amounts (src/RootBridgeAgent.sol#1110)
	- settlement.deposits = _deposits (src/RootBridgeAgent.sol#1111)
	- settlement.dstChainId = _dstChainId (src/RootBridgeAgent.sol#1112)
	- settlement.status = STATUS_SUCCESS (src/RootBridgeAgent.sol#1113)
Reentrancy in RootBridgeAgent._execute(bool,uint32,address,bytes,uint16) (src/RootBridgeAgent.sol#768-794):
	External calls:
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#779)
	State variables written after the call(s):
	- executionState[_srcChainId][_depositNonce] = STATUS_RETRIEVE (src/RootBridgeAgent.sol#786)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-2
INFO:Detectors:
Reentrancy in RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes) (src/RootBridgeAgent.sol#434-737):
	External calls:
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeSystemRequest.selector,localRouterAddress,_payload,srcChainId),srcChainId) (src/RootBridgeAgent.sol#458-464)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeNoDeposit.selector,localRouterAddress,_payload,srcChainId_scope_0),srcChainId_scope_0) (src/RootBridgeAgent.sol#481-487)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeWithDeposit.selector,localRouterAddress,_payload,srcChainId_scope_1),srcChainId_scope_1) (src/RootBridgeAgent.sol#504-510)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeWithDepositMultiple.selector,localRouterAddress,_payload,srcChainId_scope_2),srcChainId_scope_2) (src/RootBridgeAgent.sol#527-536)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- userAccount = IRootPort(localPortAddress).fetchVirtualAccount(address(uint160(bytes20(_payload)))) (src/RootBridgeAgent.sol#549-551)
	- IRootPort(localPortAddress).toggleVirtualAccountApproved(userAccount,localRouterAddress) (src/RootBridgeAgent.sol#554)
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeSignedNoDeposit.selector,address(userAccount),localRouterAddress,_payload,srcChainId_scope_3),srcChainId_scope_3) (src/RootBridgeAgent.sol#561-571)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- IRootPort(localPortAddress).toggleVirtualAccountApproved(userAccount,localRouterAddress) (src/RootBridgeAgent.sol#574)
	- userAccount_scope_4 = IRootPort(localPortAddress).fetchVirtualAccount(address(uint160(bytes20(_payload)))) (src/RootBridgeAgent.sol#587-589)
	- IRootPort(localPortAddress).toggleVirtualAccountApproved(userAccount_scope_4,localRouterAddress) (src/RootBridgeAgent.sol#592)
	- _execute(_payload[0] == 0x85,nonce,address(uint160(bytes20(_payload))),abi.encodeWithSelector(RootBridgeAgentExecutor.executeSignedWithDeposit.selector,address(userAccount_scope_4),localRouterAddress,_payload,srcChainId_scope_5),srcChainId_scope_5) (src/RootBridgeAgent.sol#599-611)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],abi.encodePacked(bytes1(0x04),_depositNonce),address(_refundee),address(0),) (src/RootBridgeAgent.sol#940-947)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#779)
	- IRootPort(localPortAddress).toggleVirtualAccountApproved(userAccount_scope_4,localRouterAddress) (src/RootBridgeAgent.sol#614)
	- userAccount_scope_6 = IRootPort(localPortAddress).fetchVirtualAccount(address(uint160(bytes20(_payload)))) (src/RootBridgeAgent.sol#627-629)
	- IRootPort(localPortAddress).toggleVirtualAccountApproved(userAccount_scope_6,localRouterAddress) (src/RootBridgeAgent.sol#632)
	- _execute(_payload[0] == 0x86,nonce,address(uint160(bytes20(_payload))),abi.encodeWithSelector(RootBridgeAgentExecutor.executeSignedWithDepositMultiple.selector,address(userAccount_scope_6),localRouterAddress,_payload,srcChainId_scope_7),srcChainId_scope_7) (src/RootBridgeAgent.sol#639-651)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],abi.encodePacked(bytes1(0x04),_depositNonce),address(_refundee),address(0),) (src/RootBridgeAgent.sol#940-947)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#779)
	- IRootPort(localPortAddress).toggleVirtualAccountApproved(userAccount_scope_6,localRouterAddress) (src/RootBridgeAgent.sol#654)
	- _performRetrySettlementCall(_payload[0] == 0x87,settlementReference.hTokens,settlementReference.tokens,settlementReference.amounts,settlementReference.deposits,params,nonce,address(settlementReference.owner),settlementReference.recipient,settlementReference.dstChainId,gParams,address(this).balance) (src/RootBridgeAgent.sol#683-696)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: _value}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],payload,address(_refundee),address(0),abi.encodePacked(uint16(2),_gParams.gasLimit,_gParams.remoteBranchExecutionGas,callee)) (src/RootBridgeAgent.sol#915-922)
		- callee.call{value: _value}() (src/RootBridgeAgent.sol#927)
		- IBranchBridgeAgent(callee).lzReceive(0,,0,payload) (src/RootBridgeAgent.sol#929)
	- _performFallbackCall(address(address(uint160(bytes20(_payload)))),nonce,_srcChainId) (src/RootBridgeAgent.sol#712-714)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],abi.encodePacked(bytes1(0x04),_depositNonce),address(_refundee),address(0),) (src/RootBridgeAgent.sol#940-947)
	External calls sending eth:
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeSystemRequest.selector,localRouterAddress,_payload,srcChainId),srcChainId) (src/RootBridgeAgent.sol#458-464)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeNoDeposit.selector,localRouterAddress,_payload,srcChainId_scope_0),srcChainId_scope_0) (src/RootBridgeAgent.sol#481-487)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeWithDeposit.selector,localRouterAddress,_payload,srcChainId_scope_1),srcChainId_scope_1) (src/RootBridgeAgent.sol#504-510)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeWithDepositMultiple.selector,localRouterAddress,_payload,srcChainId_scope_2),srcChainId_scope_2) (src/RootBridgeAgent.sol#527-536)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- _execute(nonce,abi.encodeWithSelector(RootBridgeAgentExecutor.executeSignedNoDeposit.selector,address(userAccount),localRouterAddress,_payload,srcChainId_scope_3),srcChainId_scope_3) (src/RootBridgeAgent.sol#561-571)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
	- _execute(_payload[0] == 0x85,nonce,address(uint160(bytes20(_payload))),abi.encodeWithSelector(RootBridgeAgentExecutor.executeSignedWithDeposit.selector,address(userAccount_scope_4),localRouterAddress,_payload,srcChainId_scope_5),srcChainId_scope_5) (src/RootBridgeAgent.sol#599-611)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],abi.encodePacked(bytes1(0x04),_depositNonce),address(_refundee),address(0),) (src/RootBridgeAgent.sol#940-947)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#779)
	- _execute(_payload[0] == 0x86,nonce,address(uint160(bytes20(_payload))),abi.encodeWithSelector(RootBridgeAgentExecutor.executeSignedWithDepositMultiple.selector,address(userAccount_scope_6),localRouterAddress,_payload,srcChainId_scope_7),srcChainId_scope_7) (src/RootBridgeAgent.sol#639-651)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],abi.encodePacked(bytes1(0x04),_depositNonce),address(_refundee),address(0),) (src/RootBridgeAgent.sol#940-947)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#779)
	- _performRetrySettlementCall(_payload[0] == 0x87,settlementReference.hTokens,settlementReference.tokens,settlementReference.amounts,settlementReference.deposits,params,nonce,address(settlementReference.owner),settlementReference.recipient,settlementReference.dstChainId,gParams,address(this).balance) (src/RootBridgeAgent.sol#683-696)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: _value}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],payload,address(_refundee),address(0),abi.encodePacked(uint16(2),_gParams.gasLimit,_gParams.remoteBranchExecutionGas,callee)) (src/RootBridgeAgent.sol#915-922)
		- callee.call{value: _value}() (src/RootBridgeAgent.sol#927)
	- _performFallbackCall(address(address(uint160(bytes20(_payload)))),nonce,_srcChainId) (src/RootBridgeAgent.sol#712-714)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(_dstChainId,getBranchBridgeAgentPath[_dstChainId],abi.encodePacked(bytes1(0x04),_depositNonce),address(_refundee),address(0),) (src/RootBridgeAgent.sol#940-947)
	Event emitted after the call(s):
	- LogExecute(nonce,_srcChainId) (src/RootBridgeAgent.sol#736)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-3
INFO:Detectors:
VirtualAccount.isContract(address) (src/VirtualAccount.sol#147-153) uses assembly
	- INLINE ASM (src/VirtualAccount.sol#149-151)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#assembly-usage
INFO:Detectors:
RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes) (src/RootBridgeAgent.sol#434-737) has a high cyclomatic complexity (22).
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#cyclomatic-complexity
INFO:Detectors:
Pragma version^0.8.0 (src/RootBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/RootBridgeAgentExecutor.sol#2) allows old versions
Pragma version^0.8.0 (src/VirtualAccount.sol#3) allows old versions
Pragma version^0.8.0 (src/factories/RootBridgeAgentFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentConstants.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IERC20hTokenRoot.sol#2) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroEndpoint.sol#3) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroUserApplicationConfig.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootBridgeAgentFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootPort.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootRouter.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IVirtualAccount.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Low level call in RootBridgeAgent._execute(uint256,bytes,uint16) (src/RootBridgeAgent.sol#749-758):
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#754)
Low level call in RootBridgeAgent._execute(bool,uint32,address,bytes,uint16) (src/RootBridgeAgent.sol#768-794):
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/RootBridgeAgent.sol#779)
Low level call in RootBridgeAgent._performCall(uint16,address,bytes,GasParams) (src/RootBridgeAgent.sol#808-839):
	- callee.call{value: msg.value}() (src/RootBridgeAgent.sol#835)
Low level call in RootBridgeAgent._performRetrySettlementCall(bool,address[],address[],uint256[],uint256[],bytes,uint32,address,address,uint16,GasParams,uint256) (src/RootBridgeAgent.sol#856-931):
	- callee.call{value: _value}() (src/RootBridgeAgent.sol#927)
Low level call in VirtualAccount.call(Call[]) (src/VirtualAccount.sol#66-82):
	- (success,returnData[i]) = _call.target.call(_call.callData) (src/VirtualAccount.sol#74)
Low level call in VirtualAccount.payableCall(PayableCall[]) (src/VirtualAccount.sol#85-112):
	- (success,returnData[i]) = _call.target.call{value: val}(_call.callData) (src/VirtualAccount.sol#101)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#low-level-calls
INFO:Detectors:
Parameter RootBridgeAgent.getSettlementEntry(uint32)._settlementNonce (src/RootBridgeAgent.sol#135) is not in mixedCase
Parameter RootBridgeAgent.getFeeEstimate(uint256,uint256,bytes,uint16)._gasLimit (src/RootBridgeAgent.sol#141) is not in mixedCase
Parameter RootBridgeAgent.getFeeEstimate(uint256,uint256,bytes,uint16)._remoteBranchExecutionGas (src/RootBridgeAgent.sol#142) is not in mixedCase
Parameter RootBridgeAgent.getFeeEstimate(uint256,uint256,bytes,uint16)._payload (src/RootBridgeAgent.sol#143) is not in mixedCase
Parameter RootBridgeAgent.getFeeEstimate(uint256,uint256,bytes,uint16)._dstChainId (src/RootBridgeAgent.sol#144) is not in mixedCase
Parameter RootBridgeAgent.callOut(address,address,uint16,bytes,GasParams)._refundee (src/RootBridgeAgent.sol#161) is not in mixedCase
Parameter RootBridgeAgent.callOut(address,address,uint16,bytes,GasParams)._recipient (src/RootBridgeAgent.sol#162) is not in mixedCase
Parameter RootBridgeAgent.callOut(address,address,uint16,bytes,GasParams)._dstChainId (src/RootBridgeAgent.sol#163) is not in mixedCase
Parameter RootBridgeAgent.callOut(address,address,uint16,bytes,GasParams)._params (src/RootBridgeAgent.sol#164) is not in mixedCase
Parameter RootBridgeAgent.callOut(address,address,uint16,bytes,GasParams)._gParams (src/RootBridgeAgent.sol#165) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._refundee (src/RootBridgeAgent.sol#176) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._recipient (src/RootBridgeAgent.sol#177) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._dstChainId (src/RootBridgeAgent.sol#178) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._params (src/RootBridgeAgent.sol#179) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._sParams (src/RootBridgeAgent.sol#180) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._gParams (src/RootBridgeAgent.sol#181) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._hasFallbackToggled (src/RootBridgeAgent.sol#182) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._refundee (src/RootBridgeAgent.sol#203) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._recipient (src/RootBridgeAgent.sol#204) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._dstChainId (src/RootBridgeAgent.sol#205) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._params (src/RootBridgeAgent.sol#206) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._sParams (src/RootBridgeAgent.sol#207) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._gParams (src/RootBridgeAgent.sol#208) is not in mixedCase
Parameter RootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._hasFallbackToggled (src/RootBridgeAgent.sol#209) is not in mixedCase
Parameter RootBridgeAgent.retrySettlement(uint32,address,bytes,GasParams,bool)._settlementNonce (src/RootBridgeAgent.sol#234) is not in mixedCase
Parameter RootBridgeAgent.retrySettlement(uint32,address,bytes,GasParams,bool)._recipient (src/RootBridgeAgent.sol#235) is not in mixedCase
Parameter RootBridgeAgent.retrySettlement(uint32,address,bytes,GasParams,bool)._params (src/RootBridgeAgent.sol#236) is not in mixedCase
Parameter RootBridgeAgent.retrySettlement(uint32,address,bytes,GasParams,bool)._gParams (src/RootBridgeAgent.sol#237) is not in mixedCase
Parameter RootBridgeAgent.retrySettlement(uint32,address,bytes,GasParams,bool)._hasFallbackToggled (src/RootBridgeAgent.sol#238) is not in mixedCase
Parameter RootBridgeAgent.retrieveSettlement(uint32,GasParams)._settlementNonce (src/RootBridgeAgent.sol#274) is not in mixedCase
Parameter RootBridgeAgent.retrieveSettlement(uint32,GasParams)._gParams (src/RootBridgeAgent.sol#274) is not in mixedCase
Parameter RootBridgeAgent.redeemSettlement(uint32)._settlementNonce (src/RootBridgeAgent.sol#299) is not in mixedCase
Parameter RootBridgeAgent.bridgeIn(address,DepositParams,uint256)._recipient (src/RootBridgeAgent.sol#351) is not in mixedCase
Parameter RootBridgeAgent.bridgeIn(address,DepositParams,uint256)._dParams (src/RootBridgeAgent.sol#351) is not in mixedCase
Parameter RootBridgeAgent.bridgeIn(address,DepositParams,uint256)._srcChainId (src/RootBridgeAgent.sol#351) is not in mixedCase
Parameter RootBridgeAgent.bridgeInMultiple(address,DepositMultipleParams,uint256)._recipient (src/RootBridgeAgent.sol#387) is not in mixedCase
Parameter RootBridgeAgent.bridgeInMultiple(address,DepositMultipleParams,uint256)._dParams (src/RootBridgeAgent.sol#387) is not in mixedCase
Parameter RootBridgeAgent.bridgeInMultiple(address,DepositMultipleParams,uint256)._srcChainId (src/RootBridgeAgent.sol#387) is not in mixedCase
Parameter RootBridgeAgent.lzReceive(uint16,bytes,uint64,bytes)._srcChainId (src/RootBridgeAgent.sol#423) is not in mixedCase
Parameter RootBridgeAgent.lzReceive(uint16,bytes,uint64,bytes)._srcAddress (src/RootBridgeAgent.sol#423) is not in mixedCase
Parameter RootBridgeAgent.lzReceive(uint16,bytes,uint64,bytes)._payload (src/RootBridgeAgent.sol#423) is not in mixedCase
Parameter RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes)._endpoint (src/RootBridgeAgent.sol#435) is not in mixedCase
Parameter RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes)._srcChainId (src/RootBridgeAgent.sol#436) is not in mixedCase
Parameter RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes)._srcAddress (src/RootBridgeAgent.sol#437) is not in mixedCase
Parameter RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes)._payload (src/RootBridgeAgent.sol#438) is not in mixedCase
Parameter RootBridgeAgent.approveBranchBridgeAgent(uint256)._branchChainId (src/RootBridgeAgent.sol#1170) is not in mixedCase
Parameter RootBridgeAgent.syncBranchBridgeAgent(address,uint256)._newBranchBridgeAgent (src/RootBridgeAgent.sol#1176) is not in mixedCase
Parameter RootBridgeAgent.syncBranchBridgeAgent(address,uint256)._branchChainId (src/RootBridgeAgent.sol#1176) is not in mixedCase
Variable RootBridgeAgent._unlocked (src/RootBridgeAgent.sol#92) is not in mixedCase
Parameter DeployRootBridgeAgentExecutor.deploy(address)._rootBridgeAgent (src/RootBridgeAgentExecutor.sol#14) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSystemRequest(address,bytes,uint16)._router (src/RootBridgeAgentExecutor.sol#50) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSystemRequest(address,bytes,uint16)._payload (src/RootBridgeAgentExecutor.sol#50) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSystemRequest(address,bytes,uint16)._srcChainId (src/RootBridgeAgentExecutor.sol#50) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeNoDeposit(address,bytes,uint16)._router (src/RootBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeNoDeposit(address,bytes,uint16)._payload (src/RootBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeNoDeposit(address,bytes,uint16)._srcChainId (src/RootBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeWithDeposit(address,bytes,uint16)._router (src/RootBridgeAgentExecutor.sol#82) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeWithDeposit(address,bytes,uint16)._payload (src/RootBridgeAgentExecutor.sol#82) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeWithDeposit(address,bytes,uint16)._srcChainId (src/RootBridgeAgentExecutor.sol#82) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeWithDepositMultiple(address,bytes,uint16)._router (src/RootBridgeAgentExecutor.sol#115) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeWithDepositMultiple(address,bytes,uint16)._payload (src/RootBridgeAgentExecutor.sol#115) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeWithDepositMultiple(address,bytes,uint16)._srcChainId (src/RootBridgeAgentExecutor.sol#115) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedNoDeposit(address,address,bytes,uint16)._account (src/RootBridgeAgentExecutor.sol#150) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedNoDeposit(address,address,bytes,uint16)._router (src/RootBridgeAgentExecutor.sol#150) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedNoDeposit(address,address,bytes,uint16)._payload (src/RootBridgeAgentExecutor.sol#150) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedNoDeposit(address,address,bytes,uint16)._srcChainId (src/RootBridgeAgentExecutor.sol#150) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedWithDeposit(address,address,bytes,uint16)._account (src/RootBridgeAgentExecutor.sol#167) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedWithDeposit(address,address,bytes,uint16)._router (src/RootBridgeAgentExecutor.sol#167) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedWithDeposit(address,address,bytes,uint16)._payload (src/RootBridgeAgentExecutor.sol#167) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedWithDeposit(address,address,bytes,uint16)._srcChainId (src/RootBridgeAgentExecutor.sol#167) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedWithDepositMultiple(address,address,bytes,uint16)._account (src/RootBridgeAgentExecutor.sol#202) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedWithDepositMultiple(address,address,bytes,uint16)._router (src/RootBridgeAgentExecutor.sol#203) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedWithDepositMultiple(address,address,bytes,uint16)._payload (src/RootBridgeAgentExecutor.sol#204) is not in mixedCase
Parameter RootBridgeAgentExecutor.executeSignedWithDepositMultiple(address,address,bytes,uint16)._srcChainId (src/RootBridgeAgentExecutor.sol#205) is not in mixedCase
Parameter VirtualAccount.withdrawNative(uint256)._amount (src/VirtualAccount.sol#51) is not in mixedCase
Parameter VirtualAccount.withdrawERC20(address,uint256)._token (src/VirtualAccount.sol#56) is not in mixedCase
Parameter VirtualAccount.withdrawERC20(address,uint256)._amount (src/VirtualAccount.sol#56) is not in mixedCase
Parameter VirtualAccount.withdrawERC721(address,uint256)._token (src/VirtualAccount.sol#61) is not in mixedCase
Parameter VirtualAccount.withdrawERC721(address,uint256)._tokenId (src/VirtualAccount.sol#61) is not in mixedCase
Parameter RootBridgeAgentFactory.createBridgeAgent(address)._newRootRouterAddress (src/factories/RootBridgeAgentFactory.sol#48) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
Variable RootBridgeAgent._updateStateOnBridgeOut(address,address,address,address,uint256,uint256,uint16)._dstChainId (src/RootBridgeAgent.sol#1138) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent._performCall(uint16,address,bytes,GasParams)._dstChainId (src/RootBridgeAgent.sol#809) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent.getFeeEstimate(uint256,uint256,bytes,uint16)._dstChainId (src/RootBridgeAgent.sol#144) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent.callOut(address,address,uint16,bytes,GasParams)._dstChainId (src/RootBridgeAgent.sol#163) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable IRootBridgeAgent.callOut(address,address,uint16,bytes,GasParams)._dstChainId (src/interfaces/IRootBridgeAgent.sol#171) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent._performRetrySettlementCall(bool,address[],address[],uint256[],uint256[],bytes,uint32,address,address,uint16,GasParams,uint256)._dstChainId (src/RootBridgeAgent.sol#866) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent.redeemSettlement(uint32)._dstChainId (src/RootBridgeAgent.sol#325) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool)._dstChainId (src/RootBridgeAgent.sol#1049) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable IRootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._dstChainId (src/interfaces/IRootBridgeAgent.sol#192) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable IRootBridgeAgent.getFeeEstimate(uint256,uint256,bytes,uint16)._dstChainId (src/interfaces/IRootBridgeAgent.sol#153) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._dstChainId (src/RootBridgeAgent.sol#205) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable IRootBridgeAgent.callOutAndBridgeMultiple(address,address,uint16,bytes,SettlementMultipleInput,GasParams,bool)._dstChainId (src/interfaces/IRootBridgeAgent.sol#216) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent._performFallbackCall(address,uint32,uint16)._dstChainId (src/RootBridgeAgent.sol#938) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent.callOutAndBridge(address,address,uint16,bytes,SettlementInput,GasParams,bool)._dstChainId (src/RootBridgeAgent.sol#178) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent._createSettlement(uint32,address,address,uint16,bytes,address,uint256,uint256,bool)._dstChainId (src/RootBridgeAgent.sol#970) is too similar to RootBridgeAgent._createSettlementMultiple(uint32,address,address,uint16,address[],uint256[],uint256[],bytes,bool).destChainId (src/RootBridgeAgent.sol#1076)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_0 (src/RootBridgeAgent.sol#477) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_1 (src/RootBridgeAgent.sol#500)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_0 (src/RootBridgeAgent.sol#477) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_5 (src/RootBridgeAgent.sol#595)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_0 (src/RootBridgeAgent.sol#477) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_2 (src/RootBridgeAgent.sol#523)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_1 (src/RootBridgeAgent.sol#500) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_2 (src/RootBridgeAgent.sol#523)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_2 (src/RootBridgeAgent.sol#523) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_3 (src/RootBridgeAgent.sol#557)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_2 (src/RootBridgeAgent.sol#523) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_5 (src/RootBridgeAgent.sol#595)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_0 (src/RootBridgeAgent.sol#477) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_3 (src/RootBridgeAgent.sol#557)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_1 (src/RootBridgeAgent.sol#500) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_3 (src/RootBridgeAgent.sol#557)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_3 (src/RootBridgeAgent.sol#557) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_5 (src/RootBridgeAgent.sol#595)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_1 (src/RootBridgeAgent.sol#500) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_5 (src/RootBridgeAgent.sol#595)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_0 (src/RootBridgeAgent.sol#477) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_7 (src/RootBridgeAgent.sol#635)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_1 (src/RootBridgeAgent.sol#500) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_7 (src/RootBridgeAgent.sol#635)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_2 (src/RootBridgeAgent.sol#523) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_7 (src/RootBridgeAgent.sol#635)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_3 (src/RootBridgeAgent.sol#557) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_7 (src/RootBridgeAgent.sol#635)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_5 (src/RootBridgeAgent.sol#595) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).srcChainId_scope_7 (src/RootBridgeAgent.sol#635)
Variable RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).userAccount_scope_4 (src/RootBridgeAgent.sol#587-589) is too similar to RootBridgeAgent.lzReceiveNonBlocking(address,uint16,bytes,bytes).userAccount_scope_6 (src/RootBridgeAgent.sol#627-629)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#variable-names-too-similar
INFO:Detectors:
BridgeAgentConstants.PARAMS_START (src/interfaces/BridgeAgentConstants.sol#27) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#29) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_TKN_START (src/interfaces/BridgeAgentConstants.sol#31) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_TKN_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#33) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_ENTRY_SIZE (src/interfaces/BridgeAgentConstants.sol#35) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_ADDRESS_SIZE (src/interfaces/BridgeAgentConstants.sol#37) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_TKN_SET_SIZE (src/interfaces/BridgeAgentConstants.sol#39) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_TKN_SET_SIZE_MULTIPLE (src/interfaces/BridgeAgentConstants.sol#41) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.ADDRESS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#43) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_AMT_OFFSET (src/interfaces/BridgeAgentConstants.sol#45) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_DEPOSIT_OFFSET (src/interfaces/BridgeAgentConstants.sol#47) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#49) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_END_SIGNED_OFFSET (src/interfaces/BridgeAgentConstants.sol#51) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.PARAMS_SETTLEMENT_OFFSET (src/interfaces/BridgeAgentConstants.sol#53) is never used in RootBridgeAgent (src/RootBridgeAgent.sol#32-1238)
BridgeAgentConstants.STATUS_READY (src/interfaces/BridgeAgentConstants.sol#13) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.STATUS_DONE (src/interfaces/BridgeAgentConstants.sol#15) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.STATUS_RETRIEVE (src/interfaces/BridgeAgentConstants.sol#17) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.STATUS_FAILED (src/interfaces/BridgeAgentConstants.sol#21) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.STATUS_SUCCESS (src/interfaces/BridgeAgentConstants.sol#23) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.PARAMS_TKN_START (src/interfaces/BridgeAgentConstants.sol#31) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.PARAMS_TKN_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#33) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.PARAMS_ENTRY_SIZE (src/interfaces/BridgeAgentConstants.sol#35) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.PARAMS_ADDRESS_SIZE (src/interfaces/BridgeAgentConstants.sol#37) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.ADDRESS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#43) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.PARAMS_AMT_OFFSET (src/interfaces/BridgeAgentConstants.sol#45) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.PARAMS_DEPOSIT_OFFSET (src/interfaces/BridgeAgentConstants.sol#47) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
BridgeAgentConstants.MAX_TOKENS_LENGTH (src/interfaces/BridgeAgentConstants.sol#57) is never used in RootBridgeAgentExecutor (src/RootBridgeAgentExecutor.sol#27-349)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unused-state-variable
INFO:Detectors:
BranchBridgeAgent._performFallbackCall(address,uint32) (src/BranchBridgeAgent.sol#785-795) sends eth to arbitrary user
	Dangerous calls:
	- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(rootChainId,rootBridgeAgentPath,abi.encodePacked(bytes1(0x09),_settlementNonce),_refundee,address(0),) (src/BranchBridgeAgent.sol#787-794)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#functions-that-send-ether-to-arbitrary-destinations
INFO:Detectors:
Reentrancy in BranchBridgeAgent.redeemDeposit(uint32) (src/BranchBridgeAgent.sol#434-457):
	External calls:
	- _clearToken(msg.sender,deposit.hTokens[i],deposit.tokens[i],deposit.amounts[i],deposit.deposits[i]) (src/BranchBridgeAgent.sol#448)
		- IBranchPort(localPortAddress).bridgeIn(_recipient,_hToken,_amount - _deposit) (src/BranchBridgeAgent.sol#908)
		- IBranchPort(localPortAddress).withdraw(_recipient,_token,_deposit) (src/BranchBridgeAgent.sol#913)
	State variables written after the call(s):
	- delete getDeposit[_depositNonce] (src/BranchBridgeAgent.sol#456)
	BranchBridgeAgent.getDeposit (src/BranchBridgeAgent.sol#87) can be used in cross function reentrancies:
	- BranchBridgeAgent._createDeposit(uint32,address,address,address,uint256,uint256) (src/BranchBridgeAgent.sol#812-847)
	- BranchBridgeAgent._createDepositMultiple(uint32,address,address[],address[],uint256[],uint256[]) (src/BranchBridgeAgent.sol#860-888)
	- BranchBridgeAgent.getDeposit (src/BranchBridgeAgent.sol#87)
	- BranchBridgeAgent.getDepositEntry(uint32) (src/BranchBridgeAgent.sol#156-158)
	- BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes) (src/BranchBridgeAgent.sol#587-701)
	- BranchBridgeAgent.redeemDeposit(uint32) (src/BranchBridgeAgent.sol#434-457)
	- BranchBridgeAgent.retrieveDeposit(uint32,GasParams) (src/BranchBridgeAgent.sol#422-431)
	- BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool) (src/BranchBridgeAgent.sol#343-419)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-1
INFO:Detectors:
ArbitrumBranchBridgeAgent._performCall(address,bytes,GasParams) (src/ArbitrumBranchBridgeAgent.sol#99-106) ignores return value by _rootBridgeAgentAddress.call{value: msg.value}() (src/ArbitrumBranchBridgeAgent.sol#103)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unchecked-low-level-calls
INFO:Detectors:
BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes).nonce (src/BranchBridgeAgent.sol#596) is a local variable never initialized
BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool).payload (src/BranchBridgeAgent.sol#357) is a local variable never initialized
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-local-variables
INFO:Detectors:
BranchBridgeAgent.lzReceive(uint16,bytes,uint64,bytes) (src/BranchBridgeAgent.sol#578-584) ignores return value by address(this).excessivelySafeCall(gasleft()(),150,abi.encodeWithSelector(this.lzReceiveNonBlocking.selector,msg.sender,_srcAddress,_payload)) (src/BranchBridgeAgent.sol#579-583)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unused-return
INFO:Detectors:
BranchBridgeAgent._clearToken(address,address,address,uint256,uint256) (src/BranchBridgeAgent.sol#903-915) has external calls inside a loop: IBranchPort(localPortAddress).bridgeIn(_recipient,_hToken,_amount - _deposit) (src/BranchBridgeAgent.sol#908)
BranchBridgeAgent._clearToken(address,address,address,uint256,uint256) (src/BranchBridgeAgent.sol#903-915) has external calls inside a loop: IBranchPort(localPortAddress).withdraw(_recipient,_token,_deposit) (src/BranchBridgeAgent.sol#913)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation/#calls-inside-a-loop
INFO:Detectors:
Reentrancy in BranchBridgeAgent._createDeposit(uint32,address,address,address,uint256,uint256) (src/BranchBridgeAgent.sol#812-847):
	External calls:
	- IBranchPort(localPortAddress).bridgeOut(msg.sender,_hToken,_token,_amount,_deposit) (src/BranchBridgeAgent.sol#824)
	State variables written after the call(s):
	- deposit.owner = _refundee (src/BranchBridgeAgent.sol#832)
	- deposit.hTokens = addressArray (src/BranchBridgeAgent.sol#835)
	- deposit.tokens = addressArray (src/BranchBridgeAgent.sol#838)
	- deposit.amounts = uintArray (src/BranchBridgeAgent.sol#841)
	- deposit.deposits = uintArray (src/BranchBridgeAgent.sol#844)
	- deposit.status = STATUS_SUCCESS (src/BranchBridgeAgent.sol#846)
Reentrancy in BranchBridgeAgent._createDepositMultiple(uint32,address,address[],address[],uint256[],uint256[]) (src/BranchBridgeAgent.sol#860-888):
	External calls:
	- IBranchPort(localPortAddress).bridgeOutMultiple(msg.sender,_hTokens,_tokens,_amounts,_deposits) (src/BranchBridgeAgent.sol#878)
	State variables written after the call(s):
	- deposit.owner = _refundee (src/BranchBridgeAgent.sol#882)
	- deposit.hTokens = _hTokens (src/BranchBridgeAgent.sol#883)
	- deposit.tokens = _tokens (src/BranchBridgeAgent.sol#884)
	- deposit.amounts = _amounts (src/BranchBridgeAgent.sol#885)
	- deposit.deposits = _deposits (src/BranchBridgeAgent.sol#886)
	- deposit.status = STATUS_SUCCESS (src/BranchBridgeAgent.sol#887)
Reentrancy in BranchBridgeAgent._execute(bool,uint32,address,bytes) (src/BranchBridgeAgent.sol#730-753):
	External calls:
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#737)
	State variables written after the call(s):
	- executionState[_settlementNonce] = STATUS_RETRIEVE (src/BranchBridgeAgent.sol#744)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-2
INFO:Detectors:
Reentrancy in BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes) (src/BranchBridgeAgent.sol#587-701):
	External calls:
	- _execute(nonce,abi.encodeWithSelector(BranchBridgeAgentExecutor.executeNoSettlement.selector,localRouterAddress,_payload)) (src/BranchBridgeAgent.sol#608-613)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#717)
	- _execute(_payload[0] == 0x81,nonce,recipient,abi.encodeWithSelector(BranchBridgeAgentExecutor.executeWithSettlement.selector,recipient,localRouterAddress,_payload)) (src/BranchBridgeAgent.sol#628-635)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(rootChainId,rootBridgeAgentPath,abi.encodePacked(bytes1(0x09),_settlementNonce),_refundee,address(0),) (src/BranchBridgeAgent.sol#787-794)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#737)
	- _execute(_payload[0] == 0x82,nonce,recipient_scope_0,abi.encodeWithSelector(BranchBridgeAgentExecutor.executeWithSettlementMultiple.selector,recipient_scope_0,localRouterAddress,_payload)) (src/BranchBridgeAgent.sol#650-660)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(rootChainId,rootBridgeAgentPath,abi.encodePacked(bytes1(0x09),_settlementNonce),_refundee,address(0),) (src/BranchBridgeAgent.sol#787-794)
		- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#737)
	- _performFallbackCall(recipient_scope_1,nonce) (src/BranchBridgeAgent.sol#677)
		- ILayerZeroEndpoint(lzEndpointAddress).send{value: address(this).balance}(rootChainId,rootBridgeAgentPath,abi.encodePacked(bytes1(0x09),_settlementNonce),_refundee,address(0),) (src/BranchBridgeAgent.sol#787-794)
	Event emitted after the call(s):
	- LogExecute(nonce) (src/BranchBridgeAgent.sol#700)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-3
INFO:Detectors:
BranchBridgeAgent._performCall(address,bytes,GasParams) (src/BranchBridgeAgent.sol#765-778) is never used and should be removed
BranchBridgeAgent._performFallbackCall(address,uint32) (src/BranchBridgeAgent.sol#785-795) is never used and should be removed
BranchBridgeAgent._requiresEndpoint(address,bytes) (src/BranchBridgeAgent.sol#936-944) is never used and should be removed
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#dead-code
INFO:Detectors:
Pragma version^0.8.0 (src/ArbitrumBranchBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/BranchBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/BranchBridgeAgentExecutor.sol#2) allows old versions
Pragma version^0.8.0 (src/factories/ArbitrumBranchBridgeAgentFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/factories/BranchBridgeAgentFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentConstants.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IArbitrumBranchPort.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgentFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchPort.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchRouter.sol#2) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroEndpoint.sol#3) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroUserApplicationConfig.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Low level call in ArbitrumBranchBridgeAgent._performCall(address,bytes,GasParams) (src/ArbitrumBranchBridgeAgent.sol#99-106):
	- _rootBridgeAgentAddress.call{value: msg.value}() (src/ArbitrumBranchBridgeAgent.sol#103)
Low level call in BranchBridgeAgent._execute(uint256,bytes) (src/BranchBridgeAgent.sol#712-721):
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#717)
Low level call in BranchBridgeAgent._execute(bool,uint32,address,bytes) (src/BranchBridgeAgent.sol#730-753):
	- (success) = bridgeAgentExecutorAddress.call{value: address(this).balance}(_calldata) (src/BranchBridgeAgent.sol#737)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#low-level-calls
INFO:Detectors:
Parameter DeployArbitrumBranchBridgeAgent.deploy(uint16,address,address,address)._localChainId (src/ArbitrumBranchBridgeAgent.sol#11) is not in mixedCase
Parameter DeployArbitrumBranchBridgeAgent.deploy(uint16,address,address,address)._daoAddress (src/ArbitrumBranchBridgeAgent.sol#11) is not in mixedCase
Parameter DeployArbitrumBranchBridgeAgent.deploy(uint16,address,address,address)._localRouterAddress (src/ArbitrumBranchBridgeAgent.sol#11) is not in mixedCase
Parameter DeployArbitrumBranchBridgeAgent.deploy(uint16,address,address,address)._localPortAddress (src/ArbitrumBranchBridgeAgent.sol#11) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._rootChainId (src/BranchBridgeAgent.sol#25) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._localChainId (src/BranchBridgeAgent.sol#26) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._rootBridgeAgentAddress (src/BranchBridgeAgent.sol#27) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._lzEndpointAddress (src/BranchBridgeAgent.sol#28) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._localRouterAddress (src/BranchBridgeAgent.sol#29) is not in mixedCase
Parameter DeployBranchBridgeAgent.deploy(uint16,uint16,address,address,address,address)._localPortAddress (src/BranchBridgeAgent.sol#30) is not in mixedCase
Parameter BranchBridgeAgent.getDepositEntry(uint32)._depositNonce (src/BranchBridgeAgent.sol#156) is not in mixedCase
Parameter BranchBridgeAgent.getFeeEstimate(uint256,uint256,bytes)._gasLimit (src/BranchBridgeAgent.sol#161) is not in mixedCase
Parameter BranchBridgeAgent.getFeeEstimate(uint256,uint256,bytes)._remoteBranchExecutionGas (src/BranchBridgeAgent.sol#161) is not in mixedCase
Parameter BranchBridgeAgent.getFeeEstimate(uint256,uint256,bytes)._payload (src/BranchBridgeAgent.sol#161) is not in mixedCase
Parameter BranchBridgeAgent.callOutSystem(address,bytes,GasParams)._refundee (src/BranchBridgeAgent.sol#180) is not in mixedCase
Parameter BranchBridgeAgent.callOutSystem(address,bytes,GasParams)._params (src/BranchBridgeAgent.sol#180) is not in mixedCase
Parameter BranchBridgeAgent.callOutSystem(address,bytes,GasParams)._gParams (src/BranchBridgeAgent.sol#180) is not in mixedCase
Parameter BranchBridgeAgent.callOut(address,bytes,GasParams)._refundee (src/BranchBridgeAgent.sol#195) is not in mixedCase
Parameter BranchBridgeAgent.callOut(address,bytes,GasParams)._params (src/BranchBridgeAgent.sol#195) is not in mixedCase
Parameter BranchBridgeAgent.callOut(address,bytes,GasParams)._gParams (src/BranchBridgeAgent.sol#195) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridge(address,bytes,DepositInput,GasParams)._refundee (src/BranchBridgeAgent.sol#210) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridge(address,bytes,DepositInput,GasParams)._params (src/BranchBridgeAgent.sol#211) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridge(address,bytes,DepositInput,GasParams)._dParams (src/BranchBridgeAgent.sol#212) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridge(address,bytes,DepositInput,GasParams)._gParams (src/BranchBridgeAgent.sol#213) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams)._refundee (src/BranchBridgeAgent.sol#232) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams)._params (src/BranchBridgeAgent.sol#233) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams)._dParams (src/BranchBridgeAgent.sol#234) is not in mixedCase
Parameter BranchBridgeAgent.callOutAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams)._gParams (src/BranchBridgeAgent.sol#235) is not in mixedCase
Parameter BranchBridgeAgent.callOutSigned(address,bytes,GasParams)._refundee (src/BranchBridgeAgent.sol#262) is not in mixedCase
Parameter BranchBridgeAgent.callOutSigned(address,bytes,GasParams)._params (src/BranchBridgeAgent.sol#262) is not in mixedCase
Parameter BranchBridgeAgent.callOutSigned(address,bytes,GasParams)._gParams (src/BranchBridgeAgent.sol#262) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._refundee (src/BranchBridgeAgent.sol#277) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._params (src/BranchBridgeAgent.sol#278) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._dParams (src/BranchBridgeAgent.sol#279) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._gParams (src/BranchBridgeAgent.sol#280) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridge(address,bytes,DepositInput,GasParams,bool)._hasFallbackToggled (src/BranchBridgeAgent.sol#281) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._refundee (src/BranchBridgeAgent.sol#307) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._params (src/BranchBridgeAgent.sol#308) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._dParams (src/BranchBridgeAgent.sol#309) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._gParams (src/BranchBridgeAgent.sol#310) is not in mixedCase
Parameter BranchBridgeAgent.callOutSignedAndBridgeMultiple(address,bytes,DepositMultipleInput,GasParams,bool)._hasFallbackToggled (src/BranchBridgeAgent.sol#311) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._isSigned (src/BranchBridgeAgent.sol#344) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._depositNonce (src/BranchBridgeAgent.sol#345) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._params (src/BranchBridgeAgent.sol#346) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._gParams (src/BranchBridgeAgent.sol#347) is not in mixedCase
Parameter BranchBridgeAgent.retryDeposit(bool,uint32,bytes,GasParams,bool)._hasFallbackToggled (src/BranchBridgeAgent.sol#348) is not in mixedCase
Parameter BranchBridgeAgent.retrieveDeposit(uint32,GasParams)._depositNonce (src/BranchBridgeAgent.sol#422) is not in mixedCase
Parameter BranchBridgeAgent.retrieveDeposit(uint32,GasParams)._gParams (src/BranchBridgeAgent.sol#422) is not in mixedCase
Parameter BranchBridgeAgent.redeemDeposit(uint32)._depositNonce (src/BranchBridgeAgent.sol#434) is not in mixedCase
Parameter BranchBridgeAgent.retrySettlement(uint32,bytes,GasParams[2],bool)._settlementNonce (src/BranchBridgeAgent.sol#465) is not in mixedCase
Parameter BranchBridgeAgent.retrySettlement(uint32,bytes,GasParams[2],bool)._params (src/BranchBridgeAgent.sol#466) is not in mixedCase
Parameter BranchBridgeAgent.retrySettlement(uint32,bytes,GasParams[2],bool)._gParams (src/BranchBridgeAgent.sol#467) is not in mixedCase
Parameter BranchBridgeAgent.retrySettlement(uint32,bytes,GasParams[2],bool)._hasFallbackToggled (src/BranchBridgeAgent.sol#468) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._recipient (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._hToken (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._token (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._amount (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearToken(address,address,address,uint256,uint256)._deposit (src/BranchBridgeAgent.sol#485) is not in mixedCase
Parameter BranchBridgeAgent.clearTokens(bytes,address)._sParams (src/BranchBridgeAgent.sol#494) is not in mixedCase
Parameter BranchBridgeAgent.clearTokens(bytes,address)._recipient (src/BranchBridgeAgent.sol#494) is not in mixedCase
Parameter BranchBridgeAgent.lzReceive(uint16,bytes,uint64,bytes)._srcAddress (src/BranchBridgeAgent.sol#578) is not in mixedCase
Parameter BranchBridgeAgent.lzReceive(uint16,bytes,uint64,bytes)._payload (src/BranchBridgeAgent.sol#578) is not in mixedCase
Parameter BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes)._endpoint (src/BranchBridgeAgent.sol#587) is not in mixedCase
Parameter BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes)._srcAddress (src/BranchBridgeAgent.sol#587) is not in mixedCase
Parameter BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes)._payload (src/BranchBridgeAgent.sol#587) is not in mixedCase
Variable BranchBridgeAgent._unlocked (src/BranchBridgeAgent.sol#101) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeNoSettlement(address,bytes)._router (src/BranchBridgeAgentExecutor.sol#53) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeNoSettlement(address,bytes)._payload (src/BranchBridgeAgentExecutor.sol#53) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlement(address,address,bytes)._recipient (src/BranchBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlement(address,address,bytes)._router (src/BranchBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlement(address,address,bytes)._payload (src/BranchBridgeAgentExecutor.sol#66) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlementMultiple(address,address,bytes)._recipient (src/BranchBridgeAgentExecutor.sol#104) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlementMultiple(address,address,bytes)._router (src/BranchBridgeAgentExecutor.sol#104) is not in mixedCase
Parameter BranchBridgeAgentExecutor.executeWithSettlementMultiple(address,address,bytes)._payload (src/BranchBridgeAgentExecutor.sol#104) is not in mixedCase
Parameter ArbitrumBranchBridgeAgentFactory.initialize(address)._coreRootBridgeAgent (src/factories/ArbitrumBranchBridgeAgentFactory.sol#56) is not in mixedCase
Parameter ArbitrumBranchBridgeAgentFactory.createBridgeAgent(address,address,address)._newBranchRouterAddress (src/factories/ArbitrumBranchBridgeAgentFactory.sol#80) is not in mixedCase
Parameter ArbitrumBranchBridgeAgentFactory.createBridgeAgent(address,address,address)._rootBridgeAgentAddress (src/factories/ArbitrumBranchBridgeAgentFactory.sol#81) is not in mixedCase
Parameter ArbitrumBranchBridgeAgentFactory.createBridgeAgent(address,address,address)._rootBridgeAgentFactoryAddress (src/factories/ArbitrumBranchBridgeAgentFactory.sol#82) is not in mixedCase
Parameter BranchBridgeAgentFactory.initialize(address)._coreRootBridgeAgent (src/factories/BranchBridgeAgentFactory.sol#87) is not in mixedCase
Parameter BranchBridgeAgentFactory.createBridgeAgent(address,address,address)._newBranchRouterAddress (src/factories/BranchBridgeAgentFactory.sol#116) is not in mixedCase
Parameter BranchBridgeAgentFactory.createBridgeAgent(address,address,address)._rootBridgeAgentAddress (src/factories/BranchBridgeAgentFactory.sol#117) is not in mixedCase
Parameter BranchBridgeAgentFactory.createBridgeAgent(address,address,address)._rootBridgeAgentFactoryAddress (src/factories/BranchBridgeAgentFactory.sol#118) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
Variable BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes).recipient_scope_0 (src/BranchBridgeAgent.sol#640) is too similar to BranchBridgeAgent.lzReceiveNonBlocking(address,bytes,bytes).recipient_scope_1 (src/BranchBridgeAgent.sol#665)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#variable-names-too-similar
INFO:Detectors:
BridgeAgentConstants.PARAMS_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#29) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_TKN_START (src/interfaces/BridgeAgentConstants.sol#31) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_TKN_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#33) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_ENTRY_SIZE (src/interfaces/BridgeAgentConstants.sol#35) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_ADDRESS_SIZE (src/interfaces/BridgeAgentConstants.sol#37) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_TKN_SET_SIZE (src/interfaces/BridgeAgentConstants.sol#39) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_TKN_SET_SIZE_MULTIPLE (src/interfaces/BridgeAgentConstants.sol#41) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.ADDRESS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#43) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_AMT_OFFSET (src/interfaces/BridgeAgentConstants.sol#45) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_DEPOSIT_OFFSET (src/interfaces/BridgeAgentConstants.sol#47) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#49) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_END_SIGNED_OFFSET (src/interfaces/BridgeAgentConstants.sol#51) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.PARAMS_SETTLEMENT_OFFSET (src/interfaces/BridgeAgentConstants.sol#53) is never used in ArbitrumBranchBridgeAgent (src/ArbitrumBranchBridgeAgent.sol#31-129)
BridgeAgentConstants.STATUS_READY (src/interfaces/BridgeAgentConstants.sol#13) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.STATUS_DONE (src/interfaces/BridgeAgentConstants.sol#15) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.STATUS_RETRIEVE (src/interfaces/BridgeAgentConstants.sol#17) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.STATUS_FAILED (src/interfaces/BridgeAgentConstants.sol#21) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.STATUS_SUCCESS (src/interfaces/BridgeAgentConstants.sol#23) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_START (src/interfaces/BridgeAgentConstants.sol#27) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_TKN_START_SIGNED (src/interfaces/BridgeAgentConstants.sol#33) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_ENTRY_SIZE (src/interfaces/BridgeAgentConstants.sol#35) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_ADDRESS_SIZE (src/interfaces/BridgeAgentConstants.sol#37) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_TKN_SET_SIZE (src/interfaces/BridgeAgentConstants.sol#39) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.ADDRESS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#43) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_AMT_OFFSET (src/interfaces/BridgeAgentConstants.sol#45) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_DEPOSIT_OFFSET (src/interfaces/BridgeAgentConstants.sol#47) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_END_OFFSET (src/interfaces/BridgeAgentConstants.sol#49) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.PARAMS_END_SIGNED_OFFSET (src/interfaces/BridgeAgentConstants.sol#51) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
BridgeAgentConstants.MAX_TOKENS_LENGTH (src/interfaces/BridgeAgentConstants.sol#57) is never used in BranchBridgeAgentExecutor (src/BranchBridgeAgentExecutor.sol#29-129)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unused-state-variable
INFO:Detectors:
ERC20hTokenRootFactory.initialize(address) (src/factories/ERC20hTokenRootFactory.sol#49-53) should emit an event for: 
	- coreRootRouterAddress = _coreRouter (src/factories/ERC20hTokenRootFactory.sol#51) 
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#missing-events-access-control
INFO:Detectors:
Pragma version^0.8.0 (src/factories/ERC20hTokenRootFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IERC20hTokenRoot.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IERC20hTokenRootFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/token/ERC20hTokenRoot.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Parameter ERC20hTokenRootFactory.initialize(address)._coreRouter (src/factories/ERC20hTokenRootFactory.sol#49) is not in mixedCase
Parameter ERC20hTokenRootFactory.createToken(string,string,uint8)._name (src/factories/ERC20hTokenRootFactory.sol#76) is not in mixedCase
Parameter ERC20hTokenRootFactory.createToken(string,string,uint8)._symbol (src/factories/ERC20hTokenRootFactory.sol#76) is not in mixedCase
Parameter ERC20hTokenRootFactory.createToken(string,string,uint8)._decimals (src/factories/ERC20hTokenRootFactory.sol#76) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
Different versions of Solidity are used:
	- Version used: ['>=0.5.0', '^0.8.0']
	- >=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3)
	- ^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2)
	- ^0.8.0 (src/interfaces/ICoreBranchRouter.sol#2)
	- ^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/ICoreBranchRouter.sol#2) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:SlitherSolcParsing:No contract were found in None, check the correct compilation
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IMulticall2.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Different versions of Solidity are used:
	- Version used: ['>=0.5.0', '^0.8.0']
	- >=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3)
	- ^0.8.0 (src/interfaces/IRootBridgeAgent.sol#2)
	- ^0.8.0 (src/interfaces/IRootRouter.sol#2)
	- ^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used
INFO:Detectors:
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootRouter.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IERC20hTokenRoot.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IERC20hTokenBranch.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IArbitrumBranchPort.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchPort.sol#3) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
VirtualAccount.payableCall(PayableCall[]).success (src/VirtualAccount.sol#99) is a local variable never initialized
VirtualAccount.call(Call[]).success (src/VirtualAccount.sol#71) is a local variable never initialized
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-local-variables
INFO:Detectors:
VirtualAccount.constructor(address,address)._userAddress (src/VirtualAccount.sol#35) lacks a zero-check on :
		- userAddress = _userAddress (src/VirtualAccount.sol#36)
VirtualAccount.constructor(address,address)._localPortAddress (src/VirtualAccount.sol#35) lacks a zero-check on :
		- localPortAddress = _localPortAddress (src/VirtualAccount.sol#37)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#missing-zero-address-validation
INFO:Detectors:
VirtualAccount.call(Call[]) (src/VirtualAccount.sol#66-82) has external calls inside a loop: (success,returnData[i]) = _call.target.call(_call.callData) (src/VirtualAccount.sol#74)
VirtualAccount.payableCall(PayableCall[]) (src/VirtualAccount.sol#85-112) has external calls inside a loop: (success,returnData[i]) = _call.target.call{value: val}(_call.callData) (src/VirtualAccount.sol#101)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation/#calls-inside-a-loop
INFO:Detectors:
VirtualAccount.isContract(address) (src/VirtualAccount.sol#147-153) uses assembly
	- INLINE ASM (src/VirtualAccount.sol#149-151)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#assembly-usage
INFO:Detectors:
Pragma version^0.8.0 (src/VirtualAccount.sol#3) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootPort.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IVirtualAccount.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Low level call in VirtualAccount.call(Call[]) (src/VirtualAccount.sol#66-82):
	- (success,returnData[i]) = _call.target.call(_call.callData) (src/VirtualAccount.sol#74)
Low level call in VirtualAccount.payableCall(PayableCall[]) (src/VirtualAccount.sol#85-112):
	- (success,returnData[i]) = _call.target.call{value: val}(_call.callData) (src/VirtualAccount.sol#101)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#low-level-calls
INFO:Detectors:
Parameter VirtualAccount.withdrawNative(uint256)._amount (src/VirtualAccount.sol#51) is not in mixedCase
Parameter VirtualAccount.withdrawERC20(address,uint256)._token (src/VirtualAccount.sol#56) is not in mixedCase
Parameter VirtualAccount.withdrawERC20(address,uint256)._amount (src/VirtualAccount.sol#56) is not in mixedCase
Parameter VirtualAccount.withdrawERC721(address,uint256)._token (src/VirtualAccount.sol#61) is not in mixedCase
Parameter VirtualAccount.withdrawERC721(address,uint256)._tokenId (src/VirtualAccount.sol#61) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IPortStrategy.sol#3) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IVirtualAccount.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version>=0.5.0 (src/interfaces/ILayerZeroEndpoint.sol#3) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroUserApplicationConfig.sol#3) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgentFactory.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IBranchPort.sol#3) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Different versions of Solidity are used:
	- Version used: ['>=0.5.0', '^0.8.0']
	- >=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3)
	- ^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2)
	- ^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IRootBridgeAgentFactory.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/BridgeAgentConstants.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Different versions of Solidity are used:
	- Version used: ['>=0.5.0', '^0.8.0']
	- >=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3)
	- ^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2)
	- ^0.8.0 (src/interfaces/IBranchRouter.sol#2)
	- ^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IBranchBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IBranchRouter.sol#2) allows old versions
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Different versions of Solidity are used:
	- Version used: ['>=0.5.0', '^0.8.0']
	- >=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3)
	- ^0.8.0 (src/interfaces/IRootBridgeAgent.sol#2)
	- ^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used
INFO:Detectors:
Pragma version>=0.5.0 (src/interfaces/ILayerZeroReceiver.sol#3) allows old versions
Pragma version^0.8.0 (src/interfaces/IRootBridgeAgent.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/BridgeAgentStructs.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IERC20hTokenRoot.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IERC20hTokenRootFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/token/ERC20hTokenRoot.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version>=0.5.0 (src/interfaces/ILayerZeroUserApplicationConfig.sol#3) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Pragma version^0.8.0 (src/interfaces/IERC20hTokenBranch.sol#2) allows old versions
Pragma version^0.8.0 (src/interfaces/IERC20hTokenBranchFactory.sol#2) allows old versions
Pragma version^0.8.0 (src/token/ERC20hTokenBranch.sol#2) allows old versions
solc-0.8.21 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Slither:./src/* analyzed (137 contracts with 85 detectors), 576 result(s) found
```


### Time spent:
16 hours