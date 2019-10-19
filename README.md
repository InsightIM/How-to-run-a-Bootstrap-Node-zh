# 如何运行自己的引导节点

### 在服务器控制台按照以下步骤执行即可运行自己的引导节点


* 创建data目录并进入data目录
```sh
mkdir /data && cd /data/
```

* 安装依赖库
```sh
sudo yum -y install build-essential libtool autotools-dev automake checkinstall check git yasm
```

* 编译安装依赖库 libsodium
```sh
git clone https://github.com/jedisct1/libsodium.git
```

```sh
cd libsodium && git checkout tags/1.0.3
```

```sh
./autogen.sh && ./configure && make check && sudo make install
```

* 编译安装依赖库 toxcore
```sh
cd /data && git clone https://github.com/irungentoo/toxcore.git
```

```sh
cd toxcore && autoreconf -i && ./configure && make && sudo make install
```

* 进入bootstrap_daemon目录
```sh
cd other/bootstrap_daemon/
```

* 添加Tok用户
```sh
sudo useradd --home-dir /var/lib/tox-bootstrapd --create-home --system --shell /sbin/nologin --comment "Account to run Tox's DHT bootstrap daemon" --user-group tox-bootstrapd
```

* 添加指定目录访问权限
```sh
sudo chmod 700 /var/lib/tox-bootstrapd
```

* 复制tox-bootstrapd配置文件
```sh
sudo cp tox-bootstrapd.conf /etc/tox-bootstrapd.conf
```

* 运行Tok引导节点程序
```sh
cd /usr/local/bin/ && nohup ./DHT_bootstrap --config /etc/tox-bootstrapd.conf &
```

###完成！记录引导节点信息：IP、Port、Public Key
