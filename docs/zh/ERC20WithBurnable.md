# 可销毁代币

Twitter: [Jack Lee](https://x.com/jackleeio)｜[Conflux DAO](https://x.com/ConfluxDAO)

社区: [JackLee.io](https://jacklee.io/) ｜[Conflux Forum](https://forum.conflux.fun/)

所有代码和教程都在 GitHub 上开源: https://github.com/jackleeio/CoinCraft

---

可销毁代币是一种允许代币持有者销毁（烧毁）自己的代币或经批准销毁他人代币的 ERC20 代币。这种机制可以用于减少代币供应量或实现某些特定的经济模型。

## 合约

[可销毁代币: ERC20WithBurnable.sol](../../src/ERC20/ERC20WithBurnable.sol)

## 测试

## 方法调用

## 部署

要使用 Foundry 部署 ERC20WithBurnable 代币，请按以下步骤操作：

1. 确保已安装 Foundry。如果没有，请参考 [Foundry 安装指南](https://book.getfoundry.sh/getting-started/installation)。

2. 在项目根目录创建一个 `.env` 文件，并添加以下内容：

   ```
   PRIVATE_KEY=你的私钥
   RPC_URL=目标网络的RPC_URL
   ```

3. 创建部署脚本 `script/DeployERC20WithBurnable.s.sol`：

   ```solidity:script/DeployERC20WithBurnable.s.sol
   // SPDX-License-Identifier: MIT
   pragma solidity ^0.8.24;

   import "forge-std/Script.sol";
   import "../src/ERC20/ERC20WithBurnable.sol";

   contract DeployERC20WithBurnable is Script {
       function run() external {
           uint256 deployerPrivateKey = vm.envUint("PRIVATE_KEY");
           vm.startBroadcast(deployerPrivateKey);

           ERC20WithBurnable token = new ERC20WithBurnable(
               "Burnable Token",
               "BURN",
               18,
               1000000 * 10**18 // 初始供应量为 1,000,000 代币
           );

           vm.stopBroadcast();
       }
   }
   ```

4. 运行以下命令进行部署：

   ```
   forge script script/DeployERC20WithBurnable.s.sol:DeployERC20WithBurnable --rpc-url $RPC_URL --broadcast --verify
   ```

5. 部署后，您将在控制台输出中看到已部署的合约地址。保存此地址以供将来使用。

注意：在部署之前，请确保您的账户有足够的原生代币（如 ETH、CFX）来支付燃气费。