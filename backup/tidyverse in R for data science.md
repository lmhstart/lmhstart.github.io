## 前言

> [!note] 
**tidyverse** 是由 **Hadley Wickham** 及其团队开发的一系列R语言包的集合，它们有着共同的**设计哲学、语法和数据结构**，旨在使数据科学的整个过程——从数据导入到可视化和建模——更加**简单、高效且易于理解**。


顾名思义，tidyverse库的作用核心是==“tidy”==，让数据处理更加==整洁美观==



下载方法：
```R
install.packages("tidyverse")
```



`tidyverse` 实际上是一个**元包 (Metapackage)**，在里面其实有多种核心包(dplyr,ggplot2,tidyr,readr,purr,tibble,stringr,forcats)，
- **数据导入:** 使用 `readr` 包
    
- **数据整理:** 使用 `tidyr` 包
    
- **数据操作:** 使用 **`dplyr`** 包
    
- **数据可视化:** 使用 `ggplot2` 包
    
- **函数式编程:** 使用 `purrr` 包

每次使用时，必须像这样`library(tidyverse)`将包导入

> [!tip] 
在详细介绍之前，我需要补充一个非常方便的东西———管道操作符`%>%`，打印方法非常简单，Windows系统只需要摁住Ctrl+Shift+M快捷键打出。
管道操作符 是 `tidyverse` 风格的精髓。它允许您将上一步的结果直接作为下一步函数的**第一个参数**。这使得代码流程清晰、可读性极高。


下面我们着重介绍最常用的两个包——`dplyr`和`ggplot2`


## dplyr包

此包的主要功能是数据**操作**和**转换**，提供一套用于**筛选 (filter)**、**选择 (select)**、**排列 (arrange)**、**新建变量 (mutate)** 和**汇总 (summarise)** 等数据处理的“动词”。

#### 1. 筛选行：`filter()`

**功能：** 根据变量的**值**，选择符合条件的行（观测）。

```R
# 选出所有来自“北京”的客户
data_frame %>% 
  filter(city == "北京") 
```

#### 2. 重排列行：`arrange()`

**功能：** 根据一个或多个变量的值对行进行**排序**。

```R
# 按年龄升序排列，如果年龄相同，则按收入降序排列
data_frame %>% 
  arrange(age, desc(income)) 
```

#### 3. 选择列：`select()`

**功能：** 根据变量的**名称**，选择、删除或重命名列。

```R
# 仅保留 'ID'、'name' 和 'salary' 三列
data_frame %>% 
  select(ID, name, salary)

# 删除 'notes' 这一列
data_frame %>% 
  select(-notes)
```

#### 4. 添加或修改列：`mutate()`

**功能：** 利用现有变量的值，**创建新的变量（列）**，或修改现有变量。

```R
# 计算人均消费（总消费/月数）
data_frame %>% 
  mutate(avg_spend = total_spend / months)
```

#### 5. 汇总数据：`summarise()`

**功能：** 将多行数据**塌缩**为一行，计算出汇总统计量（如均值、总和、计数）。

```R
# 计算所有客户的平均年龄和最高收入
data_frame %>% 
  summarise(
    mean_age = mean(age, na.rm = TRUE),
    max_income = max(income)
  )
```

## ggplot2包

此包的主要功能是数据**可视化**，基于**图形语法，提供强大、灵活且美观的绘图功能

```R
library(tidyverse)

ggplot(data = <数据框>) +
  geom_<图形类型>(mapping = aes(<x轴变量>, <y轴变量>, color = <分组变量>))
```


 ---

# 实际运用


看完这些可能还是很模糊，接下来结合**实际运用**

