# minieap的Openwrt Makefile
**需配合SDK使用，具备一定的Linux操作能力与交叉编译知识**  
~~_LUCI界面在做了在做了_~~

## 这个Makefile干了什么？
1. 拉取[minieap][1]的源码
2. 切换到PKG_VERSION指定的Tag
3. 用sed替换ICONV为GBCONV
4. make

## 配合SDK使用方法
1. 下载路由器对应OpenWRT版本的SDK
2. 进入SDK目录，执行命令获取Makefile
```shell
git clone https://github.com/BoringCat/minieap-openwrt.git package/minieap
```
3. 执行make命令
```shell
# 多线程编译
make defconfig
make package/minieap/compile -j$(grep processor /proc/cpuinfo | wc -l)
```
（上下二选一）
```shell
# 显示详情
make defconfig
make package/minieap/compile V=s
```
4. 找到ipk文件
```shell
find -name '*minieap*.ipk' -type f
```
5. 将ipk文件拷贝到路由器中，执行opkg安装

## 配合 toolchain 使用方法（需要交叉编译基础）
1. 找到toolchain的bin目录，设好PATH变量
2. 执行 `git clone https://github.com/updateing/minieap.git` 下载minieap源码
3. 进入minieap目录，根据项目[README文件][2]配置config.mk文件  
   - 注意！需配置CC := $(toolchain的gcc)
4. 将编译出来的minieap可执行文件拷贝到路由器上

## 认证方法
请参考[官方文档][2]和程序帮助`minieap -h`

### GCP
直接自己装个luci-app-minieap自己认证就行


[1]: https://github.com/updateing/minieap
[2]: https://github.com/updateing/minieap/blob/master/README.md
