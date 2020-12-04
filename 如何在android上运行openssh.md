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
  uyang@u19:~/android$ ls -l out/target/product/generic/system/bin
  total 512
  -rwxrwxr-x 1 ouyang ouyang  37328 12月  2 17:28 scp
  -rwxrwxr-x 1 ouyang ouyang  62668 12月  2 17:28 sftp
  -rwxrwxr-x 1 ouyang ouyang 162508 12月  2 17:28 ssh
  -rwxrwxr-x 1 ouyang ouyang 190452 12月  2 17:28 sshd
  -rwxrwxr-x 1 ouyang ouyang  53764 12月  2 17:28 ssh-keygen
  -rwxrwxr-x 1 ouyang ouyang    998 12月  2 17:28 start-ssh
  ```

* lib文件

  ```bash
  ouyang@u19:~/android$ ls -l out/target/product/generic/system/lib/
  total 3520
  -rwxrwxr-x 1 ouyang ouyang   5408 12月  2 13:45 ld-android.so
  -rwxrwxr-x 1 ouyang ouyang 906448 12月  2 13:45 libcrypto.so
  -rwxrwxr-x 1 ouyang ouyang 636324 12月  2 13:45 libc++.so
  -rwxrwxr-x 1 ouyang ouyang 841896 12月  2 13:45 libc.so
  -rwxrwxr-x 1 ouyang ouyang  67468 12月  2 13:45 libcutils.so
  -rwxrwxr-x 1 ouyang ouyang   5940 12月  2 13:45 libdl.so
  -rwxrwxr-x 1 ouyang ouyang  89004 12月  2 13:45 liblog.so
  -rwxrwxr-x 1 ouyang ouyang 136680 12月  2 13:45 libm.so
  -rwxrwxr-x 1 ouyang ouyang 527288 12月  2 17:28 libssh.so
  -rwxrwxr-x 1 ouyang ouyang 261384 12月  2 13:45 libssl.so
  -rwxrwxr-x 1 ouyang ouyang 106440 12月  2 13:45 libz.so
  ```

### 4. 拷贝到android系统中

* 拷贝bin文件

  ```
  adb push out/target/product/generic/symbols/system/bin/* /system/bin/
  ```

* 拷贝lib文件

  ```bash
  adb push out/target/product/generic/symbols/system/lib/* /system/lib/
  ```

### 5. 在android文件系统中为ssh建立目录

```bash
mkdir /data/ssh
mkdir /data/ssh/empty
```

## 二、运行ssh-server

### 1. 运行sshd

```bash
start-ssh
```

### 2. 使用ssh证书验证客户端

* 创建验证文件

  ```bash
  vi /data/ssh/authorized_keys
  ```

* 将ssh客户端的公钥添加到authorized_keys中，如：

  ```bash
  is:/data/ssh # cat authorized_keys
  ssh-rsa xxxxxxxxxxxxxxxxxxxxxxxxxxxxx ouyang@ubuntu
  ```
  ### 3. 使用ssh密码验证客户端
  
  ## 三、运行ssh-client
  
  ### 1. 使用证书验证
  
  ### 2. 使用密码验证
  
