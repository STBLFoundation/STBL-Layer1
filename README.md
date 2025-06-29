<p align="center">
  <img src=".github/stbl.jpg" alt="STBL Banner" width="600"/>
</p>

<h1 align="center">STBL Foundation | 稳定币基金会</h1>

<p align="center">
  <a href="https://github.com/STBLFoundation/STBL-Layer1/releases">
    <img src="https://img.shields.io/github/v/release/STBLFoundation/STBL-Layer1?style=flat-square" alt="Release">
  </a>
  <a href="https://github.com/STBLFoundation/STBL-Layer1/issues">
    <img src="https://img.shields.io/github/issues/STBLFoundation/STBL-Layer1?style=flat-square" alt="Issues">
  </a>
</p>

---

## 🚀 快速启动 STBL Layer1 区块链验证者节点

### 🛠️ 步骤一：克隆仓库

```bash
git clone https://github.com/STBLFoundation/STBL-Layer1.git
cd STBL-Layer1
```

### 🧩 步骤二：安装依赖

```bash
go mod tidy
```

### ⚙️ 步骤三：编译项目

```bash
make build
```

> 编译完成后，将在当前目录生成 `stbl` 可执行文件，您已准备好启动区块链节点！

---

### 🗝️ 步骤四：初始化数据目录

```bash
./stbl secrets init --data-dir test-chain --insecure
```

<details>
<summary>点击展开示例输出</summary>

```
[WARNING: INSECURE LOCAL SECRETS - SHOULD NOT BE RUN IN PRODUCTION]

[SECRETS INIT]
Public key (address) = 0xe851DbCF86aC139B5B2c5D868f7D053F480D3f6a
BLS Public key       = 0x826d2b355ce32caaa388e3d05bb937487123714897fa5783686f8036bc3ac046f53b4ded29810b3fa234202a36e25eea
Node ID              = 16Uiu2HAm2iJmhgypvRfX2cNJNggv8zaEBLT819Ez7bzFzmkHAA5B
```
</details>

---

### 📝 步骤五：生成 Genesis 文件

> ⚠️ **注意：**  
> `--validators` 参数后面的 `0xe851DbCF86aC139B5B2c5D868f7D053F480D3f6a:0x826d2b355ce32caaa388e3d05bb937487123714897fa5783686f8036bc3ac046f53b4ded29810b3fa234202a36e25eea`  
> 需要填写**您自己电脑生成的 address 和 BLS Public Key**，请根据上一步输出替换为您的实际值！

```bash
./stbl genesis \
  --consensus ibft \
  --pos \
  --chain-id 100234 \
  --validators <你的address>:<你的BLS Public Key> \
  --premine 0x01E0075B970e10614fA3D2cdb8Eb10d368296673:10000000000000000000000000000 \
  --block-gas-limit 10000000 \
  --block-time 1s \
  --bootnode /ip4/38.244.14.92/tcp/10001/p2p/16Uiu2HAm2iJmhgypvRfX2cNJNggv8zaEBLT819Ez7bzFzmkHAA5B \
  --dir test-chain/genesis.json
```

---

### 🚦 步骤六：启动区块链节点

```bash
nohup ./stbl server \
  --data-dir ./test-chain \
  --chain ./test-chain/genesis.json \
  --grpc-address 0.0.0.0:10000 \
  --libp2p 0.0.0.0:1478 \
  --jsonrpc 0.0.0.0:10002 \
  --nat <your ip address> \
  --seal > /dev/null 2>&1 &
```

---

### 💎 步骤七：质押代币，成为验证者

> ⚠️ **质押前请先创建 `.env` 文件，并确保已设置所需参数。**

#### `.env` 文件格式示例

```env
JSONRPC_URL=
PRIVATE_KEYS=
STAKING_CONTRACT_ADDRESS=0x0000000000000000000000000000000000001001
MAX_VALIDATOR_COUNT=500
MIN_VALIDATOR_COUNT=1
BLS_PUBLIC_KEY=
```

- `JSONRPC_URL`：填写RPC 地址  
- `PRIVATE_KEYS`：填写 `test-chain/consensus` 目录下的验证者私钥  
- 其余参数请根据实际情况填写

#### 1. 拉取质押合约

```bash
git clone https://github.com/STBLFoundation/staking-contracts.git
cd staking-contracts
```

#### 2. 质押 STBL 代币

```bash
npm run stake
```

#### 3. 查看网络所有验证者信息

```bash
npm run info
```

---

## 📚 社区链接

- [Telegram](https://t.me/STBL_F)
- [X](https://x.com/STBL_F)暂无
- [Youtube](https://stbl.foundation)暂无

---

<p align="center">
  <b>欢迎加入 STBL 社区，共建第一个去中心化的人民币支付网络！</b>
</p>