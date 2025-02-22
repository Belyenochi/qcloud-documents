### 延时（Sleep）

#### 1. 简介
“延时组件”可以延迟指定时间后，继续执行集成流

#### 2. 操作配置

##### 参数配置

| 参数 | 数据类型 | 描述                  | 是否必填 | 默认值 |
| :--- | :------- | :-------------------- | :------- | ------ |
| 延迟时间   | int      | 指定的延迟时间（单位：毫秒） | 是       | 1000     |

##### 输出

组件输出的message信息如下：

| message属性 | 值                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | 继承上个组件的attribute信息                                  |                                               |
| error       | 执行成功后，error为空；执行失败后，error为dict类型，包含“Code”和“Description”字段：“Code”字段表示错误类型，“Description”字段表示错误具体信息 |
| attribute   | 继承上个组件的attribute信息                                  |
| variable    | 继承上个组件的variable信息                                   |
##### 数据预览

无

#### 3. 案例

1. 添加“延时组件”

![image-20210330173121330](https://qcloudimg.tencent-cloud.cn/raw/17a0ee88dc8ea5fd462299ee7ffbc632.png)


2. 填入要设置的延迟时间
![image-20210330173057043](https://qcloudimg.tencent-cloud.cn/raw/e9208042d139d4c1351264bf223a17cd.png)
