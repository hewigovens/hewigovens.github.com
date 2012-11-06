---
layout: post
title: "Install dpkg on Mac"
description: ""
category: 
tags: 
- mac
- dpkg
---
{% include JB/setup %}

最近需要在Mac下生成Cydia源的Packages文件，结果遇到一堆问题，现在记录下过程。

**Step1**. [brew](http://mxcl.github.com/homebrew/)安装dpkg:

{% highlight sh %} 
	$ brew install dpkg
{% endhighlight %}

dpkg-deb命令基本可以用了，但是dpkg-scanpackages会提示找不到Dpkg.pm

**Step2**. 下载[libdpkg-perl](http://packages.debian.org/sid/libdpkg-perl) 解压并放入Perl目录下：

{% highlight sh %} 
	$ dpkg-deb -x libdpkg-perl_1.16.9_all.deb tmp
{% endhighlight %}  
{% highlight sh %} 
	$ sudo cp -Rf tmp/usr/share/perl5/Dpkg* /Library/Perl/5.12
{% endhighlight %}

**Step3**. brew安装coreutils和md5sha1sum:

{% highlight sh %}
$ brew install coreutils md5sha1sum 
{% endhighlight %}

如果下载md5sha1sum的时候提示403错误，可以手动从[镜像处](http://www.sourcefiles.org/Utilities/Console/M-P/md5sha1sum-0.9.5.tar.gz)下载并放入/Library/Caches/Homebrew，再brew install 一遍应该就好了。

另外coreutils安装之后所有的命令都有g的前缀，运行dpkg-scanpackages会提示找不到sha256sum，可以简单给gsha256sum创建一个符号链接，或者是在bashrc/zshrc下添加一行:
{% highlight sh %} 
PATH="$(brew --prefix coreutils)/libexec/gnubin:$PATH"
{% endhighlight %}

**Step4**. patch dpkg-scanpackages
生成的Packages中Filename路径不正确，多了个/，需要修改下dpkg-scanpackages

{% highlight bash %} 
 	vim `which dpkg-scanpackages`
{% endhighlight %}
 
 跳到line 187, 添加一行:
{% highlight perl %}
 	$fn =~ s/\.\/\//\.\//g;
{% endhighlight %}

这下dpkg应该基本没问题了~



