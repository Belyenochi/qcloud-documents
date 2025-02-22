### 错误捕获（Try-Catch）

#### 1. 简介

*错误捕获*组件由一个***执行***子流和一个或多个***捕获错误***子流组成。通过配置，可以捕获***执行***子流运行时抛出的错误和系统错误，也可与***抛出错误***组件搭配使用，捕获用户自定义错误。如果*执行*子流发生错误，将运行第一个匹配的***捕获错误***子流，如果没有匹配，则抛出错误到外层。

#### 2. 操作指引

##### 连接说明

无

##### 参数配置

| 参数     | 数据类型             | 描述                                                         | 是否必填 | 默认值 |
| :------- | :------------------- | :----------------------------------------------------------- | :------- | ------ |
| 事务     | 枚举（无；本地事务） | 和Database组件搭配使用，执行失败时回滚数据库操作             | 是       | 无     |
| 错误类型 | string               | 流执行过程中抛出的错误类型，通过下拉列表选择，支持任意多选，支持选择全部错误或者某一类错误 | 是       | 无     |
| 重试次数 | int                  | 发生此类错误时重试*执行*子流的次数（0-5次），每个***捕获错误***单独统计 | 是       | 不重试 |
| 重试间隔 | int                  | 重试时两次执行的间隔（1-300秒）                              | 否       | 60     |

事务在**开启错误捕获**节点配置

![](https://qcloudimg.tencent-cloud.cn/raw/eae301612ef6b85b1bfebd8b8219a5ef.jpg)

错误类型和重试在**捕获错误**节点配置

![](https://qcloudimg.tencent-cloud.cn/raw/38da9a6e91c13851ff9df8cf36da99af.jpg)

##### 数据预览

无

##### 输入到子流中的message

| message属性 | 值                                      |
| ----------- | --------------------------------------- |
| payload     | 继承***错误捕获***上一个组件的payload   |
| error       | 继承***错误捕获***上一个组件的error     |
| attribute   | 继承***错误捕获***上一个组件的attribute |
| variable    | 继承***错误捕获***上一个组件的variable  |

##### 输出

组件输出的message信息如下：

| message属性 | 值                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | 若***执行***子流正常运行，payload的结果为***执行***子流输出的payload。若抛出错误，且错误被捕获，则payload的结果为***捕获错误***子流输出的payload。若抛出的错误未被捕获，则流终止运行 |
| error       | 若***执行***子流抛出错误，且未被捕获，或者*捕获错误*子流中抛出错误，则error保存了错误信息，为dict类型，包含“Code”和“Description”字段：“Code”字段表示错误类型，“Description”字段表示错误描述。否则error为空 |
| attribute   | 若***执行***子流正常运行，attribute的结果为***执行***子流输出的attribute。若抛出错误，且错误被捕获，则attribute的结果为***捕获错误***子流输出的attribute。若抛出的错误未被捕获，则流终止运行 |
| variable    | 若***执行***子流正常运行，variable的结果为子流输出的variable。若抛出错误，且错误被捕获，则variable的结果为***捕获错误***子流输出的variable。若抛出的错误未被捕获，则流终止运行 |

#### 3. 案例

1. 新增自定义错误类型请求失败
2. 当请求失败时，抛出该错误
3. 捕获该错误，执行重试策略，会重新执行*执行*子流中的HTTP请求，条件判断。重试后仍失败，则记录日志

![](/Users/finalone/Library/Application Support/typora-user-images/image-20220628111844055.png)
