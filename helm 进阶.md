### 1. 登录免费 Kubernetes 资源

登录以下网址
https://www.katacoda.com/courses/kubernetes/guestbook

认证后，点击 ***START SCENARIO*** 按钮

### 2. 安装 helm 3

Helm3 不需要安装tiller，下载到 Helm 二进制文件直接解压到 $PATH 下就可以使用了。

```
# cd /opt && wget https://get.helm.sh/helm-v3.1.0-linux-amd64.tar.gz
# tar -xvf helm-v3.1.0-linux-amd64.tar.gz
# mv linux-amd64/helm /usr/local/bin/

# helm version
```

#### 2.1  helm 快速命令补全

```
# apt install -y bash-completion 
# source /usr/share/bash-completion/bash_completion 
# source <(helm completion bash) 
# echo "source <(helm completion bash)" >> ~/.bashrc
```

### 3. 利用 helm3 安装 harbor

```
# helm repo add goharbor https://helm.goharbor.io

# helm pull goharbor/harbor

# tar -zxvf harbor-1.3.1.tgz

# cd harbor

# tree .

# vi values.yaml

# /persistence

找到 ***persistence.enabled*** 字段，将值改为 ***false***

# / expose

找到 ***expose.type*** 字段，将值改为 ***nodePort***

找到 ***expose.tls.enabled*** 字段，将值改为 ***false***

# / externalURL

找到 ***externalURL*** 字段，将值改为 ***http://127.0.0.1:30002***

配置修改完只有，保存。

# helm install barbor .
```

### 4. 访问 harbor

点击页面上的 ***Guestbook***

在端口输入框中输入 ***30002***，然后点击 ***Display Port*** 按钮

出现 harbor 登录页面, harbor 的默认账号密码是 admin/Harbor12345

### 5. 推 chart 到 harbor

先下载一个chart包，待用

```
# helm repo add google  https://kubernetes-charts.storage.googleapis.com
# helm repo add stable https://kubernetes.oss-cn-hangzhou.aliyuncs.com/charts
# helm pull stable/nginx-ingress
```

在 ***项目*** 栏中点击 ***新建项目*** 按钮，新建一个chart repo，起名为 ***chart_repo***

添加 repo 到 helm 中

```
# helm repo add test http://127.0.0.1:30002/chartrepo/chart_repo
```

安装使用 helm-push 插件

```
# helm plugin install https://github.com/chartmuseum/helm-push
```

推送 chart 到 harbor 中

```
# helm push nginx-ingress-0.9.5.tgz test --username admin --password Harbor12345
```

当出现以下提示时，说明推送正常

```
Pushing nginx-ingress-0.9.5.tgz to test...
Done.
```

点击 harbor 页面的中 ***chart_repo*** 项目链接，可以查看到相关信息。 
