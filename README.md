# DeepPurpose Windows Installation Guide

DeepPurpose 在 **Python 3.8 环境下最稳定**，官方文档目前没有及时更新版本说明。

本教程介绍如何在 **Windows + Anaconda** 环境下安装：

- DeepPurpose
- RDKit
- PyTorch

建议 **右键管理员模式打开 PowerShell**。

---

# 1 Create Environment

创建 Python 3.8 环境：

```bash
conda create -n deeppurpose python=3.8 -y
conda activate deeppurpose
```

---

# 2 Install RDKit

安装 RDKit：

```bash
conda install -c conda-forge rdkit -y
```

测试：

```bash
python -c "import rdkit; print('RDKit OK')"
```

如果输出：

```
RDKit OK
```

说明安装成功。

---

# 3 Install PyTorch

如果有 **NVIDIA GPU（推荐）**

安装 CUDA 11.8 版本：

```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

测试：

```bash
python -c "import torch; print(torch.__version__)"
```

如果 **没有 GPU**

安装 CPU 版本：

```bash
pip install torch torchvision torchaudio
```

---

# 4 Install Descriptastorus

```bash
pip install descriptastorus
```

---

# 5 Install DeepPurpose

```bash
pip install DeepPurpose
```

第一次安装会自动安装依赖：

- dgl
- lifelines
- scikit-learn

安装时间可能稍长。

---

# 6 Install Jupyter Notebook

安装 Notebook：

```bash
conda install notebook
```

安装 kernel 支持：

```bash
pip install ipykernel
```

注册环境：

```bash
python -m ipykernel install --user --name deeppurpose --display-name "Python (deeppurpose)"
```

启动 Notebook：

```bash
jupyter notebook
```

在 Notebook 中选择：

```
Kernel → Change Kernel → Python (deeppurpose)
```

---

# 7 Environment Test

在 Jupyter Notebook 中运行：

```python
import torch

print("Torch version:", torch.__version__)
print("CUDA available:", torch.cuda.is_available())

if torch.cuda.is_available():
    print("GPU:", torch.cuda.get_device_name(0))
```

示例输出：

```
Torch version: 2.x.x
CUDA available: True
GPU: NVIDIA GeForce RTX 3060
```

---

# 8 RDKit Test

```python
from rdkit import Chem

mol = Chem.MolFromSmiles("CCO")

print("RDKit OK:", mol is not None)
```

输出：

```
RDKit OK: True
```

---

# 9 DeepPurpose Test

```python
from DeepPurpose import utils
from DeepPurpose import DTI as models

drug_encoding = "CNN"
target_encoding = "CNN"

config = utils.generate_config(drug_encoding, target_encoding)

model = models.model_initialize(**config)

print("DeepPurpose OK")
```

如果输出：

```
DeepPurpose OK
```

说明安装成功。

---




⭐ 如果这个教程对你有帮助，欢迎 Star 本仓库
