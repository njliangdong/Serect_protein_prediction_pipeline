# 分泌蛋白预测流程（TMHMM + SignalP）

本项目提供一个简单的蛋白质分泌预测流程，结合跨膜结构预测工具 TMHMM 和信号肽预测工具 SignalP，用于筛选候选分泌蛋白。

---

## 📦 环境要求

* macOS 或 Linux 系统
* Perl（用于 TMHMM）
* Bash 环境

---

# 🔬 TMHMM v2.0

## 安装

```bash
tar zxvf tmhmm-2.0d.macOS.tar.gz
cd tmhmm-2.0d
```

---

## 配置

需要修改以下两个脚本的第一行（Perl 路径）：

```bash
./bin/tmhmm
./bin/tmhmmformat.pl
```

例如：

```bash
#!/usr/bin/perl
```

---

## 使用方法

```bash
cat pep.fa | ../bin/tmhmm > pep.tmhmm.out.txt
```

---

# 🧬 SignalP v5.0

## 安装

```bash
tar zxvf signalp-5.0b.Linux.tar.gz
cd signalp-5.0b

mkdir -p ~/local/bin
mkdir -p ~/local/lib

cp ./bin/signalp ~/local/bin/
cp -r ./lib ~/local/
```

---

## 环境变量配置

```bash
echo 'export PATH=$HOME/local/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

测试安装是否成功：

```bash
signalp -h
```

---

## 使用方法

```bash
signalp \
    -fasta pep.fa \
    -org euk \
    -format short \
    -gff3 \
    -mature \
    -prefix pep.signalp.out.txt
```

---

# 📁 输入文件

* `pep.fa`：蛋白序列 FASTA 文件

---

# 📤 输出结果

### TMHMM

* `pep.tmhmm.out.txt`：跨膜结构预测结果

### SignalP

* `pep.signalp.out.txt*`：信号肽预测结果（包含多种格式输出）

---

# 🧠 使用说明

* TMHMM 依赖 Perl，请确保路径正确
* SignalP 建议在 Linux 环境运行（服务器或 WSL）
* 大规模数据建议并行处理

---

# 🚀 分泌蛋白筛选思路

典型筛选逻辑如下：

1. 使用 SignalP 预测信号肽（筛选分泌相关蛋白）
2. 使用 TMHMM 预测跨膜结构
3. 去除含跨膜结构蛋白（通常为膜蛋白）
4. 保留候选分泌蛋白：

👉 **SignalP 阳性 + TMHMM 阴性**

---

# 📌 示例流程

```bash
# Step 1: 信号肽预测
signalp -fasta pep.fa -org euk -format short -prefix signalp_out

# Step 2: 跨膜结构预测
cat pep.fa | tmhmm > tmhmm_out.txt
```

---

# 📬 联系方式

如有问题或改进建议，欢迎提交 Issue 或 Pull Request。
