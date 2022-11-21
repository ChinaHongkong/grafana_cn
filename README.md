grafana 汉化
切到version-cn分支,例如9.2.5 切换到9.2.5-cn分支，不带cn的为官方release-version分支的代码

go
1. 查看go.mod安装版本,设置阿里源 export GOPROXY=https://mirrors.aliyun.com/goproxy/   如果不能用设置下dns
2. gopath新版本不需要设置,只需要goroot
3. linux安装gcc和make
4. make gen-go 
5. go run build.go setup
6. go run build.go build
7. 生成bin/linux-amd64/grafana-*文件，拷贝到bin下，运行grafana-server

node
1. 设置淘宝镜像export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node/ 和export NVM_IOJS_ORG_MIRROR=http://npm.taobao.org/mirrors/iojs
2. yarn CYPRESS 这个组件下载很慢加入环境变量 export CYPRESS_DOWNLOAD_MIRROR=https://download.cypress.io 如果不行 export CYPRESS_INSTALL_BINARY=https://registry.npmmirror.com/-/binary/cypress/9.5.1/linux-x64/cypress.zip 根据版本号写死路径
3. 打包对内存有要求4GB不够，最好8GB 加入环境变量export NODE_OPTIONS="--max-old-space-size=8192"
4. yarn
5. yarn build
6. 打包会生成public/build         还有public/view里的一些文件

打包rpm
先编译前端
再编译后端把编译后的文件放到bin目录下
安装nfpm版本2.22.1
mkdir dist
nfpm pkg --packager rpm --config packaging/conf/nfpm_rpm.yaml --target dist/
在dist目录生成相应的rpm文件
通过yum install  rpm文件名   安装
