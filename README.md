﻿# Data Warehouse

### Submission

1.  ETL脚本

2.  E-R图

3.  物理存储模型（Schema）

4.  数据仓库导出文件（请按照每张表分别导出csv格式文件并压缩。文件名同表名）

5.  分布式文件系统导出文件，schema定义文件

6.  查询和统计程序

7.  每组准备一个答辩ppt，说明整体思考过程和解决方案。

8.  组员姓名学号&百分比

### TODO:

##### 前端

1. 季节的数据未发到后端

2. 先选季节再选月份的问题

3. Comprehenssive检索：

    3.1 先点时间再换成别的下拉框还在（可重复该过程产生无数下拉框）；

    3.2 input无法正常submit；

    3.3 复杂检索-高级检索，补上name，高级检索不要加上复杂检索中已有的项了。

4. 结果展示页无法回到主页

5. **所有的css/js无法正常获取**

6. 检索演员,需要加上选择[Starring/Supporting]的下拉框(默认Starring), value分别为'starring'和'supporting', name为'type'; 对应Comprehensive name类似time添加后缀, "\_0"是type, "\_1"是name

##### 后端

1. 执行stmt.executeQuery抛出异常时无法获取endtime，计时成负值（防护：为负时置0；待解决抛出异常问题，数据仓库没有建表）

2. 没有数据，不能看有没有成功检索到结果

3. 需要根据实际检索时间决定最终表示时间的单位（目前：**ns**）

### Solution

- 考虑到本项目为静态数据, 以提高检索&获取数据速度为重点:

    1. 针对各搜索高频度的属性建立维度表, 针对只需要统计总数的需求, 存储Count(即可通过直接查询一次dimension表得到结果);

    2. 为避免做字符串解析或join, 建立list分表(以Category为例, 总共约200,000条数据, 30个Category, 则平均每个分类下有约7,000部电影, 需要解析的字符串太长);

    3. 为方便直接读取每一部电影的数据, 同时将所有属性存储于movie表中, 并将属性统一存储为字符串而非子表.

- 根据未来可能添加数据的需求, 维护雪花模型:

    1. 即以movie表为fact表, movie表前半部分为属性值, 后半部分为维度表id(primary不使用拼接dimension id);

    2. 通过建立movie\_review\_bridge表构建review同movie的关联, 保留review中的ProductId.

### Optimization

- Category -> ProductId子表
- Name -> Hash

### Collaboration & Percentage

- 爬虫&数据解析: 张尹嘉(1452716, 25%)
- 数据仓库: 王冠淞(1452693, 25%)
- 前端: 项安颖(1452719, 25%)
- 后端: 王家慧(1452712, 25%)

### Schedule

a) 建模&建项目
>12.04 24:00

b) 抽数据&建数据仓库(Hadoop架构)
>12.08 24:00

c) 后端&前端实现
>12.13 24:00

d) 整理文件
>12.14 24:00

e) 填充数据
>12.17 24:00

f) 准备答辩
>01.?
