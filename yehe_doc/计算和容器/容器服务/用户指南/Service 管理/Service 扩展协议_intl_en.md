## Protocols Supported by Services by Default

 A Service is a mechanism and abstraction through which Kubernetes exposes applications outside the cluster. You can access the applications in a cluster through a Service.


<dx-alert infotype="notice" title="">
- For access in [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837), there are no restrictions on the use of extension protocols, and TCP and UDP protocols can be used together.
- In non-direct access scenarios, `ClusterIP` and `NodePort` modes can be used together. However, the community has restrictions on Services of the `LoadBalance` type, and only protocols of the same type can be used currently.
- When `LoadBalance` is declared as TCP, the port can use the capabilities of extension protocols to change the protocol of CLB to TCP_SSL, HTTP, or HTTPS.
- When `LoadBalance` is declared as UDP, the port can use the capabilities of extension protocols to change the protocol of CLB to UDP or QUIC.
</dx-alert>



## TKE Extension of Service Forwarding Protocols

In addition to the rules of the protocols supported by a native Service, a Service needs to support the mix use of TCP and UDP as well as the TCP SSL, HTTP, and HTTPS protocols in certain scenarios. TKE extends the support for more protocols in `LoadBalancer` mode.



### Prerequisites

- Extension protocols are only effective for Services in `LoadBalancer` mode.
- An extension protocol describes the relationship between the protocol and the port through an annotation.
- The relationship between the extension protocol and the annotation is as follows:
   - When the port described in `Service Spec` is not covered in the annotation of the extension protocol, `Service Spec` will be configured according to your declaration.
   - When the port described in the annotation of the extension protocol does not exist in `Service Spec`, the configuration will be ignored.
   - When the port described in the annotation of the extension protocol exists in `Service Spec`, the protocol configuration declared in `Service Spec` will be overwritten.



### Annotation name
`service.cloud.tencent.com/specify-protocol`

### Sample annotations of extension protocols

<dx-tabs>
::: Sample for TCP_SSL
<dx-codeblock>
::: xml 
{"80":{"protocol":["TCP_SSL"],"tls":"cert-secret"}}
:::
</dx-codeblock>
:::
::: Sample for HTTP
<dx-codeblock>
::: xml 
{"80":{"protocol":["HTTP"],"hosts":{"a.tencent.com":{},"b.tencent.com":{}}}}
:::
</dx-codeblock>
:::
::: Sample for HTTPS
<dx-codeblock>
::: xml 
 {"80":{"protocol":["HTTPS"],"hosts":{"a.tencent.com":{"tls":"cert-secret-a"},"b.tencent.com":{"tls":"cert-secret-b"}}}}
:::
</dx-codeblock>
:::
::: Sample for TCP/UDP
<dx-codeblock>
::: xml 
{"80":{"protocol":["TCP","UDP"]}} # Only supported in [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837)
:::
</dx-codeblock>
:::
::: Sample for mix use
<dx-codeblock>
::: xml 
 {"80":{"protocol":["TCP_SSL","UDP"],"tls":"cert-secret"}} # Only supported in [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837)
:::
</dx-codeblock>
:::
</dx-tabs>




### Extension protocol use instructions
<dx-tabs>
::: Use instructions of extension protocol `YAML`
```yaml
apiVersion: v1
kind: Service
metadata:
    annotations:  
      service.cloud.tencent.com/specify-protocol: '{"80":{"protocol":["TCP_SSL"],"tls":"cert-secret"}}' # To use other protocols, change the value in the key-value pair to the above content
    name: test
   ....
```
:::
::: Use instructions of extension protocols in the console
- If you expose a Service in the form of "**public network CLB**" or "**private network CLB**" when creating it, in modes other than [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837), only TCP and TCP SSL can be used together in **Port Mapping** as shown below:
![](https://main.qcloudimg.com/raw/1f9ff7c6ebcffd2cfb35404f9d1f728e.png)

- When the Service is in "**ClusterIP**" or "**NodeBalance**" mode, any protocols can be used together.

- In [direct access mode](https://intl.cloud.tencent.com/document/product/457/36837), any protocols can be used together.
:::
</dx-tabs>



