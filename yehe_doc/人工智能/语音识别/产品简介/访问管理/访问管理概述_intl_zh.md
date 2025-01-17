如果您在腾讯云中使用到了语音识别（ASR）服务里面的各种操作，这些操作可能由不同的人分类使用，但都共享您的云账号密钥，将存在以下问题：

- 您的密钥由多人共享，泄密风险高；
- 您无法限制其它人的访问权限，易产生误操作造成安全风险。

这个时候，您就可以通过子帐号实现不同的人管理不同的服务，以避免以上的问题。默认情况下，子帐号没有使用 ASR 的权利或者相关资源的权限。因此，我们就需要创建策略来允许子帐号使用他们所需要的资源或者权限。

访问管理（CAM，Cloud Access Management）是腾讯云提供的一套 Web 服务，它主要用于帮助客户安全管理腾讯云账户下的资源的访问权限。通过 CAM，您可以创建、管理和销毁用户(组)，并通过身份管理和策略管理控制哪些人可以使用哪些腾讯云资源。

当您使用 CAM 的时候，可以将策略与一个用户或者一组用户关联起来，策略能够授权或者拒绝用户使用指定资源完成指定任务。有关 CAM 策略的更多相关基本信息，请参照 [策略语法](https://intl.cloud.tencent.com/document/product/598/10603)。有关 CAM 策略的更多相关使用信息，请参照 [策略](https://intl.cloud.tencent.com/document/product/598/10601)。

如果您不需要对子账户进行 ASR 相关资源的访问管理，您可以跳过此章节。跳过这些部分并不影响您对文档中其余部分的理解和使用。

## 入门
CAM 策略必须授权使用一个或多个 ASR 操作或者必须拒绝使用一个或多个 ASR 操作。同时还必须指定可以用于操作的资源（可以是全部资源，某些操作也可以是部分资源），策略还可以包含操作资源所设置的条件。

ASR 部分 API 是接口级权限，对于该类 API 操作，您不需要指定授权某些资源；部分 API 是资源级权限，对于该类 API 操作，您可以指定授权某些资源。

<table>
<tr>
<th>了解策略基本结构</th>
<th><a href="https://intl.cloud.tencent.com/document/product/1118/43351">策略语法</a></th>
</tr>
<tr>
<td>在策略中定义操作</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1118/43351">ASR 的操作</a></td>
</tr>
<tr>
<td>在策略中定义资源</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1118/43351">ASR 的资源路径</a></td>
</tr>
<tr>
<td>ASR 的授权粒度</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1118/43350">ASR 支持的资源级权限</a></td>
</tr>
</table>

