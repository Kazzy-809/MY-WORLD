🚀 基于硬件能耗特征的物联网通信效能回归分析
IoT Communication Efficiency Regression based on Hardware Energy Characteristics
🌟 项目亮点 (Highlights)

硬核特征工程：不同于常规统计，本项目深入微电子底层通信机制，构造了单位字节传输功耗、实际吞吐率等物理驱动特征 。
+1


处理极端工况：针对物联网数据分布不均问题，在交叉验证框架下引入 SMOTE 过采样策略 。
+1


高精度模型融合：构建以 Random Forest 为元模型的 Stacking 融合策略，将预测均方根误差（RMSE）优化至 0.3769 。


模型可解释性：利用 SHAP 框架剖析射频收发器能耗对通信效能的影响，实现“黑盒模型”透明化 。

📊 数据集说明 (Dataset)
来源：IoT Sensor–Cloud Data Transmission Dataset。


规模：10,000 条原始日志，涵盖 ECG、血氧仪等五类异构传感器 。
+1


处理：完成异常值修正、缺失填充及设备编码标准化 。
+1

🛠️ 技术栈 (Tech Stack)

核心框架：Scikit-learn, Pandas, Matplotlib 。
+1


主流算法：CatBoost, XGBoost, Random Forest 。


解释工具：SHAP (Lundberg & Lee) 。
