# helm-quickstart

## Source

https://helm.sh/docs/intro/quickstart/



## 安装与准备

### 1. 安装K8s（忽略）

### 2. 安装helm（忽略）

### 3. 安装mysql

```shell
$ helm install stable/mysql --set persistence.enabled=false  --generate-name
```

 得到输出：

```
NAME: mysql-1591639340
LAST DEPLOYED: Tue Jun  9 02:02:24 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
MySQL can be accessed via port 3306 on the following DNS name from within your cluster:
mysql-1591639340.default.svc.cluster.local

To get your root password run:

MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace default mysql-1591639340 -o jsonpath="{.data.mysql-root-password}" | base64 --decode; echo)

To connect to your database:

1. Run an Ubuntu pod that you can use as a client:

   kubectl run -i --tty ubuntu --image=ubuntu:16.04 --restart=Never -- bash -il

2. Install the mysql client:

   $ apt-get update && apt-get install mysql-client -y

3. Connect using the mysql cli, then provide your password:
   $ mysql -h mysql-1591639340 -p

To connect to your database directly from outside the K8s cluster:
    MYSQL_HOST=127.0.0.1
    MYSQL_PORT=3306

# Execute the following command to route the connection:

kubectl port-forward svc/mysql-1591639340 3306

mysql -h ${MYSQL_HOST} -P${MYSQL_PORT} -u root -p${MYSQL_ROOT_PASSWORD}
```

### 4. 通过观察上面得到

```
NAME: mysql-1591639340
```

### 5. 获得加密的密码

```shell
kubectl get secret --namespace default mysql-1591639340 -o jsonpath="{.data.mysql-root-password}" 
```

### 6. 得到

```
 ZHNhV0FZeThOVg==
```



### 7. 打开网站

https://www.base64decode.net/

### 8. 转换得到

```
dsaWAYy8NV
```

到此安装与准备工作完成

==============================================

## 访问与使用

### 1. 通过k8s中的容器来访问

创建一个ubuntu实例

```shell
kubectl run -i --tty ubuntu --image=ubuntu:16.04 --restart=Never -- bash -il
```

在实例中安装mysql客户端

```shell
apt-get update && apt-get install mysql-client -y
```

链接数据库实例

```shell
mysql -h mysql-1591639340 -p    #然后粘贴上面的密码
```

执行sql命令

```mysql
show databases;
```

### 2. 在当前OS中访问

将远程数据库端口映射到本地端口

```shell
kubectl port-forward svc/mysql-1591639340 3306
```

### 3.在本地的WSL中执行:

```shell
export MYSQL_ROOT_PASSWORD=dsaWAYy8NV
export MYSQL_HOST=127.0.0.1
export MYSQL_PORT=3306
```

```shell
mysql -h ${MYSQL_HOST} -P${MYSQL_PORT} -u root -p${MYSQL_ROOT_PASSWORD}
```

