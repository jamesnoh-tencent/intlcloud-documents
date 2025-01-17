自动化助手提供了控制台、API 及 SDK 三种方式管理您的云服务。本文以使用轻量应用服务器控制台为例，快速开始使用自动化助手。

## 步骤1：安装自动化助手客户端

<dx-alert infotype="explain" title="">
- 2020年12月15日之后使用公共镜像创建的实例，默认已预装自动化助手客户端。若您的实例于2020年12月15日前购买，请参考以下步骤安装自动化助手客户端。
- 自动化助手仅支持使用私有网络 VPC 的实例。使用基础网络的实例将无法使用自动化助手，请按需切换网络。
</dx-alert>

请参考 [安装自动化助手客户端](https://intl.cloud.tencent.com/document/product/1147/46042) 完成安装。


## 步骤2：创建命令
1. 登录轻量应用服务器控制台，选择左侧导航栏中的 <b>[命令列表](https://console.cloud.tencent.com/lighthouse/command)</b>。
2. 在“命令列表”页面中，选择**创建命令**。
3. 在弹出的“创建命令”窗口中，根据参数说明设置参数。如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/4976802fc3d9274103281c70ea4ed204.png" style="width:70%"/>
<table>
<tr>
<th style="width:14%">参数</th>
<th>说明</th>
</tr>
<tr>
<td>命令名称</td>
<td>设置命令名称。</td>
</tr>
<tr>
<td>命令类型</td>
<td>按需选择命令类型。
</td>
</tr>
<tr>
<td>执行路径</td>
<td>自定义命令的执行路径。
<ul style="margin-bottom:0px">
<li>Linux 实例默认路径为 root 用户的 /home 目录。</li>
<li>Windows 实例默认路径为 System 权限的 C:\\Program Files\\qcloud\\tat_agent\\workdir 目录。</li>
</ul>
</td>
</tr>
<td>执行用户</td>
<td>自定义执行命令的用户。
<ul style="margin-bottom:0px">
<li>Linux 实例默认为 root 用户。</li>
<li>Windows 实例默认为 System 用户。</li>
</ul>
</td>
</tr>
<tr>
<td>超时时间</td>
<td>设置命令在实例中的超时时间，当执行命令的任务超时后，自动化助手将强制终止任务进程。单位为秒，默认为60秒，取值范围为[1, 86400]。</td>
</tr>
<tr>
<td>命令内容</td>
<td>编辑或者粘贴您的命令。</td>
</tr>
<tr>
<td>使用参数</td>
<td>是否在命令中使用参数。您可在命令中设置变量值，以 <code>{{key}}</code> 的形式表示。</td>
</tr>
</table>
4. 单击**保存命令**即可创建命令。

## 步骤3：执行命令

<dx-alert infotype="explain" title="">
使用自动化助手在实例上执行命令，指定的实例需要处于 VPC 网络。
</dx-alert>


1. 在“命令列表”页面中，选择所需执行命令所在行右侧的**执行**。
2. 在打开的“执行命令”窗口中，在“选择实例”下拉列表中选择需执行命令的实例。
3. 单击**执行命令**即可执行命令。
命令执行完成后，您可在“我的命令”页面选择命令所在行右侧的**日志**，进入“日志详情”页面查看命令执行结果。