这里直接使用R里的著名数据集`mpg

>ps：`mpg` 数据集观测了 **38 种不同型号汽车**在 1999 年和 2008 年的各种性能和分类数据

|**变量名**|**含义 (What it measures)**|**类型**|
|---|---|---|
|`manufacturer`|制造商名称 (e.g., audi, ford)|字符/分类|
|`model`|汽车型号名称|字符/分类|
|**`displ`**|**发动机排量**（Liters）|连续|
|**`year`**|汽车生产年份|离散|
|**`cyl`**|**气缸数**（4, 5, 6, 8）|离散|
|**`trans`**|变速器类型（自动或手动）|字符/分类|
|**`drv`**|驱动类型（前驱 `f`，后驱 `r`，四驱 `4`）|字符/分类|
|**`cty`**|**城市燃油效率**（city miles per gallon, MPG）|连续|
|**`hwy`**|**高速公路燃油效率**（highway miles per gallon, MPG）|连续|
|`fl`|燃油类型 (e.g., r: Regular, p: Premium)|字符/分类|
|`class`|汽车类型/级别（e.g., SUV, compact）|字符/分类|
首先，加载库
```R
library(tidyverse)
data(mpg)
```

### 1. 改变和创建变量：`mutate()`

**目标：** 计算城市（`cty`）和高速（`hwy`）燃油效率的**平均值**，并将其转换为更直观的 **每百公里油耗 (L/100km)**。

```R
mpg_mutated <- mpg %>%
  mutate(
    avg_mpg = (cty + hwy) / 2,
    l_per_100km = 235.21 / avg_mpg,
	    )
```

对比：
直接使用R的基础用法：
```R
mpg$avg_mpg <- (mpg$cty + mpg$hwy) / 2
mpg$l_per_100km <- 235.21 / mpg$avg_mpg
```
不难发现需要重复使用 '$' 符号

### 2. 筛选行观测：`filter()`

**目标：** 筛选出产于 **2008 年**，且 **城市油耗（`cty`）高于 20 MPG** 的车型。

```R
mpg_filtered <- mpg %>%
  filter(
    year == 2008,     # 筛选2008年的车型
    cty > 20          # 城市油耗高于20
  ) %>%
  select(manufacturer, model, cty, hwy)

mpg_filtered
```

对比：
直接使用R的基础用法：
```R
mpg_filtered_base <- mpg[mpg$year == 2008 & mpg$cty > 20, ]
```
也不难发现，使用下标 '[]' 和 '&' 符号，语句较长

### 3. 选择列变量：`select()`

**目标：** 只保留描述汽车**基本特征**（制造商、型号、排量）和**油耗指标**（`cty`, `hwy`）的列。

```R
mpg_selected <- mpg %>%
  select(
    manufacturer, # 选择 'manufacturer'
    model,        # 选择 'model'
    displ,        # 选择 'displ'
    starts_with("c"), # 选择以 'c' 开头的变量 (cty, class)
    contains("wy") # 选择包含 'wy' 的变量 (hwy)
  )

mpg_selected %>% head(3)
```

对比：
直接使用R的基础用法：
```R
mpg_selected_base <- mpg[, c("manufacturer", "model", "displ", "cty", "hwy")]
```

### 4. 按组拆分：`group_by()` 和 5. 聚合总结：`summarise()`

`group_by()` 负责将数据按某一分类变量分组；`summarise()` 负责对每个组计算汇总统计量。

```R
mpg_summary <- mpg %>%
  group_by(drv) %>% # 1. 按驱动类型分组 ('4', 'f', 'r')
  summarise(
    # 2. 计算每个组的平均高速油耗
    mean_hwy = mean(hwy, na.rm = TRUE),
    # 3. 计算每个组的车型数量
    count = n(),
    # 4. 计算油耗的标准差
    sd_hwy = sd(hwy, na.rm = TRUE)
  ) %>%
  # 5. 管道操作：按平均油耗降序排列结果
  arrange(desc(mean_hwy))

mpg_summary
```

对比：
直接使用R的基础用法：
```R
avg_hwy_base <- tapply(mpg$hwy, mpg$drv, mean)
count_base <- table(mpg$drv)
```
劣势：使用 tapply，只能聚合一列


### 6. 数据可视化：`ggplot2`

**目标：** 绘制**发动机排量（`displ`）**与**高速油耗（`hwy`）**之间的关系，并按**汽车类型（`class`）**着色。

`ggplot2` 是 `tidyverse` 的可视化组件，基于图形语法（Grammar of Graphics）。

```R
# 使用 ggplot2 绘制散点图
mpg %>%
  ggplot(aes(x = displ, y = hwy, color = class)) + # 1. 定义数据和映射 (aes)
  geom_point() +                                   # 2. 添加几何对象 (散点图)
  geom_smooth(method = "lm", se = FALSE) +         # 3. 添加线性回归趋势线
  labs(                                            # 4. 添加标签
    title = "发动机排量与高速油耗的关系",
    x = "发动机排量 (L)",
    y = "高速油耗 (MPG)",
    color = "汽车类型"
  ) +
  theme_minimal() # 5. 应用简洁主题
```

