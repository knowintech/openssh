# 如何在android上运行openssh



## 一、源码编译

这里只介绍在android源码中编译。

### 1. 拉取android源码

```bash
git clone xxxx
```

android源码的编译请见相关wiki.

### 2. 拉取openssh源码

```
git clone https://github.com/knowintech/openssh.git
```

* 注意：

  1. openssh源码的分支是android10-release

  2. openssh源码必须位于：

     ```bash
     ${android}/external/openssh
     ```

### 3. 编译openssh

```bash
mmm external/openssh
```

编译后的文件分为bin和libs:

* bin文件

  ```bash
  
  ```

* lib文件

  ```bash
  
  ```

### 4. 拷贝到android系统中

* 拷贝bin文件

  ```
  
  ```

* 拷贝lib文件

  ```
  
  ```

### 5. 在android文件系统中为ssh建立目录

```
mkdir /data/ssh
mkdir /data/ssh/empty
```



## 二、运行ssh-server



## 三、运行ssh-client

