# brew install的时候做了什么  

通常，当我们拿到一台崭新的MAC电脑，都会安装Homebrew来管理软件包；  
类似于，Linux系统Redhat系列的 yum 以及Debian系列的 apt-get.

### 为什么使用Homebrew
As we all know, Mac下源码的手动安装一般需要经过下面几个步骤：  
```
1.wget：下载压缩包  
2.tar：解压这个源码软件包  
3.configure：配置，configure是一个可执行脚本，./configure –help输出详细的选项列表,  
其中--prefix选项是配置安装的路径，如果不配置该选项，安装后可执行文件默认放在/usr/local/bin，库文件默认放在/usr/local/lib，配置文件默认放在/usr/local/etc，其它的资源文件放在/usr/local/share。
4.make: 编译程序
5.make install: 安装
```  
如果安装过程中有很多的依赖库，手动解决这些依赖库是十分痛苦的事情，还可能会涉及一些环境变量的设置等操作。  
Homebrew解决了以上繁琐的安装过程，HB会将套件安装到独立目录，并将文件软链接至 /usr/local ，所有文件均会被安装到预定义目录下，所以无需担心 Homebrew 的安装位置。也可以方便的对包进行更新、卸载等操作。  

### brew install的时候具体做了什么  

比如我们在安装wget的时候，输入brew install wget,屏幕上会显示以下内容：  
从软件服务器地址下载，  
安装目录在：/usr/local/Cellar/wget/1.19.1
![](/images/1512150136rv.png)

进入/usr/local/Cellar 目录下可以看到wget的安装文件
![](/images/1512151529vt.png)

ls -l /usr/local/bin 可以看到一条软链指向目录/usr/local/Cellar下
```
lrwxr-xr-x  1 yuanyazhen  admin  30 12  2 01:22 wget -> ../Cellar/wget/1.19.1/bin/wget
```

实际上，install的运行是以下一段Ruby scripts

```ruby
class Wget < Formula
  homepage "https://www.gnu.org/software/wget/"
  url "https://ftp.gnu.org/gnu/wget/wget-1.15.tar.gz"
  sha256 "52126be8cf1bddd7536886e74c053ad7d0ed2aa89b4b630f76785bac21695fcd"

  def install
    system "./configure", "--prefix=#{prefix}"
    system "make", "install"
  end
end
```

### 其他  
1.跟其他包管理器一样，homebrew可以更`换源`，也就是换个软件服务器。  
2.很多时候有些软件包并不在官方提供列表里面而是由第三方提供的这个时候，我们就需要进行`扩展`，使用以下命令：  
brew [un]tap <github_userid/repo_name> #添加或者删除仓库  
```
常用命令  

brew list     列出已安装的软件  
brew update   更新brew  
brew home     用浏览器打开brew的官方网站  
brew info     显示软件信息  
brew deps     显示包依赖  
# 卸载对应包名字
brew uninstall <package_name>
# 列出过时的包
brew outdated
# 更新过时的包，不带包名就跟新所有包
brew upgrade [ package_name ]
# 跟新HomeBrew自身
 brew update
# 清除缓存
brew cleanup [包名]
```  
[Homebrew官网](https://brew.sh/)  
[Homebrew总结](https://zhuanlan.zhihu.com/p/22598799)