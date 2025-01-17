## 操作场景

轻量应用服务器提供重置实例登录密码的功能。主要应用在以下场景：
- 首次从本地计算机远程登录实例：
 - 首次使用远程登录软件（或使用 SSH ）登录 Linux 实例前，您需要通过此操作重置用户名（root）的密码。
 - 首次登录 Windows 实例前，若您在创建实例时“登录方式”选择了“自动生成密码”，则建议通过此操作重置管理员帐号（如 Administrator）的密码，更换为自定义登录密码。
- 忘记密码：如果您遗忘了密码，您可以在控制台上重新设置实例的登录密码。

## 注意事项
- 只有处于关机状态的实例才允许执行重置密码操作。
- 对于正在运行的实例，在重置密码过程中会关闭服务器。为了避免数据丢失，请提前规划好操作时间，建议在业务低谷时进行此操作，将影响降到最低。
- 使用 Ubuntu 镜像创建的实例默认禁用 root 用户名通过密码的方式登录实例。如需开启，[请参考 Ubuntu 系统如何使用 root 用户登录实例？](https://intl.cloud.tencent.com/document/product/1103/41257)。
- 为提升实例的安全性，建议您使用 SSH 密钥对的方式登录 Linux 实例。详情请参见 [管理密钥](https://intl.cloud.tencent.com/document/product/1103/41392)。

## 操作步骤

1. 登录 [轻量应用服务器控制台](https://console.cloud.tencent.com/lighthouse/instance/index)。
2. 在“服务器”页面中，单击待重置密码的实例的卡片。
3. 进入实例详情页后，单击页面右上角的**重置密码**。
4. 在弹出的窗口中，根据实例状态的不同，重置密码操作会有一定差别，具体如下：
<dx-tabs>
::: 实例为“运行中”
如果需要重置密码的实例为 “运行中” 状态，执行以下操作：
 1. 确认需要重置密码的用户名，输入对应的 “新密码” 和 “确认密码”，单击**下一步**。如下图所示：
 <dx-alert infotype="notice" title="">
    其中“用户名”类型默认为“系统默认”，并使用对应操作系统的默认用户名（Windows 系统默认用户名为 `Administrator`、Ubuntu 系统默认用户名为 `ubuntu`、其他版本 Linux 系统默认为 `root`）。如您需指定其他用户名，请选择“指定用户名”并输入对应用户名称。
    </dx-alert>
    ![](https://qcloudimg.tencent-cloud.cn/raw/d2e31e20f88cd7dc9167c2cdb77af60d.png)
 2. 勾选 “同意强制关机”，单击**重置密码**，完成重置。如下图所示：
     ![](https://qcloudimg.tencent-cloud.cn/raw/c7da2fb6683367bae3e1b8cf4aec38c8.png)
     :::
     ::: 实例为“已关机”
     如果需要重置密码的实例为 “已关机” 状态，执行以下操作：
 1. 确认需要重置密码的用户名，输入对应的 “新密码” 和 “确认密码”，单击**下一步**。如下图所示：
	<dx-alert infotype="notice" title="">
	其中“用户名”类型默认为“系统默认”，并使用对应操作系统的默认用户名（Windows 系统默认用户名为 `Administrator`、Ubuntu 系统默认用户名为 `ubuntu`、其他版本 Linux 系统默认为 `root`）。如您需指定其他用户名，请选择“指定用户名”并输入对应用户名称。
	</dx-alert>
	  ![](https://qcloudimg.tencent-cloud.cn/raw/9604f84907bd4154d96e2eeb0c9fe1e8.png)
 2. 单击**重置密码**，完成重置。如下图所示：
	  ![](https://qcloudimg.tencent-cloud.cn/raw/fe680e817ae643c1ce3b12a6b454f09d.png)
	  :::
	  </dx-tabs>



