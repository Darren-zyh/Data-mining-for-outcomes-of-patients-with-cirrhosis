# Data-mining-for-outcomes-of-patients-with-cirrhosis
### 1. 引言

项目目标是使用从深度学习模型生成的合成数据集来预测肝硬化患者的状态。深度学习模型基于1984年梅奥诊所的临床试验数据。报告包括数据探索、缺失数据处理、不平衡类处理、模型尝试及结果、结论和建议。

### 2. 数据探索

数据集包含13175名患者，其中7905名用于训练，5270名用于测试。每个患者的数据包括多项体征和状态。对数值特征进行分箱处理，观察特征与状态之间的关系。观察到的趋势包括：

- 高胆红素、胆固醇、铜、SGOT、凝血酶原时间与死亡率增加有关
- 高白蛋白、血小板与存活率增加有关
- 第1-3期患者存活率较高，第4期患者接受移植的概率最高

### 3. 缺失数据处理

测试了三种插补方法：简单插补、迭代插补和KNN插补。首先随机删除部分数据进行测试，发现迭代插补在5%数据缺失时表现最好，而KNN在10%数据缺失时表现最佳。迭代插补在分类少数类（CL）时效果最佳。

### 4. 不平衡类处理

针对标签状态的不平衡问题，采用了权重调整和SMOTE方法。权重调整在整体准确性方面略好于SMOTE，但在识别少数类CL方面表现较差。SMOTE在处理极不平衡数据集时表现更好。

### 5. 模型评估

尝试了六种模型：支持向量机（SVC）、梯度提升分类器（GBC）、随机森林分类器、高斯朴素贝叶斯、逻辑回归和XGBoost。XGBoost模型表现最好，并作为最终模型。各模型的详细参数和表现如下：

- **XGBoost**：logloss 0.50，精度和召回率均较高，尤其在CL类的召回率方面。
- **随机森林分类器**：logloss 0.506，准确率81%。
- **梯度提升分类器**：logloss 0.52，调整超参数后效果改善。
- **高斯朴素贝叶斯**：logloss 2.59，对CL类预测效果差。
- **逻辑回归**：logloss 0.81，准确率65%。
- **SVM**：logloss 2.1，对CL类的正确分类减少。

最终，XGBoost模型在测试集上的Kaggle评分为0.46593。

### 6. 建议

由于药物（Drug）与患者状态的相关性较低，建议在模型中忽略该特征。数值特征的重要性明显高于分类特征，建议进一步测试模型在没有分类特征时的表现。

### 7. 结论

研究强调了数据探索、有效的插补技术和适当的不平衡数据处理方法对预测模型的重要性。XGBoost模型在分类PBC患者状态方面表现最佳，具有最低的logloss和较高的准确率。尽管模型在整体准确率上优于基线估计，但由于N天（N Days）特征的重要性，建议仅对已住院多日的患者使用该模型
