# Istio + Kubernetes

## 环境准备
- 硬件资源充足
- Kubernetes 1.9.1+
- docker 1.12+
- istioctl 0.7.1
- git

## 安装 Kubernetes
忽略

## 安装 Istio
 从项目中获取安装YAML文件
 ``` bash
 git clone https://github.com/liyanyanli/example-istio.git
 ```
 安装 Istio （其中包含prometheus、zipkin、servicegraph等组件，可根据集群情况通过nodeport，ingress等方式提供外部访问）
 ``` bash
 cd example-istio
 kubectl apply -f istio
 ```
 安装 Istioctl
 ``` bash
 cp bin/istioctl /usr/bin/istioctl
 ```
 运行示例应用bookinfo
 ``` bash
 kubectl apply -n default -f <(istioctl kube-inject -f example/bookinfo/bookinfo.yaml)
 ```

## Istio 规则配置
**以下例子均以bookinfo为测试应用**

Bookinfo应用程序分为四个独立的微服务：
- productpage：productpage microservice调用详细信息并查看微服务来填充页面
- details：细节微服务包含书籍信息
- reviews：评论microservice包含书评。它也称为评级微服务
- ratings：评级微服务包含伴随书评的书籍排名信息

有3个版本的reviews：
- 版本v1不会调用评分服务
- 版本v2调用评分服务，并将每个评分显示为1至5个黑星
- 版本v3调用评分服务，并将每个评分显示为1到5个红色星星

![Bookinfo](./image/withistio.svg)

**流量管理**：将“reviews”服务100％的传入流量发送到“v1”版本
配置前：

``` bash
istioctl create -f example/policy/RouteRule.yaml
```
配置后：

**更多规则配置例子见 /example/policy/kube**



