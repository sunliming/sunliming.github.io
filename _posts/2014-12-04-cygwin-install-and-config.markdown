---
layout: post
title:  "基于Cygwin的git环境配置步骤"
date:   2014-12-04 11:19:00
categories: git
---
## 1.下载安装cygwin

软件下载链接: [cygwin install][cygwin-install],建议安装32-bit版.

在选择安装包时, 搜索框中输入"git", 通过鼠标单击将"Devel"子树整个改为"install"; 同样,对"openssh"的"network"子树、“vim”的“Editor”子树、“chere”的全部子树都改为"install".

## 2.配置cygwin

# 2.1.让cygwin可以正确输入中文

编辑C:\cygwin\home\你的用户名\.inputrc文件，将 “set completion-ignore-case on” 前面的#去掉

# 2.2.编辑C:\cygwin\cygwin.bat

在开头加入一行:
set HOME=

# 2.3.开始菜单中打开 Cygwin Terminal，执行以下命令:

git config --system core.fileMode false

git config --global core.quotepath false

git config --global user.name "你的显示名"

git config --global user.email "你的电子邮件”

git config --system alias.st status

git config --system alias.ci commit

git config --system alias.co checkout

git config --system alias.br branch

git config --global color.ui true

# 2.4.增加文件夹上下文菜单

导入注册表文件cygwin.context.menu.reg, 就可以在文件夹空白处鼠标右键直接打开cygwin的命令行窗体了；

# 2.5.生成密钥对

ssh-keygen, 一路回车. 


{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

[cygwin-install]: http://cygwin.com/install.html