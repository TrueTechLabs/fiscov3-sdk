#BCOS V3 SDK使用步骤
> 官方仓库：https://github.com/FISCO-BCOS/go-sdk
1. 按官方教程部署好BCOS
2. 安装go环境 ,gcc 
````bash
#下载二进制包
wget https://golang.google.cn/dl/go1.19.linux-amd64.tar.gz
#将下载的二进制包解压至 /usr/local目录
sudo tar -C /usr/local -xzf go1.19.linux-amd64.tar.gz
mkdir $HOME/go
#将以下内容添加至环境变量 ~/.bashrc
export GOPATH=$HOME/go
export GOROOT=/usr/local/go
export PATH=$GOROOT/bin:$PATH
#更新环境变量
source  ~/.bashrc 
#设置代理
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct

sudo apt install gcc
````
3. 克隆go-sdk到本地
git clone https://github.com/realcoooool/fiscov3-sdk

4. 安装bcos-c-sdk.so
./tools/download_csdk_lib.sh

5. 编译console控制台，拷贝证书到go-sdk目录，即证书与console在同一目录
go build cmd/console.go
cp ~/fisco/nodes/127.0.0.1/sdk/* .

6. 创建合约目录
# 该指令在go-sdk目录中执行
mkdir helloworld && cd helloworld
7. 安装solc编译器
# 该指令在helloworld文件夹中执行
bash ../tools/download_solc.sh -v 0.8.11

8. 构建abigen （用于将
# 该指令在helloworld文件夹中执行，编译生成abigen工具，该工具用于将abi和bin文件转换为go文件
go build ../cmd/abigen
9. 编译为go文件
./solc-0.8.11 --bin --abi -o ./ ./HelloWorld.sol
./abigen --bin ./HelloWorld.bin --abi ./HelloWorld.abi --pkg helloworld --type HelloWorld --out ./HelloWorld.go

10. 部署合约
go run helloworld/cmd/main.go

11. 异步部署、调用HelloWorld合约

go run helloworld/cmd/main.go
