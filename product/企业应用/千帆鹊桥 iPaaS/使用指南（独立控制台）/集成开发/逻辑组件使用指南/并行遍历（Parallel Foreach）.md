### 并行遍历（Parallel Foreach）

#### 1. 简介

**并行遍历**（Parallel Foreach）用于并行执行任务，对数据集上的元素并行执行相同的处理逻辑。实际并行数取当前剩余元素数与设置最大并行度之间较小值。

并行遍历的子流可以只读访问主流的变量和其他组件输出，但子流所做的修改均是不影响主流

处理完成后，每个元素的处理结果按照原始顺序输出到message的payload中。并行遍历一般用于批量数据处理的场景，例如批量查询、批量导入数据等。

#### 2. 操作配置

##### 参数配置

| 参数    | 数据类型                 | 描述                                                                                                                                                                                     | 是否必填 | 默认值         |
|:------|:---------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----|-------------|
| 数据集   | string、list、dict、int | 待遍历的数据。<br/> 当类型为string时，遍历字符串的每个字符；<br/>当类型为list时，遍历list的每个元素；<br/>当类型为dict时，遍历dict中的value；<br/>当数据集类型为int时，例如3，实际遍历的数据集为[0,1,2]                                                      | 是    | 无           |
| 最大并行数 | int                  | 并行执行的任务数，取值范围为2~8                                                                                                                                                                      | 是    | 4           |
| 计数器   | string               | 计数器是一个变量，该变量存储了当前的迭代次数，从0开始，这里填入变量名称，msg.vars.get('#计数器变量#')即可使用；例：当计数器变量使用默认值counter时，第1次循环，msg.vars.get('counter')值为0，第2次循环，msg.vars.get('counter')值为1。                              | 否    | counter     |
| 根信息   | string               | 根信息同样是一个变量，这里填入变量名称，根信息中保存了主流的message信息。msg.vars.get('#根信息名称#').payload即可访问主流的payload数据。当使用默认值rootMessage时，使用msg.vars.get('rootMessage').payload即可在Parallel ForEach的子流中访问主流的payload数据。 | 否    | rootMessage |
| 错误时终止 | bool                 | 若子任务发生错误，则会在已发起的子任务执行完成后终止遍历                                                                                                                                                           | 否    | False       |

##### 配置界面

![img_19.png](https://qcloudimg.tencent-cloud.cn/raw/9db0a6efe6bf3948b589173f87eee9a4.png)

##### 数据预览

| 预览字段    | 数据类型 | 描述                               |
|:--------|:-----|:---------------------------------|
| payload | any  | 每次遍历的输入值，属于数据集的其中一个元素            |
| index   | int  | 每次遍历的位置，代表当前输入值在数据集中的下标位置，从0开始计数 |

![img_20.png](https://qcloudimg.tencent-cloud.cn/raw/be41642bcf0dd0d6c6e8f1d3998ba759.png)

数据预览的内容仅为子流可见，子流中的组件可以直接使用遍历组件的Payload和index，如图所示：

![img_21.png](https://qcloudimg.tencent-cloud.cn/raw/3a75988c25fa5914cd4a14681928f2df.png)

##### 输入到子流中的message

| message属性 | 值                                                                                                                                                                         |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payload   | 数据集中的元素，例如待迭代的数据集为[1,2,3]<br/>第一次循环，子流中payload的数据为1<br/>第二次循环为2<br/>当迭代的数据集为dict类型{"key":"key1", "value":"value1"}<br/>第一次循环，子流中的payload为value1<br/>第二次为value2            |
| error     | 空                                                                                                                                                                         |
| attribute | 空                                                                                                                                                                         |
| variable  | 继承主流中的variable数据，同时新增两个变量，一个是计数器，一个是根信息，若用户使用默认值，可使用表达式msg.vars.get('counter')和msg.vars.get('rootMessage')访问。<br/>若For Each中使用了Set Variable，则在子流执行过程中，新增的变量也会添加到varaible中 |

##### 输出

并行遍历的输出结果中，不会包含处理逻辑中使用的variable变量，最终输出的只有payload里的数据，输出的payload是个list类型变量，里边包含了原始数据集中每个元素迭代处理的结果，顺序与原始数据集一致。attribute的值继承自上一个组件。

组件输出的message信息如下：

| message属性 | 值                                                                                                |
|-----------|--------------------------------------------------------------------------------------------------|
| payload   | list类型，包含了每个数据的处理结果，输出顺序与原始的输入顺序一致                                                               |
| error     | 执行成功后，error为空；执行失败后，error为dict类型，包含“Code”和“Description”字段：“Code”字段表示错误类型，“Description”字段表示错误具体信息 |
| attribute | 继承Parallel ForEach上一个组件的attribute信息                                                              |
| variable  | 继承Parallel ForEach上一个组件的variable信息                                                               |

输出样例如下：

![img_22.png](https://qcloudimg.tencent-cloud.cn/raw/36d2770fa2e07b5bff2bfcadbc0b1084.png)

#### 3. 案例

本案例中，我们使用并行遍历对列表中的数据统一进行乘2操作，原始的数据集为[1,2,3,4]

1. 添加并行遍历组件，配置数据集[1,2,3,4]，并设置并行度为3

   ![img_23.png](https://qcloudimg.tencent-cloud.cn/raw/914a6113d49197c6c95dfe08e09f74d8.png)

2. 在并行遍历中加入配置Payload组件，对子流Payload执行乘2操作

   ![img_24.png](https://qcloudimg.tencent-cloud.cn/raw/8b1072f9f38fed089a8197c11f975c29.png)

3. 输出结果

   ![img_25.png](https://qcloudimg.tencent-cloud.cn/raw/f776153279fbd63b2b03dda53ef648a7.png)
