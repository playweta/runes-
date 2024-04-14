# runes-runes全节点搭建教程以及可能后续的mint脚本

## 1.硬件准备
* 至少1tb硬盘
* 内存越高越好
* mac、windows、ubunt、wsl都行

## 2.安装比特币全节点bitcoin core (安装过的直接跳到第3步)
下载bitcoincore 
地址：https://bitcoincore.org/en/releases/
最新版本26.1，选择适合你的系统的版本

我用的是ubunt安装比特币全节点
直接命令行(snap的安装方式)：
```shell
sudo apt update;
sudo apt install snapd;
snap install bitcoin-core;
mkdir /mnt/HC_Volume/bitcoin_chain
```

开始同步    /mnt/HC_Volume/bitcoin_chain是全节点的数据存储位置  
```
bitcoin-core.daemon -txindex=1 -datadir="/mnt/HC_Volume/bitcoin_chain" -rest;
```

## 3.下载 runes，最新版本18.0
地址：https://github.com/ordinals/ord/releases/tag/0.18.0

![image](https://github.com/playweta/runes-/assets/47896870/42ac89e4-8f2e-47e1-ad33-55d8a58f8db0)

下载解压，放到路径 /root/ord，此路径最好和比特币全节点一致。
或者用git:
```git
git clone https://github.com/ordinals/ord.git
```
3.2 在ord文件下编译代码
选择版本
```
git checkout 0.18.1
```
没有安装rust的,安装rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
编译ord
```
cargo build --release
```
## 4.运行ord
如果只玩runes，正常索引会很慢，可以不索引铭文。
在ord文件夹内添加配置文件
新建一个 config 文件，然后添加 
```
# 是否不索引引铭文
no_index_inscriptions: true 
# 是否索引符文
index_runes: true
# 全节点账号（默认是没有的，没有设置不用管）
bitcoin-rpc-username 账号
# 全节点密码（默认是没有的，没有设置不用管）
bitcoin-rpc-password 密码
# 全节点数据
bitcoin-data-dir /mnt/HC_Volume/bitcoin_chain/
# 内存，单位是字节 ，默认是1/4， 内存大的自己算一下设置多少合适
index_cache_size: 6800000000
```

然后执行节点同步，
```
./ord--config config index update
```

列出所有的runes代币
```
./ord runes
```

运行server
```
./ord --config config server
```
浏览器打开
http://0.0.0.0/runes

# 5.有什么问题可以在这里问
![image](https://github.com/playweta/runes-/assets/47896870/d616387f-a5a2-4b85-a994-0aed406289db)

