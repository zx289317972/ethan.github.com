# <center>ConfigMap</center>
## 简介
configmap（cm）是Kubernetes中的一个资源对象，用来存储键值对数据，往往是配置信息，可以理解为整个命名空间的/etc目录。

configmap可用于环境变量，命令行参数和挂载数据卷。值得一提的是，configmap还具备热更新的功能。

## 热更新实践
首先，创建一个测试的configmap 
```
# kubectl create -f test-cm.yml

apiVersion: v1
kind: ConfigMap
metadata:
  name: test
  namespace: default
data:
  a: "1"

# kubectl exec test -- env | grep a=
```
创建后，可以使用edit，apply或patch命令修改a的值：

```
kubectl patch cm test -p '{"data":{"a":"2"}}'
kubectl edit cm test
kubectl apply -f test.yaml
```
anyshare 示例
```
# kubectl get cm -A |grep mariadb
# kubectl get cm proton-mariadb-proton-rds-mariadb -n resource -o yaml
```
通过环境变量，命令行参数以及数据卷挂载这三种方式测试configmap的热更新效果。

```

```