# istio+Kubernetes

## 环境准备
- 硬件资源充足
- Kubernetes 1.9.1+
- docker 1.12+
- istioctl 0.7.1
- git

## 安装Kubernetes
忽略

## 安装 Istio
 从项目中获取安装YAML文件
 ``` bash
 git clone https://github.com/liyanyanli/example-istio.git
 ```
 安装 Istio
 ``` bash
 cd example-istio
 kubectl apply -f istio
 ```
 安装 istioctl
 ``` bash
 cp bin/istioctl /usr/bin/istioctl
 ```
 