# Conda常用命令

#### Conda版本管理

```c
conda -version
conda -V
```

#### 获取帮助

```c
conda --help
conda -h
conda <命令> --help  //获取某一条命令的帮助
```

#### 环境管理

```c
conda env -h  //查看环境管理全部命令帮助
conda create -n <env_name>  //创建虚拟环境
conda create -n <env_name> python=<版本号> /*创建特定python版本                                              的环境*/
conda create -n <env_name> python=<版本号> <包名> /*创建特定                                      python版本以及特定包的环境*/
/*列出所有的环境*/
conda info --envs
conda env list

/*进入某个环境*/
activate <env_name>  //windows下命令
source activate      //linux以及MacOS下命令

/*退出当前环境*/
deactivate

/*克隆环境*/
conda create -n <new_env_name> --clone <old_env_name>

/*删除环境*/
conda remove -n <your_env_name> --all
```

#### 环境分享

如果你想把你当前的环境配置与别人分享，这样ta可以快速建立一个与你一模一样的环境（同一个版本的python及各种包）来共同开发/进行新的实验。一个分享环境的快速方法就是给ta一个你的环境的.yml文件。

首先通过`activate target_env`要分享的环境`target_env`，然后输入下面的命令会在当前工作目录下生成一个`environment.yml`文件

```c
conda env export > environment.yml
```

小伙伴拿到`environment.yml`文件后，将该文件放在工作目录下，可以通过以下命令从该文件创建环境

```c
conda env create -f environment.yml
```

#### 包管理

```c
conda list //列举当前活跃环境下的所有包
conda list -n <env_name> //列举一个非当前活跃环境下的所有包
conda install -n <env_name> <package_name> /*为指定环境安装
                                             某个包*/
conda remove -n <env_name> <package> //从某个环境卸载包
conda install <package>=<package_version> //安装特定版本的包
```

#### Conda配置

```c
conda config --add channels <URL> //添加源
conda config --set show_channel_urls yes //设置搜索时显示通道地址
conda config --show-sources  //查看当前使用源
conda config --remove channels <URL> //删除指定源
```

