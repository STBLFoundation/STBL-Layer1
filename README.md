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

```bash
./stbl genesis \
  --consensus ibft \
  --pos \
  --chain-id 100234 \
  --validators 0xe851DbCF86aC139B5B2c5D868f7D053F480D3f6a:0x826d2b355ce32caaa388e3d05bb937487123714897fa5783686f8036bc3ac046f53b4ded29810b3fa234202a36e25eea \
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
  --nat 38.244.14.92 \
  --seal > /dev/null 2>&1 &
```

---

### 💎 步骤七：质押代币，成为验证者

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

## 📚 参考与支持

- [项目 Wiki](https://github.com/STBLFoundation/STBL-Layer1/wiki)
- [提交 Issue](https://github.com/STBLFoundation/STBL-Layer1/issues)
- [官方网站](https://stbl.foundation)

---

<p align="center">
  <b>欢迎加入 STBL 社区，共建去中心化金融新生态！</b>
</p>