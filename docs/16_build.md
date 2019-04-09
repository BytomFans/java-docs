---
id: build
title: Build Bytom
sidebar_label: 搭建节点
---

## 源码搭建



## ubuntu搭建

### 1.1 安装系统依赖库

    sudo apt-get update
    sudo apt-get install build-essential git unzip wget vim

### 1.2 下载并解压节点

    wget https://mirrors.tuna.tsinghua.edu.cn/osdn/bytom/70718/bytom-1.0.8-linux.zip
    unzip bytom-1.0.8-linux.zip
    chmod +777 ./bytomd

### 1.3 启动并运行节点

    ./bytomd init --chain_id mainnet
    ./bytomd node --simd.enable

## windows搭建

### 安装系统依赖库

#### 安装MinGW
官方链接：https://nuwen.net/mingw.html

下载链接：https://nuwen.net/files/mingw/mingw-16.1.exe

#### 安装Golang

官方地址：https://golang.org/

下载链接：https://studygolang.com/dl/golang/go1.12.windows-amd64.msi

#### 安装Git

官方地址：https://git-scm.com/

下载链接：https://git-scm.com/download/win

### 下载并解压节点

下载链接：https://mirrors.tuna.tsinghua.edu.cn/osdn/bytom/70718/bytom-1.0.8-linux.zip解压zip文件，并右键文件夹权限修改成可读写

### 启动并运行节点

    ./bytomd.exe init --chain_id mainnet
    ./bytomd.exe node --simd.enable

## docker搭建

### 获取Docker镜像

    docker pull bytom/bytom:latest

### 初始化节点

    docker run -v ~/Bytom:/root/.bytom bytom/bytom:latest bytomd init --chain_id mainnet

### 运行节点

    docker run -d -p 46657:46657 -v ~/Bytom:/root/.bytom bytom/bytom:latest 

## Mac搭建

使用HomeBrew安装比原链节点

    brew install bytom