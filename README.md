# crack-elasticsearch-by-docker

Crack elasticsearch 7.x / 8.x by docker

适用于破解elasticsearch 7.x / 8.x的自动脚本

已测试版本
* elasticsearch 8.2.0
* elasticsearch 8.5.0
* elasticsearch 8.7.0
* elasticsearch 8.9.1



# 注意事项

JDK版本，必须与ES使用的版本完全一致，即使是小版本。
curl拉取github文件，网络不好会导致失败，建议全局代理。

## Usage

Get srcipt

获取脚本源码

```shell
git clone https://github.com/wolfbolin/crack-elasticsearch-by-docker.git
```

Run srcipt with version

运行脚本并指定完整版本（예: 8.9.1)

```shell
cd crack-elasticsearch-by-docker
version=8.9.1
bash crack.sh $version
```

Get cracked x-pack-core-$version.jar

编译产物和编译中间件保存在output文件夹中

```shell
cp output/x-pack-core-$version.crack.jar x-pack-core-$version.jar
```
### 覆盖路径

RPM包安装默认路径

```shell
/usr/share/elasticsearch/modules/x-pack-core/

```



## Others
You can change `crack.sh` shell with http_proxy / https_proxy url

你可以修改`crack.sh`以使用代理访问网络，避免网络访问故障

```shell
docker build --no-cache -f Dockerfile \
  --build-arg VERSION="${version}" \
  --build-arg HTTP_PROXY="http://1.2.3.4:8080" \
  --build-arg HTTPS_PROXY="http://1.2.3.4:8080" \
  --tag ${service_name}:${version} .

docker run -it --rm \
  -v $(pwd)/output:/crack/output \
  -e HTTP_PROXY="http://1.2.3.4:8080" \
  -e HTTPS_PROXY="http://1.2.3.4:8080" \
  ${service_name}:${version}
```


