## 引言
本项目属于探索性数据分析项目（Explore Data Analysis）。项目所涉及的Prosper 贷款数据集包括了2005-11到2014-03期间113,937 项贷款记录，每项贷款有
81个变量。本项目诣在探索哪些因素会影响借贷状态（这里主要指"Defaulted"和"Completed"两种状态）。通过选择了重要的16个变量，利用R语言及其ggplot包
探索了单变量、双变量、多变量对贷款状态（LoanStatus）的影响。

## 安装
为了完成此项目，你需要安装 R。你可以从 [CRAN](https://cran.r-project.org/) 下载并安装 R。
安装 R 以后，你需要下载并安装 [R Studio](https://www.rstudio.com/products/rstudio/download/)。为你的操作系统选择合适的安装方式。
最后，你需要安装一些包。我们建议你打开 R Studio，通过命令行安装以下包：
install.packages("ggplot2", dependencies = T) 
install.packages("knitr", dependencies = T)
install.packages("dplyr", dependencies = T)

## 使用

#### 导入包
library(ggplot2)
library(gridExtra)
library(grid)
library(dplyr)
library(GGally)
library(knitr)

#### 了解数据集
导入csv数据集后，从整体上认识数据集，例如：通过dim()函数了解数据集维度，str()了解各变量名称及其数据类型，summary()函数了解数值类型变量的统计学特征等。

#### 简单的数据清理
将数据集中所涉及到的12种贷款状态调整为待研究的两种状态（"Defaulted"和"Completed"），调整主要是依据Prosper内部对贷款状态的定义来完成；
选择待研究的16个变量组成待研究数据集，内部需要进行简单的数据清理，如变量类型转换等；
需要注意的是该贷款机构在2009-7调整过贷款等级和贷款评分制度，所以当研究这两个变量时，需要分别对待。

#### 单变量分析
本项目所选择的变量包含三方面：首先是借贷人员的人身特性，例如就业状态及时长（EmploymentStatus/EmploymentStatusDuration），
债务与收入比例（DebtToIncomeRatio），收入范围（IncomeRange），是否有房子（IsBorrowerHomeowner），居住在哪个州（BorrowerState）等，其次是借贷
人的行为特性，比如信用等级及评分（CreditGrade/ProsperRating/ProsperScore），借贷原因（ListingCategory），过去7年信用额度情况（TotalCreditLinespast7years），
银行卡使用情况（BankcardUtilization）等，最后是一些贷款特性，例如贷款期限（Term），贷款利率（BorrowerRate）等。
单变量研究中，通过直方图或柱状图研究上述变量的分布情况。

#### 双变量分析
双变量分析的核心方向是探索所选变量与贷款状态的有趣关系。通过spineplot、箱线图、柱状图和散点图等图形工具探索所选变量对贷款违约率（违约数/总贷款项目数）
的影响情况，试图找到影响最强的变量，或者说是关系最强的变量。

#### 多变量分析
在双变量探索中发现了最强的关系后，以此为主线加入其它变量进行多变量探索分析。即在双变量基础上，加入颜色及形状探索多变量关系。

## 建模
通过逻辑回归模型，预测贷款是否会发生违约。

### 数据处理
1.通过数据处理重新调整贷款状态分类，最终将所有状态划分为二，违约和按时还款；
2.将缺失值较多的特征进行缺失值填充，去除与预测变量无关的特征；
3.根据需要创建新的变量。

### 特征选择
采用基于L1的惩罚项特征选择，将重要性低的特征系数转换为0，提升特征稀疏度。

### 创建逻辑回归模型
1.创建逻辑回归模型；
2.使用训练集训练模型；
3.模型在测试集的评分；
4.模型预测；

### 通过学习曲线查看模型效果

## 附言
具体的代码及可视化图形请参考Github中ProsperLoan-Data-Exploration项目其它文件。
