## Overview
After creating a command, you can execute it on one or more CVM or Lighthouse instances. The execution status and results on different instances are independent. This document describes how to execute the command on multiple CVM instances.

## Prerequisites
- The instances are in **Running** status.
- The TAT agent is installed on the target instance. See [Installing TAT Agent](https://intl.cloud.tencent.com/document/product/1147/46042).
- The target instance in based on a VPC.


## Directions

<dx-tabs>
::: Console
1. Log in to the CVM console and select [My Commands](https://console.cloud.tencent.com/cvm/command) under **TencentCloud Automation Tools** from the left sidebar.
2. In the **My commands** page, select the region, locate the target command and click **Execute**.
![](https://qcloudimg.tencent-cloud.cn/raw/932a05d66f77a105a0c17310ad9caba8.png)
3. In the **Execute command** page, modify the command configuration and select the target instances.
![](https://qcloudimg.tencent-cloud.cn/raw/4ce30ed74fa47b69a8474b26315bab56.png)
4. Click **Execute command**.

:::
::: API
You can call the `InvokeCommand` API to execute the command on multiple servers.
:::
</dx-tabs>

## Subsequent Operations
After the task execution, you can check the task result in **My commands - Logs - Log details**.
