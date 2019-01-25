+++
showonlyimage = false
draft = false
image = "img/portfolio/mac.png"
date = "2016-11-05T19:59:22+05:30"
title = "Mac 使用技巧"
writer = "子适"
categories = [ "code" ]
weight = 8
+++

## 快捷键
<!--more-->
- 访达
  - **Shift-Command-C**：打开“电脑”窗口。
  - **Shift-Command-D**：打开“桌面”文件夹。
  - **Shift-Command-F**：打开“最近使用”窗口，其中显示了您最近查看或更改过的所有文件。
  - **Shift-Command-G**：打开“前往文件夹”窗口。
  - **Shift-Command-H**：打开当前 macOS 用户帐户的个人文件夹。
  - **Shift-Command-N：**新建文件夹。


## 环境变量

- 环境变量优先级

  ```
  /etc/profile
  /etc/paths 
  ~/.bash_profile 
  ~/.bash_login 
  ~/.profile ~/.bashrc
  ```

- 说明

  - /etc/profile （建议不修改这个文件 ） 全局（公有）配置，不管是哪个用户，登录时都会读取该文件。
  - /etc/bashrc （一般在这个文件中添加系统级环境变量） 全局（公有）配置，bash shell执行时，不管是何种方式，都会读取此文件。
  - ~/.bash_profile （一般在这个文件中添加用户级环境变量） 每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!

- 查看环境变量

```
	echo $PATH
```

- 两种修改方法：

  - 添加，但重启终端后会失效（不知为何）

  ```
  #中间用冒号隔开
  export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N>
  # 例如
  export PATH=/usr/local/mongodb/bin:$PATH
  
  ```

  - 直接编辑环境变量文件

  ```
  vim ~/.bash_profile
  # 编辑文件（i），将export PATH=/usr/local/mongodb/bin:$PATH加入到文件中
  # esc 退出编辑，:wq 保存退出
  # 更新环境变量
  source ~/.bash_profile
  ```



