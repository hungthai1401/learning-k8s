```shell
kubectl create -f ku-rc.yml
```

```shell
kubectl label pod ku-rc-8g8w7 app=foo --overwrite
```

### metalb

https://metallb.universe.tf/

```shell
kubectl create -f ku-ip-pool.yml
kubectl create -f ku-svc-loadbalancer.yml
kubectl create -f ku-rc-readiness-probe.yml
...
kubectl exec <POD_NAME> -- touch /var/ready
```

```shell
kubectl scale rc ku-rc --replicas=3
```

```shell
kubectl create -f ku-rs.yml
kubectl create -f ku-rs-expression.yml
```

```shell
kubectl create -f ku-ds.yml
# Attach label disk=ssd to node-1
kubectl label node node-1 disk=ssd
# Detach label disk from node-1
kubectl label node node-1 disk-
```

```shell
kubectl create -f ku-job.yml
kubectl create -f ku-multi-completion-job.yml
kubectl create -f ku-multi-completion-parallel-job.yml
kubectl create -f ku-time-limited-job.yml
```
