## 操作场景
WebShell 为腾讯云推荐的登录方式，您可以直接使用腾讯云 WebShell 工具一键登录 Linux 实例。其优点如下：
- 支持复制、粘贴。
- 支持鼠标滚屏。
- 支持中文输入法。


<dx-alert infotype="explain" title="">
- 创建 Linux 操作系统的轻量应用服务器时，该服务器默认绑定1个密钥。此密钥对应的用户名为 `lighthouse`，具备 root 权限。
- 当您使用 WebShell 工具登录 Linux 实例时，系统默认使用此密钥（对应的用户名为 `lighthouse`）进行登录。
</dx-alert>



## 适用本地操作系统
Windows，Linux 或者 Mac OS

## 前提条件

在登录前，请确认实例的防火墙已放行22端口（创建实例时默认已开通22端口）。

## 操作步骤

1. 登录 [轻量应用服务器控制台](https://console.cloud.tencent.com/lighthouse/instance/index)。
2. 在服务器列表中找到对应的实例，并根据实际的操作习惯选择不同的方式进行登录。
 - 在服务器列表中的实例卡片上，单击**登录**。
![](https://main.qcloudimg.com/raw/ad83b4066ea56c22ca1593a6ab808ff0.png)
 - 单击实例卡片进入服务器详情页，单击“远程登录”中的**登录**，或页面右上角的**登录**。
![](https://qcloudimg.tencent-cloud.cn/raw/1b953c64f89f4efc541616159189b841.png)
 - 使用 [应用镜像](https://cloud.tencent.com/document/product/1207/44361#appOS) 创建的实例，可在实例详情页选择**应用管理**，单击页面右上角的**登录**。
![](https://qcloudimg.tencent-cloud.cn/raw/3ca1397e8ee72ff5e762271d05fa82ae.png)
登录成功界面如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/c35791160e39774e72a7f0b1cc25f8b2.png)
    - 成功登录后，您可参考 [最佳实践](https://cloud.tencent.com/document/product/1207/45116) 及 [第三方教程](https://cloud.tencent.com/document/product/1207/58793)，进行搭建中小型网站、Web 应用、博客、论坛、小程序/小游戏、电商、云盘/图床、云端开发测试和学习环境等轻量级、低负载且访问量适中的应用。
    - WebSehll 界面功能丰富，您可参考 [更多 WebShell 功能](#wedShellWork) 使用移动端的虚拟键盘，在控制台上更改 WebShell 外观、上传/下载文件、发起实例自助检测、开启多会话、分屏、获取提示，开启轻量应用服务器的便捷使用。

## 相关操作
### 关闭或开启 WebShell 一键登录


<dx-alert infotype="explain" title="">
服务器创建成功后，默认开启 WebShell 一键登录功能，您可参考以下步骤进行关闭或再次开启 WebShell 一键登录功能。
</dx-alert>


1. 登录 [轻量应用服务器控制台](https://console.cloud.tencent.com/lighthouse/instance/index)。
2. 在服务器列表中找到对应的实例，进入服务器详情页。
3. 在“远程登录”的“一键登录”中，按需选择**开启**或**关闭** WebShell 一键登录：
 - **关闭**：当无需使用一键登录时，可选择关闭此功能。
<dx-alert infotype="notice" title="">
- 关闭一键登录后，并不会影响您使用本地 SSH 客户端远程登录实例，您也可以选择再次开启一键登录功能。
- 关闭一键登录操作并不会在实例操作系统中同步删除系统默认密钥的公钥（默认保存在操作系统的 lighthouse 用户下）。您可以自行删除公钥，但删除将会导致再次开启一键登录功能无效。
</dx-alert>
 - **开启**：开启一键登录后，您可以基于系统默认密钥实现浏览器 WebShell 一键登录实例。
<dx-alert infotype="notice" title="">
请确认系统默认私钥的公钥（默认保存在操作系统的 lighthouse 用户下）未被删除，否则开启后仍无法正常一键登录。
</dx-alert>



### 更多 WebShell 功能[](id:wedShellWork)

WebShell 目前具备丰富的功能，希望您在使用过程中拥有满意的体验。欢迎您参与 [WebShell 使用满意度调研](https://wj.qq.com/s2/10389082/ca3a/) 来提出更多建议或反馈，我们会不断改进 WebShell，使您拥有更好的产品体验！

WebShell 功能介绍如下：
<dx-accordion>
::: 上传/下载文件[](id:updownload)



您可通过该步骤，向实例上传本地文件，或将实例文件下载至本地。具体步骤如下：

1. 参考 [使用 WebShell 方式登录 Linux 实例](https://cloud.tencent.com/document/product/1207/44642)，登录实例。
2. 选择 WebShell 界面工具栏中的 <img src="https://qcloudimg.tencent-cloud.cn/raw/81fbdd2c2b7cb70f17c508073496f58e.png" style="margin:-3px 0px">。
3. 在弹出的菜单中，选择**上传**或**下载**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/40a90811712d7800c21f309d2971fa81.png)
具体操作步骤如下：
    - **上传文件**：
       1. 在弹出窗口的“选择上传文件和位置”窗口中，选择 `点击上传`。
       2. 在弹出窗口中，选择文件后单击**确定**。
       3. 上传位置请选择 `home > lighthouse` 目录。
    <dx-alert infotype="explain" title="">
目前仅支持上传文件至  `home > lighthouse` 目录。
  </dx-alert>
       4. 单击**确定**即可。您可单击页面右下角的 <img src="https://qcloudimg.tencent-cloud.cn/raw/a78e204de7cde3473482732c8b9fef98.png" style="margin:-3px 0px">，在弹出窗口中查看操作结果。上传成功则如下图所示：
    ![](https://qcloudimg.tencent-cloud.cn/raw/742c648fbb6191849f0f1b4ad31df288.png)
    - **下载文件**：
       1. 在弹出窗口的“下载文件”窗口中，依次再开目录，选择需下载的文件。
       2. 单击**确定**，并在弹出窗口中，选择需存储的本地位置。
       3. 您可单击页面右下角的 <img src="https://qcloudimg.tencent-cloud.cn/raw/a78e204de7cde3473482732c8b9fef98.png" style="margin:-3px 0px">，在弹出窗口中查看操作结果。下载成功则如下图所示：
   ![](https://qcloudimg.tencent-cloud.cn/raw/5e54b868de203f3dd24e4213eb9ad194.png)

:::
::: 使用实例自助检测[](id:selfCheck)

若您在登录或使用实例过程中遇到问题，可随时使用实例自助检测。步骤如下：

1. 参考 [使用 WebShell 方式登录 Linux 实例](https://cloud.tencent.com/document/product/1207/44642)，登录实例。
2. 选择 WebShell 界面工具栏中的 <img src="https://qcloudimg.tencent-cloud.cn/raw/2d3d7e693d09bb8a58d58557e4f25ff4.png" style="margin:-3px 0px">。
3. 在弹出的“实例自助检测”窗口中，单击**确定**即可使用实例自助检测。您可参考 [使用实例自助检测](https://cloud.tencent.com/document/product/1207/74704) 了解实例自助检测及检测项。


:::
::: 开启多标签窗口会话[](id:multilabel)

您可通过该步骤，在 WebShell 界面以标签的形式打开多个实例连接界面，以便捷使用实例。具体步骤如下：

1. 参考 [使用 WebShell 方式登录 Linux 实例](https://cloud.tencent.com/document/product/1207/44642)，登录实例。
2. 选择 WebShell 界面上方的 <img src="https://qcloudimg.tencent-cloud.cn/raw/fc93655617db690aecdc7b1cea0baf39.png" style="margin:-3px 0px">。
3. 您即可看到已新建了标签 `(1)实例 ID`，如下图所示：
<dx-alert infotype="explain" title="">
- 最多支持同时打开5个标签。
- 标签将以 `（递增数字）实例 ID` 命名，帮助您区分标签。
</dx-alert> <img src="https://qcloudimg.tencent-cloud.cn/raw/b978c74d0b6c127e0948de0a39716dc4.png"/>


:::
::: 开启分屏[](id:splitScreen)

您可通过该步骤，在 WebShell 界面开启分屏，开启后您可同屏查看并执行多个操作任务，以便捷使用实例。具体步骤如下：

1. 参考 [使用 WebShell 方式登录 Linux 实例](https://cloud.tencent.com/document/product/1207/44642)，登录实例。
2. 选择 WebShell 界面上方的 <img src="https://qcloudimg.tencent-cloud.cn/raw/bf17a1103ce6fa76150df87768987f79.png" style="margin:-3px 0px">。
3. 您即可看到已执行分屏，命名为 `(1)实例 ID`。如下图所示为3个分屏效果：
<dx-alert infotype="explain" title="">
- 最多支持同时4个分屏。
- 分屏将以 `（递增数字）实例 ID` 命名，帮助您进行区分。
</dx-alert> <img src="https://qcloudimg.tencent-cloud.cn/raw/4d4b2c02d5173c92fe189c358c71a29f.png"/>


:::
::: 更改皮肤[](id:changeAppearance)

您可通过该步骤，修改 WedShell 界面的文字大小、字体及配色。具体步骤如下：

1. 参考 [使用 WebShell 方式登录 Linux 实例](https://cloud.tencent.com/document/product/1207/44642)，登录实例。
2. 选择 WebShell 界面工具栏中的 <img src="https://qcloudimg.tencent-cloud.cn/raw/183be38a53180ccd705dddbb859820e3.png" style="margin:-3px 0px">。
3. 在弹出的菜单中修改字体大小、字体或配色，按照喜好更改 WebShell 外观。
![](https://qcloudimg.tencent-cloud.cn/raw/cca68be8bd34a8aa7be49387322701e5.png)



:::
::: 使用移动端虚拟键盘[](id:virtualKeyboard)


1. 微信搜索“腾讯云助手”小程序，并登录腾讯云账号。
2. 选择页面下方的**控制台**，并单击页面中“收藏的云产品”中的**更多云产品**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/194d2b7f4625d0442f1546eda1bb7816.jpg)
3. 在“云产品中心”页面，选择**轻量应用服务器**。
4. 在“轻量应用服务器”控制台页面，选择实例所在地域，并单击实例卡片中的 <img src="https://qcloudimg.tencent-cloud.cn/raw/278e10214177bff2c64ae55480c99493.png" style="margin:-3px 0px">。
5. 在弹出窗口中，单击**登录**。
6. 登录成功后，可选择键盘右上方的**虚拟**。开启后如下图所示，您可再次单击**系统**切换回手机系统键盘。
![](https://qcloudimg.tencent-cloud.cn/raw/87ca1e1fb1ac9d20f664a19722a639bd.jpg)



:::
</dx-accordion>






