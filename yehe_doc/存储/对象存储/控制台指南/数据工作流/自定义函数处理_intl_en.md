## Overview

If the existing services or features of COS media processing cannot meet your needs, you can use the custom function processing feature of SCF to write core code logic in order to flexibly implement your business needs while reducing your development costs. For more information on SCF, see [Overview](https://intl.cloud.tencent.com/document/product/583/9199).

>?
> - Currently, the custom function processing feature can only be initiated in a [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
> - Using SCF for custom processing will incur fees, which will be charged by SCF. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
> 

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to operate.
4. On the left sidebar, click **Data Processing Workflow** > **Workflow** to enter the workflow management page.
5. Click **Create Workflow** and add a **Custom Function** node during workflow configuration.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4b341e1e9a494368ebacaf9e3387022e.png" /></br>
The configuration items are described as follows:
 - Input Parameters: The input parameters specified with a custom function in a workflow don't need to be added manually. Instead, they can be obtained according to the node before the custom function.
 - Namespace: The created function is in the COS namespace by default.
 - Type: Select **Common feature** to quickly perform common operations on COS objects or **Custom** to configure other feature parameters.
 - Feature: When you select **Common feature**, you can select a preset feature as instructed in [Using Custom Function to Manage COS File].
 - Function: Currently, only functions that are executed asynchronously and have status tracking enabled are supported in a workflow.
 To create a function, click **Create Function** and configure the function as prompted.
6. After confirming that the configuration is correct, click **OK**.



