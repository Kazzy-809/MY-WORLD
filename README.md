# 📡 IoT-End-Cloud-Efficiency-Predictor
**基于硬件能耗特征的物联网端云协同传输效能预测模型**

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Stacking%20Ensemble-orange)
![Framework](https://img.shields.io/badge/Framework-XGBoost%20%7C%20LightGBM%20%7C%20CatBoost-green)
![RMSE](https://img.shields.io/badge/RMSE-0.3769-brightgreen)

## 📖 项目背景 (Project Background)
在医疗物联网（WBSN）与边缘计算协同场景中，端侧物理硬件的**功耗墙**与**内存墙**是制约大规模 AI 和数据传输的核心瓶颈。本项目摒弃了传统纯数据驱动的“暴力特征堆砌”，深入微电子端侧通信的底层物理机制，通过分析 10,000 条异构传感器（ECG、血氧仪等）底层日志，构建了**具有物理学意义的效能回归预测模型**，为端侧算力分配与芯片前端能耗优化提供数据支撑。

[Image of edge computing IoT architecture with sensor nodes and cloud]

## ✨ 核心创新点 (Key Features)

### 1. ⚡ 硬件驱动的特征工程 (Hardware-aware Feature Engineering)
* 深入底层通信物理机制，构造了 15+ 具有实际物理意义的衍生特征。
* 核心特征包括：**单位字节传输功耗 (`energy_per_byte`)**、**任务平均功率 (`avg_power`)**、**能量收益比 (`yield_per_energy`)** 及实际吞吐率等，精准刻画端侧芯片动态能耗。

### 2. 🛡️ 极端工况下的鲁棒性处理 (Robustness to Extreme Conditions)
* 针对真实物联网日志中的长尾偏态分布，引入**对数变换（Log Transform）**进行特征平滑。
* 在派生特征计算中严格引入**极小量 (`eps=1e-9`) 惩罚项**，彻底解决由于传感器采集异常导致的除零异常，大幅提升模型在复杂工况下的抗干扰性。

### 3. 🧠 双轨制 Stacking 融合架构 (Dual-track Stacking Ensemble)
* 采用 **5 折交叉验证 (5-Fold CV)** 联合训练 GBDT 三剑客（XGBoost, LightGBM, CatBoost），严格生成 OOF (Out-of-Fold) 预测集，杜绝数据泄露。
* **Level 1**：构建基于**误差倒数加权 (Inverse RMSE Weighting)** 的线性融合 Baseline，锁死精度下限。
* **Level 2**：重构次级特征空间，动态择优选用 **Random Forest** 作为元模型 (Meta-model)，成功捕捉基模型间的非线性互补关系。

[Image of stacking ensemble machine learning architecture]

### 4. 🔍 基于 SHAP 的微电子效能归因 (SHAP Interpretability)
* 引入博弈论 SHAP 框架打开模型黑盒，实现从全局到个体的特征重要性量化。
* **关键发现**：端侧射频收发器能耗、基带处理包大小与传输持续时间是主导通信效能的最关键驱动因素，从数据层面印证了“芯片前端能量瓶颈决定整体传输效率”的硬件直觉。

[Image of SHAP summary plot feature importance]

## 📊 最终性能表现 (Performance)
* **评估指标**: 均方根误差 (RMSE)
* **最终得分**: **`0.3769`** (相较于单一基模型表现出显著的精度跃升与泛化稳定性)

## 📁 核心目录结构 (Repository Structure)
```text
├── data/                  # 原始数据集与清洗后的数据 (10,000条传感器日志)
├── baseline.ipynb         # 核心 Jupyter Notebook (包含数据清洗、特征工程、EDA与模型训练全流程)
├── requirements.txt       # 项目依赖包
└── README.md              # 项目说明文档
