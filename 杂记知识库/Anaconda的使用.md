---
文章名称: Anaconda的使用
作者: DC_DC
关键字:
  - Anaconda
tags:
  - Editing
创建时间: 2024-04-21 21:41
修改时间: 2024-04-21 21:46
---
> 文章前言：
> - Anaconda的入门到入坑

# 基础操作

## 创建和管理环境

创建环境

```
conda create --name env
```

指定python版本创建环境

```
conda create --name env [python=3.8]  #推荐用法
```

删除环境

```
conda remove --name env --all  # 必须加上--all
```

激活环境

```
activate env
```

退出环境

```
conda deactivate env
```

列出所有环境

```
conda env list
```

## 安装和管理包

安装包

```
conda install package_name [=1.0]
```

卸载包

```
conda remove package_name
```

更新包

```
conda update package_name
```

查看已安装的包

```
conda list
```
---
# 打包操作

## 轻量级打包

导出环境配置

```
conda env export > [path] environment.yml
```

根据环境配置创建环境

```
conda env create -f [path] environment.yml
```

## 重量级打包

使用`conda-pack`

安装这个包

```
conda install [-c conda-forge] conda-pack  # 可选参数指定频道(推荐)，否则使用默认频道
```

打包环境

```
conda pack -n env [-o /path/env.tar.gz]  # 如果使用路径，必须遵守文件后缀
```

解包和使用环境

```
tar -xzf env.tar.gz -C env
```

激活环境

```
Linux   -> source env/bin/activate
Windows -> .\\env\\Scripts\\activate
```

修复硬编码的路径

```
conda-unpack
```
---
# 其他操作

查看conda版本

```
conda --version
```

更新conda

```
conda update conda
```

如果存在包冲突，有以下办法

1. 读取错误信息
    
2. 尝试手动指定某些包的版本来解决冲突
    
3. 尝试更新所有包到最新版本，可能会自行解决版本冲突
    
    ```
    conda update --all
    ```
    
---
# 问题总结

> pycharm无法直接添加conda环境，只能选择本地解释器，然后选择虚拟环境下的Python解释器

- 解决
    - [x] pycharm的版本问题，现在更新版本为

---

> 使用命令行创建环境后，但是此环境下没有Python解释器，无法正常为项目配置解释器

- 解决
    1. 如果使用 `conda create —name env` 这个命令不指定python版本创建anaconda虚拟环境，那此环境为空
    2. 推荐使用`conda create --name env [python=x.x]` 这个命令创建anaconda虚拟环境，可以避免上述问题
    3. 如果已经创建了一个空的虚拟环境，那么可以激活这个环境，再次安装python`conda install python=x.x`

---

> 使用conda创建虚拟环境，更改默认安装位置

- 解决
    1. 我期望安装在D盘的Anaconda目录下的envs中，但是默认的是C盘.conda目录中
    2. `conda info` 查看默认安装位置
        - 图片
            
            > [https://img-cdn.akass.cn/42/2024/03/65fbcdf4452a1.png!wp](https://img-cdn.akass.cn/42/2024/03/65fbcdf4452a1.png!wp)
            
    3. `conda config --add envs_dirs D:\\SoftWares\\Anaconda\\envs` 修改默认安装位置
    4. 接着创建虚拟环境，发现还是安装在了C盘，此时需要去修改D盘下envs这个目录的权限，改为完全控制
        - 图片
            
            > [https://img-cdn.akass.cn/42/2024/03/65fbcdf43a947.png!wp](https://img-cdn.akass.cn/42/2024/03/65fbcdf43a947.png!wp)
            

> 如果某些包无法从过conda install 命令安装，显示无法找到这个包，此时可以通过pip 在虚拟环境下安装

- 图片
    
    [https://img-cdn.akass.cn/42/2024/04/66233df44500b.png!wp](https://img-cdn.akass.cn/42/2024/04/66233df44500b.png!wp)
    

---