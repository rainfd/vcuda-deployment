# vcuda deployment

link: https://github.com/tkestack/gpu-manager

vcuda 部署文件

对比官方的部署，这里额外部署了一个kube-scheduler。这是为了将gpu和正常服务调度分开，防止异常影响到普通业务。
pod需要额外加上 `schedulerName: gpu-scheduler` 来选择添加的调度器。

gpu-scheduler 权限绑定的是我本地默认kube-scheduler的角色，如果不一样就要对应修改。



## test

```bash
kubectl exec -it `kubectl get pods -o name | cut -d '/' -f2` -- bash
# a. Mnist
cd /data/tensorflow/mnist && time python convolutional.py
# b. AlexNet
cd /data/tensorflow/alexnet && time python alexnet_benchmark.py
# c. Cifar10
cd /data/tensorflow/cifar10 && time python cifar10_train.py
```