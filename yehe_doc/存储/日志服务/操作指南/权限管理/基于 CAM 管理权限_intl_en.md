## Overview

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598) is a web-based Tencent Cloud service that helps you securely manage and control access to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (user groups), and control who can access and use your Tencent Cloud resources through identity and policy management. For more information about CAM policies and how to use them, see [Policy](https://cloud.tencent.com/document/product/598/10601).

A root account can grant a sub-account or collaborator access to specified CLS resources.

## Preset Access Policies

CLS offers two preset access policies to meet your basic access management demand.
- QcloudCLSFullAccess: access to all CLS resources and actions, including creating log topics, modifying index configuration, deleting log topics, searching for logs, uploading logs, etc.
- QcloudCLSReadOnlyAccess: only read access to CLS data; no CRUD access

For how to use the policies, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

## Custom Access Policies

You can use a custom access policy to grant access at a finer granularity, for example, to allow a specific user to view the data of a specific log topic.

A custom access policy consists of two parts:
- Action: the action a user is allowed to perform, such as searching for logs, modifying index configuration, uploading logs, and creating alarm policies
- Resource: the resources a user is allowed to operate on, such as a specific log topic, dashboard, data processing task

For the authorizable resource types and related APIs supported by CLS, see [Authorizable Resource Types](https://cloud.tencent.com/document/product/614/70091). For how to configure custom access policies, see [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596).

Configuring custom access policies can be a demanding process. The examples we offer in [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004) should meet most access management needs. You can also modify the examples based on your requirements.
1. Log in to the console with the root account (or an account with CAM access). On the [Policies](https://console.cloud.tencent.com/cam/policy) page, click **Create Custom Policy**.
2. In the pop-up window, click **Create by Policy Syntax**.
3. Select **Blank Template** and click **Next**.
4. Enter a policy name and policy content. For the latter, you can copy content from [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).
5. Click **Complete** to save the policy.
After creating a custom access policy, you can [associate](https://intl.cloud.tencent.com/document/product/598/10602) it with a user/user group to grant the user/user group the corresponding access.
