## prometheus
prometheus监控平台

## 命名空间
`执行namespace.yaml文件`
```
kubectl create -f namespace.yaml
```
## 部署服务
`行每个目录里面的yaml文件`
```
kubectl create -f ./kube-state-metrics
kubectl create -f ./node-exporter
kubectl create -f ./k8s
kubectl create -f ./blackbox-exporter
kubectl create -f ./alertmanager
kubectl create -f ./dingtalk
kubectl create -f ./prometheus
kubectl create -f ./grafana
```

## 查看执行结果
`查看pod`
>[root@k8s-master ~]# kubectl get pod -n monitoring 
```
NAME                                  READY   STATUS    RESTARTS   AGE
alertmanager-7ff5dbf7fc-5b2b7         1/1     Running   0          6d4h
blackbox-exporter-7d567fbcd-cb5n7     1/1     Running   1          12d
dingtalk-754c898575-swmmh             1/1     Running   0          6d4h
grafana-b7954c6f7-jxc6g               1/1     Running   0          6d4h
kube-state-metrics-7b9689c648-jzqc5   1/1     Running   1          12d
node-exporter-hrzd5                   1/1     Running   1          12d
prometheus-67dcb69b5f-22q5c           1/1     Running   1          6d5h
```
`查看config`
>[root@k8s-master ~]# kubectl get configmaps -n monitoring 
```
NAME                     DATA   AGE
alertmanager-config      1      6d5h
alertmanager-templates   2      6d5h
blackbox-exporter        1      12d
dingtalk-config          1      6d4h
prometheus-config        1      6d5h
prometheus-rules         1      6d5h
```
`查看pvc`
>[root@k8s-master ~]# kubectl get pvc -n monitoring 
```
NAME           STATUS   VOLUME         CAPACITY   ACCESS MODES   STORAGECLASS   AGE
alertmanager   Bound    alertmanager   5Gi        RWO                           6d5h
grafana        Bound    grafana        5Gi        RWO                           6d4h
prometheus     Bound    prometheus     5Gi        RWO                           6d5h
```
`查看service`
>[root@k8s-master ~]# kubectl get service -n monitoring 
```
NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
alertmanager         ClusterIP   10.101.249.116   <none>        9093/TCP         6d5h
blackbox-exporter    NodePort    10.105.110.34    <none>        9115:30115/TCP   12d
dingtalk             ClusterIP   10.96.45.168     <none>        8060/TCP         6d4h
grafana              ClusterIP   10.108.90.112    <none>        3000/TCP         6d4h
kube-state-metrics   ClusterIP   10.108.60.247    <none>        8080/TCP         12d
node-exporter        ClusterIP   None             <none>        9100/TCP         12d
prometheus           ClusterIP   10.97.119.131    <none>        9090/TCP         6d5h
```
`查看ingress`
>[root@k8s-master ~]# kubectl get ingress -n monitoring 
```
NAME            CLASS    HOSTS                      ADDRESS       PORTS   AGE
alertmanager    <none>   alertmanager.liangzy.com   10.99.99.42   80      6d5h
grafana         <none>   grafana.liangzy.com        10.99.99.42   80      6d4h
node-exporter   <none>   node115.liangzy.com        10.99.99.42   80      6d5h
prometheus      <none>   prometheus.liangzy.com     10.99.99.42   80      6d5h
```
