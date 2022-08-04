# WAIC 2022 Hackathon Causal Learning and Decision Optimization Challenge
2022 WAIC 黑客松九章云极赛道-因果学习和决策优化挑战赛

## 任务和主题
---
因果学习可以通俗地定义为一个结合了因果推断和机器学习，研究因果关系和回答因果问题的人工智能技术。本次挑战赛以“如何优化干预方案能使因果效应最大”为主题，考察参赛者在基于因果推断策略制定问题上的估计能力。

九章云极DataCanvas公司准备了两份生成数据：train.csv和test.csv.
其中，训练集数据train.csv包括三类列变量：

+ 特征列，名为‘V_0’, ‘V_1’等的列：离散和连续特征均有；
+ 干预方案列，名为‘treatment’的列：是一个拥有3个值的离散变量。其中，treatment=0视为未施加干预，treatment=1, 2分别视为施加了干预方案1和干预方案2；
+ 结果列，名为‘outcome’的例：是一个连续型变量。

测试集数据test.csv 只包含一类特征列变量，移除了‘treatment’ 和 ‘outcome’两列。

数据的生成过程遵从所示因果图。其中，X为treatment, Y 为 outcome，其余字母代表了数据集中的其他变量或变量集合，但不对选手公布。

>> enter image description here

请注意，数据集在生成过程中有如下假设：

1. 没有未观测到的confounder；
2. SUTVA 即每个个体的outcome不被其他个体的treatment影响；
3. 每个个体采取每个treatment的概率都不为0或1。

选手首先在训练集train.csv上利用不同的因果推断，机器学习和数据处理等手段，估计每个样本在干预方案1和干预方案2下的因果效应。其次，选手需要对test.csv中的新样本也估计得到干预方案1和干预方案2的因果效应。提示：选手可尝试使用因果发现，因果效应识别等辅助手段，使估计的结果更加准确。

## 比赛数据
---
比赛使用的数据是生成数据，已进行脱敏处理，是一个没有场景的通用数据集。
其中，训练集（train.csv）的数据量为36188；测试集（test.csv）的数据量为 5000。

## 结果提交
---
1. 选手在train.csv中分别估计得出干预方案1，干预方案2的因果效应，记作df_1；例如，若数据格式为pandas.DataFrame, 则其shape应为（train.csv的行数, 2）；
2. 在test.csv中的数据上分别估计得出干预方案1，干预方案2的因果效应，记作 df_2；
3. 将df_2拼接在df_1之后，拼接后的shape为(train.csv的行数+test.csv的行数，2)，一起作为结果文件result.csv输出，表头应为 ‘ce_1’, ’ce_2’。
4. 在天池平台提交结果文件result.csv，查看评分。

## 评价指标
---
评估指标是干预方案1的因果效应与真实因果效应之间的normalized RMSE (NRMSE)，加上干预方案2的因果效应与真实因果效应之间NRMSE。NRMSE具体的表达式为：
enter image description here
其中，
enter image description here是第i个样本的因果效应估计值；
enter image description here是因果效应的真实值；
enter image description here是真实值的mean。

总的评价得分为
enter image description here

其中
enter image description here为干预方案1的NRMSE
enter image description here为干预方案2的NRMSE

## 比赛阶段
---
1. 报名成功后，参赛队伍通过天池平台下载数据，本地调试代码，在线提交结果。
+ 比赛训练集-train.csv；
+ 比赛测试集-test.csv；
2. 九章云极DataCanvas公司提供了一个基于因果推断工具YLearn解题的基准示例，帮助选手快速理解赛题，详见论坛置顶的notebook。（选手不限于使用所提供的工具）
+ 基准示例-baseline_example

## 评分规则
---
1. 以所得score（两个NRMSE之和）为唯一评价指标对选手进行排序，score值越小越好。
2. 评价指标score的排名占最终比赛评比的权重为100%；
