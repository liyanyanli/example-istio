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
流量管理：将“reviews”服务100％的传入流量发送到“v1”版本
``` yaml
apiVersion: config.istio.io/v1alpha2
kind: RouteRule
metadata:
  name: reviews-default
spec:
  destination:
    name: reviews
  route:
  - labels:
      version: v1
    weight: 100
```



