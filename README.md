# 利用 github page 存储 helm 3 chart 

1. 通过配置一个项目来为特定页面分支提供静态网页服务

  通过网络浏览器使用Github存储库上的分支按钮，新建 ***gh-pages*** 分支。

  接下来，确保gh-pages分支设置为Github Pages，点击 ***Settings*** 并向下滚动到Github页面部分。
  
  默认情况下，Source通常被设置为gh-pages分支。 如果这不是默认设置，那么选择它。
  
  并检查是否勾选了强制HTTPS，以便在提供图表时使用HTTPS。
  
2. 新建 ***index.yaml*** 文件，在文件中填入以下内容：

```yaml
apiVersion: v1
entries: {}
generated: "2020-02-22T07:10:59.249370366Z"
```

3. 在helm 3上敲入命令，测试是否成功，例如：

```shell
helm repo add gh-page https://www.y2p.cc/helm3-harbor
```
