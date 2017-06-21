---
title: ssh免密码登录和传输
date: 2017-05-19 17:25:19
categories: Technology
tags: [linux,ssh,tool,scp]
comments: true

---

## Why

玩linux的，都会遇到需要操作一大堆serve时，要切换不同身份，端口和密码去分别登录，烦人的很，其实ssh提供了一种基于非对称加密的方法实现免密码登录

## How

假定需要从A传输文件或登录到B，执行以下步骤

### Step 1

在A机器上生成的ssh public-private keys，如果已经生成过了，可忽略这一步
```
ssh-keygen -t rsa
```
就会在~/.ssh/目录下生成一个id_rsa (private key) and id_ras.pub (public key)

### Step 2

在A机器上配置~/.ssh/config文件,add below content
```
Host fire
    HostName 115.159.114.116
    Port 22
    User ubuntu
    IdentityFile ~/.ssh/id_rsa
```
Note:
- 'Port' field default to 22,
- 'User' default to the current account name on machine A
- 'IdentityFile' is the private key you want to user on machine A, aka the private key file you generated in step 1

Please modify them if necessary 

### Step 3

在机器B上，添加机器A的public key的完成内容到 ~/.ssh/authorized_keys，create the file if not not exist
可以添加多个哦

添加完成后，就可以在A上免密ssh到B了
```
ssh fire
scp ./xxx fire:~/
``` 

## Reference
[Simplify Your Life With an SSH Config File
](http://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/)


