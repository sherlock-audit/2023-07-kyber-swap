
# KyberSwap contest details

- Join [Sherlock Discord](https://discord.gg/MABEWyASkp)
- Submit findings using the issue page in your private contest repo (label issues as med or high)
- [Read for more details](https://docs.sherlock.xyz/audits/watsons)

# Q&A

### Q: On what chains are the smart contracts going to be deployed?
Mainnet, BNB Chain, Polygon, Arbitrum, Optimism, Avalanche, Fantom, Linea, Polygon zkEVM, Base, BitTorrent, Cronos, Velas, Oasis (and could be any EVM compatible chains)
___

### Q: Which ERC20 tokens do you expect will interact with the smart contracts? 
Standard ERC20
___

### Q: Which ERC721 tokens do you expect will interact with the smart contracts? 
It mints ERC721 token as positions, similar to Uni-v3
___

### Q: Which ERC777 tokens do you expect will interact with the smart contracts? 
none
___

### Q: Are there any FEE-ON-TRANSFER tokens interacting with the smart contracts?

no
___

### Q: Are there any REBASING tokens interacting with the smart contracts?

no
___

### Q: Are the admins of the protocols your contracts integrate with (if any) TRUSTED or RESTRICTED?
RESTRICTED
___

### Q: Is the admin/owner of the protocol/contracts TRUSTED or RESTRICTED?
Restricted - Owner shouldn’t be able to steal funds, but is trusted with setting fee recipient address and fee collection (up to 20%)
___

### Q: Are there any additional protocol roles? If yes, please explain in detail:
Factory configMaster
- Config protocol fee recipient and fee percentage.
- Enable new swap fee tiers
- Update whitelisted Position Manager
- Enable/Disable whitelist requirement for Position Manager
- Update configMaster.
- update vesting period
- configMaster should not be able to steal funds but is trusted with the actions above.

Pool Oracle’s owner:
- Upgrade Oracle implementation
- Rescue funds wrongly sent to the Pool Oracle

___

### Q: Is the code/contract expected to comply with any EIPs? Are there specific assumptions around adhering to those EIPs that Watsons should be aware of?
No
___

### Q: Please list any known issues/acceptable risks that should not result in a valid finding.
- The condition getTickAtSqrtRatio(currentSqrtP) == currentTick may not hold. In some edge cases, getTickAtSqrtRatio(currentSqrtP) == currentTick+1 due to the tick is crossed but the price is closed to currentSqrtP (and must be rounded up for the solvency of the AMM).

___

### Q: Please provide links to previous audits (if any).
https://chainsecurity.com/wp-content/uploads/2021/12/ChainSecurity_Kyber_Network_KyberSwap_Elastic_V2_audit.pdf
___

### Q: Are there any off-chain mechanisms or off-chain procedures for the protocol (keeper bots, input validation expectations, etc)?
no
___

### Q: In case of external protocol integrations, are the risks of external contracts pausing or executing an emergency withdrawal acceptable? If not, Watsons will submit issues related to these situations that can harm your protocol's functionality.
yes
___

### Q: Do you expect to use any of the following tokens with non-standard behaviour with the smart contracts?
no
___

### Q: Add links to relevant protocol resources
https://docs.google.com/document/d/1F50RWQRRyaNxnW5RvKgw09fN2FofIVLVccijgcOt-Iw/edit?usp=sharing
https://hackmd.io/7zTuB6WHSoOzS446WODWzQ?view
https://hackmd.io/sgADNlGNS8eSGU_8mZYqDQ?view

___



# Audit scope


[ks-elastic-sc @ 4ab08c0a60f74809f731bdd333076e32d05f1d17](https://github.com/KyberNetwork/ks-elastic-sc/tree/4ab08c0a60f74809f731bdd333076e32d05f1d17)
- [ks-elastic-sc/contracts/Factory.sol](ks-elastic-sc/contracts/Factory.sol)
- [ks-elastic-sc/contracts/Pool.sol](ks-elastic-sc/contracts/Pool.sol)
- [ks-elastic-sc/contracts/PoolStorage.sol](ks-elastic-sc/contracts/PoolStorage.sol)
- [ks-elastic-sc/contracts/PoolTicksState.sol](ks-elastic-sc/contracts/PoolTicksState.sol)
- [ks-elastic-sc/contracts/interfaces/IFactory.sol](ks-elastic-sc/contracts/interfaces/IFactory.sol)
- [ks-elastic-sc/contracts/interfaces/IPool.sol](ks-elastic-sc/contracts/interfaces/IPool.sol)
- [ks-elastic-sc/contracts/interfaces/callback/IFlashCallback.sol](ks-elastic-sc/contracts/interfaces/callback/IFlashCallback.sol)
- [ks-elastic-sc/contracts/interfaces/callback/IFlashCallback.sol](ks-elastic-sc/contracts/interfaces/callback/IFlashCallback.sol)
- [ks-elastic-sc/contracts/interfaces/callback/IMintCallback.sol](ks-elastic-sc/contracts/interfaces/callback/IMintCallback.sol)
- [ks-elastic-sc/contracts/interfaces/callback/ISwapCallback.sol](ks-elastic-sc/contracts/interfaces/callback/ISwapCallback.sol)
- [ks-elastic-sc/contracts/interfaces/oracle/IPoolOracle.sol](ks-elastic-sc/contracts/interfaces/oracle/IPoolOracle.sol)
- [ks-elastic-sc/contracts/interfaces/periphery/IBasePositionManager.sol](ks-elastic-sc/contracts/interfaces/periphery/IBasePositionManager.sol)
- [ks-elastic-sc/contracts/interfaces/periphery/IERC721Permit.sol](ks-elastic-sc/contracts/interfaces/periphery/IERC721Permit.sol)
- [ks-elastic-sc/contracts/interfaces/periphery/IMulticall.sol](ks-elastic-sc/contracts/interfaces/periphery/IMulticall.sol)
- [ks-elastic-sc/contracts/interfaces/periphery/INonfungibleTokenPositionDescriptor.sol](ks-elastic-sc/contracts/interfaces/periphery/INonfungibleTokenPositionDescriptor.sol)
- [ks-elastic-sc/contracts/interfaces/periphery/IRouter.sol](ks-elastic-sc/contracts/interfaces/periphery/IRouter.sol)
- [ks-elastic-sc/contracts/interfaces/periphery/IRouterTokenHelper.sol](ks-elastic-sc/contracts/interfaces/periphery/IRouterTokenHelper.sol)
- [ks-elastic-sc/contracts/interfaces/periphery/IRouterTokenHelperWithFee.sol](ks-elastic-sc/contracts/interfaces/periphery/IRouterTokenHelperWithFee.sol)
- [ks-elastic-sc/contracts/interfaces/periphery/base_position_manager/IBasePositionManagerEvents.sol](ks-elastic-sc/contracts/interfaces/periphery/base_position_manager/IBasePositionManagerEvents.sol)
- [ks-elastic-sc/contracts/interfaces/pool/IPoolActions.sol](ks-elastic-sc/contracts/interfaces/pool/IPoolActions.sol)
- [ks-elastic-sc/contracts/interfaces/pool/IPoolEvents.sol](ks-elastic-sc/contracts/interfaces/pool/IPoolEvents.sol)
- [ks-elastic-sc/contracts/interfaces/pool/IPoolStorage.sol](ks-elastic-sc/contracts/interfaces/pool/IPoolStorage.sol)
- [ks-elastic-sc/contracts/libraries/BaseSplitCodeFactory.sol](ks-elastic-sc/contracts/libraries/BaseSplitCodeFactory.sol)
- [ks-elastic-sc/contracts/libraries/CodeDeployer.sol](ks-elastic-sc/contracts/libraries/CodeDeployer.sol)
- [ks-elastic-sc/contracts/libraries/Linkedlist.sol](ks-elastic-sc/contracts/libraries/Linkedlist.sol)
- [ks-elastic-sc/contracts/libraries/LiqDeltaMath.sol](ks-elastic-sc/contracts/libraries/LiqDeltaMath.sol)
- [ks-elastic-sc/contracts/libraries/MathConstants.sol](ks-elastic-sc/contracts/libraries/MathConstants.sol)
- [ks-elastic-sc/contracts/libraries/Oracle.sol](ks-elastic-sc/contracts/libraries/Oracle.sol)
- [ks-elastic-sc/contracts/libraries/QtyDeltaMath.sol](ks-elastic-sc/contracts/libraries/QtyDeltaMath.sol)
- [ks-elastic-sc/contracts/libraries/QuadMath.sol](ks-elastic-sc/contracts/libraries/QuadMath.sol)
- [ks-elastic-sc/contracts/libraries/ReinvestmentMath.sol](ks-elastic-sc/contracts/libraries/ReinvestmentMath.sol)
- [ks-elastic-sc/contracts/libraries/SafeCast.sol](ks-elastic-sc/contracts/libraries/SafeCast.sol)
- [ks-elastic-sc/contracts/libraries/SwapMath.sol](ks-elastic-sc/contracts/libraries/SwapMath.sol)
- [ks-elastic-sc/contracts/oracle/PoolOracle.sol](ks-elastic-sc/contracts/oracle/PoolOracle.sol)
- [ks-elastic-sc/contracts/periphery/AntiSnipAttackPositionManager.sol](ks-elastic-sc/contracts/periphery/AntiSnipAttackPositionManager.sol)
- [ks-elastic-sc/contracts/periphery/BasePositionManager.sol](ks-elastic-sc/contracts/periphery/BasePositionManager.sol)
- [ks-elastic-sc/contracts/periphery/Router.sol](ks-elastic-sc/contracts/periphery/Router.sol)
- [ks-elastic-sc/contracts/periphery/base/DeadlineValidation.sol](ks-elastic-sc/contracts/periphery/base/DeadlineValidation.sol)
- [ks-elastic-sc/contracts/periphery/base/ERC721Permit.sol](ks-elastic-sc/contracts/periphery/base/ERC721Permit.sol)
- [ks-elastic-sc/contracts/periphery/base/ImmutablePeripheryStorage.sol](ks-elastic-sc/contracts/periphery/base/ImmutablePeripheryStorage.sol)
- [ks-elastic-sc/contracts/periphery/base/LiquidityHelper.sol](ks-elastic-sc/contracts/periphery/base/LiquidityHelper.sol)
- [ks-elastic-sc/contracts/periphery/base/Multicall.sol](ks-elastic-sc/contracts/periphery/base/Multicall.sol)
- [ks-elastic-sc/contracts/periphery/base/RouterTokenHelper.sol](ks-elastic-sc/contracts/periphery/base/RouterTokenHelper.sol)
- [ks-elastic-sc/contracts/periphery/base/RouterTokenHelperWithFee.sol](ks-elastic-sc/contracts/periphery/base/RouterTokenHelperWithFee.sol)
- [ks-elastic-sc/contracts/periphery/libraries/AntiSnipAttack.sol](ks-elastic-sc/contracts/periphery/libraries/AntiSnipAttack.sol)
- [ks-elastic-sc/contracts/periphery/libraries/LiquidityMath.sol](ks-elastic-sc/contracts/periphery/libraries/LiquidityMath.sol)
- [ks-elastic-sc/contracts/periphery/libraries/PathHelper.sol](ks-elastic-sc/contracts/periphery/libraries/PathHelper.sol)
- [ks-elastic-sc/contracts/periphery/libraries/PoolAddress.sol](ks-elastic-sc/contracts/periphery/libraries/PoolAddress.sol)
- [ks-elastic-sc/contracts/periphery/libraries/TokenHelper.sol](ks-elastic-sc/contracts/periphery/libraries/TokenHelper.sol)
- [ks-elastic-sc/contracts/periphery/TokenPositionDescriptor.sol](ks-elastic-sc/contracts/periphery/TokenPositionDescriptor.sol)


