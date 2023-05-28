## Column Explanation
```
pH：水的pH值。
Iron：水中铁的含量。
Nitrate：水中硝酸盐的含量。
Chloride：水中氯化物的含量。
Lead：水中铅的含量。
Zinc：水中锌的含量。
Color：水的颜色。
Turbidity：水的浑浊度。
Fluoride：水中氟化物的含量。
Copper：水中铜的含量。
Odor：水的气味。
Sulfate：水中硫酸盐的含量。
Conductivity：水的电导率。
Chlorine：水中氯的含量。
Manganese：水中锰的含量。
Total Dissolved Solids：水中的总溶解固体含量。
Source：水源。
Water Temperature：水的温度。
Air Temperature：空气温度。
Month：月份。
Day：天数。
Time of Day：一天中的时间。
Target：目标变量，可能是水质等级或其他评价水质的标准。

pH：水的酸碱度能够影响生物生存的环境，过高或过低的pH都可能影响水质。
Iron, Lead, Zinc, Copper, Manganese：这些重金属的浓度过高可能会对人类和环境产生毒性影响，因此它们的浓度是评价水质的重要指标。
Nitrate, Chloride, Sulfate：这些离子的浓度可能反映水源的污染程度。例如，高硝酸盐水平可能来源于农田排水，这可能影响水质。
Color, Odor：这些是水质感官属性，与水质直接相关。例如，不正常的颜色或气味可能表示有污染物存在。
Turbidity：水的浑浊度可能表明有悬浮颗粒或溶解固体存在，这些可能会影响水质。
Fluoride, Chlorine：虽然适量的氟和氯对人体有益，但过量则可能导致健康问题。
Total Dissolved Solids：这是一个广义的度量，表示水中的总溶解固体含量，它可能与水质有关。
Source：水源可能影响水质，因为不同的源头可能存在不同的污染物。
Water Temperature, Air Temperature：温度可能影响水中的化学反应和溶解度，从而影响水质。
Month, Day, Time of Day：这些时间因素可能影响水质，因为某些污染事件可能在特定的时间发生（例如，农业排水可能在特定季节更为严重）。
```

## Prerequisites
Upgrade packages

```sh
pip install pip-review
pip-review --auto
```

Install modin Ray engine

```sh
pip install "modin[all]"
```

## Description - To Be Refined
该方案使用英特尔oneAPI AI库和相关工具,通过机器学习模型预测淡水样本的质量及是否适合饮用和生态系统使用。我们使用C++和SYCL编程语言调用oneAPI工具包,构建机器学习pipeline。
方案架构:数据采集->数据预处理->特征工程->模型训练->模型评估->模型优化->模型推理。
使用的算法和模型:随机森林,XGBoost。
优化技术:超参数调整,特征选择等提高模型精度;使用oneAPI工具优化模型部署在不同设备上加速推理速度。
使用oneAPI工具:
oneAPI AI分析工具套件:数据处理、机器学习框架(MLAPI)
oneAPI 基础工具套件:SYCL直接编程模型,优化编译器等

方案扩展性和优势:
数据量大时,可以优化模型并行化训练,提高训练速度。支持更大数据量训练更强大的模型。
oneAPI具有跨架构部署工具,模型可以部署在CPU、GPU、FPGA等不同设备上,实现硬件异构计算,提高推理速度与吞吐量。
方案结构灵活,可针对新数据和问题作进一步优化。可增加新特征,调整超参数,尝试不同的机器学习模型等。
oneAPI提供统一的编程模型和工具,从数据到部署实现端到端的机器学习和深度学习工作流程。该方案利用oneAPI工具的优势,提出针对水质预测的高效且可扩展的机器学习解决方案。

---

#### 程序架构和流程图

该程序由三个主要组件组成：

- 数据收集和预处理
- 机器学习模型训练
- 淡水质量预测

数据收集和预处理组件负责从各种来源收集数据并对其进行预处理，以便在机器学习模型中使用。机器学习模型训练组件负责在预处理后的数据上训练机器学习模型。淡水质量预测组件负责使用训练好的机器学习模型来预测任何位置的淡水质量。

我们的流程为：数据采集 -> 数据预处理 -> 特征工程 -> 模型训练 -> 模型评估 -> 模型优化 -> 模型推理。

#### 使用的算法和模型

我们可能考虑使用的一些算法和模型包括：

- 线性回归
- 逻辑回归
- 支持向量机
- XGBoost
- 随机森林
- 神经网络

#### 优化技术

我们将使用各种优化技术来提高我们机器学习方案的性能，包括：

- 数据降维
- 特征选择
- 超参数调整
- 正则化

#### 使用oneAPI工具

在我们的方案中，我们将使用各种 oneAPI 相关工具。这些工具包括：

- Intel® Extension for Scikit-learn
- Intel® Optimization for XGBoost
- Intel® Distribution for Python
- Intel® Distribution of Modin
- Intel® Neural Compressor


## Test Result

1. Selected: ['Color', 'Turbidity', 'Copper', 'Manganese', 'Chloride', 'Iron','Fluoride', 'Nitrate',
                'Odor', 'Chlorine', 'Sulfate', 'Total Dissolved Solids', 'Zinc', 'pH']
    > SVC: Test F1 accuracy: 70.98%, AUC: 0.85827
    >
    > XGB: Test F1 accuracy: 81.30%, AUC: 0.91964
    >
    > RFC: Test F1 accuracy: 82.68%, AUC: 0.91699
    >
    > NN:  Test F1 accuracy: 78.78%, AUC: 0.90347

