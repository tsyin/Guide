# Git生成sshkey,并链接github  
## ssh知识点  
*设置github加速      
  >更改hosts文件   
  windows系统hosts文件位于目录：C:WindowsSystem32driversetc   
  linux系统的hosts文件位于目录：/etc/   
  添加以下内容：   
'''
  140.82.114.3 github.com   
  199.232.69.194 github.global.ssl.fastly.net   
  185.199.108.153 github.com   
  185.199.109.153 github.com   
  185.199.110.153 github.com   
  185.199.111.153 github.com   
  '''
  对于windows系统还需要在cmd窗口输入ipconfig /flushdns才能使用
* ssh  
  >Secure Shell (SSH) 是一个允许两台电脑之间通过安全的连接进行数据交换的网络协议。通过加密保证了数据的保密性和完整性。SSH采用公钥加密技术来验证远程主机，以及(必要时)允许远程主机验证用户。  
  
* SSH的好处  
  >传统的FTP、Telnet是再网络中明文传送数据、用户帐号和密码，很容易受到中间人攻击。而通过使用SSH，你可以把所有传输的数据进行加密，这样“中间人”这种攻击方式就不可能实现了， 而且也能够防止DNS和IP欺骗;  
  传输的数据是经过压缩的，所以可以加快传输的速度。  
* 实现SSH的好处  
  >SSH利用SSH Key来进行前面提到的基于密钥的安全验证。  
* SSH-Key  
  >SSH-Key 就是一对密钥对  
  公钥是给别人用的。私钥是给自己用的  
  别人是谁？可以是GitLab服务器  
  自己是谁？可以是本地  
  本地想要使用git从gitHub/gitlab上拉取代码  
  给GitHub/GitLab配置公钥，公钥就可以作为一个加密的箱子，将代码放在箱子里  
  被本地拉取到后，使用私钥将加密的箱子打开。就能拿到代码了  
  整个过程中，都没有用户名/密码在网络中传输，所以不会给他人拦截到，破解你的数据  
  SSH-Key的直观作用，就是【让你方便的登录到 SSH 服务器，而无需输入密码】  
* SSH-Key的密钥类型  
  >有RSA和DSA两种认证密钥
* ssh-keygen命令参数解释  
  >-b：指定密钥长度;  
-e：读取openssh的私钥或者公钥文件;  
-C：添加注释;  
-f：指定用来保存密钥的文件名;  
-i：读取未加密的ssh-v2兼容的私钥/公钥文件，然后在标准输出设备上显示openssh兼容的私钥/公钥;  
-l：显示公钥文件的指纹数据;  
-N：提供一个新密语;  
-P：提供（旧）密语;  
-q：静默模式;   
-t：指定要创建的密钥类型。  
## ssh生成密钥  
1. 到用户目录下  
    >linux:cd /root  
    windows:cd /用户  
2. 查看是否已经存在SSH-Key(.ssh隐藏文件夹)  
    >ls -al ~/.ssh  
    如果没有就新建，如果有，建议删除再新建   
    rm -rf .ssh  
3. 新生成SSH-key(替换成你自己的邮箱)
    >```ssh-keygen -t rsa -C "1115653102@qq.com"```  (三次回车默认生成)
4. 生成后，会在/root目录下，也就是当前用户的目录下，生成一个.ssh隐藏目录，目录中会有[id_rsa]和[id_rsa.pub]两个文件，一个是私钥，一个是公钥。
5. 复制使用  
    >cat *.pub  
6.将内容复制到github中sshkey,测试是否连接上github  
    >ssh -T git@github.com  
    无错表示连接成功
## git的使用方法
1. 配置   
    >安装好git后，在命令行或终端中使用下面的命令可以设置git自己的名字和电子邮件。这是因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。  
    ```
    git config --global user.name "tsyin_desktop"  
    git config --global user.email "1115653102@qq.com"
    ```
    >注意git config命令的–global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。  
    配置好之后可以使用下面命令查看配置  
    ```
    git config -l
    ```
    
  
2. 创建仓库  
    先在github上创建一个仓库
    >github提供了两种和本地仓库关联起来的方式  
    * 方法一  
      >把本地已有的同名Git仓库和GitHub上的仓库关联起来  
      我们在本地新建了一个名为*(和远程仓库名一样)的文件夹，将文件夹设置成git本地仓库  
      command进入这个文件夹  
      ```
      cd *
      git init
      ```
      >新建一个文件，随便写点什么,例如hello.txt
      将文件加入到更新清单里，并提交到本地仓库  
      ```
      git add hello.txt
      git commit -m "第一次提交"
      ```
      >关联本地仓库和远程仓库(github仓库)  
      ```
      git remote add origin git@github.com:tsyin/cppcode.git
      ```
      >remote是远程的意思，操作远程仓库时记得加上remote,origin是托管版本  
    * 方法二  
      >从已有的github仓库克隆到本地  
      ```
      git clone git@github.com:fsliurujie/cppcode.git
      ```
      >git clone的几种用法  
      ```
      git clone git@github.com:fsliurujie/test.git         --SSH协议  
      git clone git://github.com/fsliurujie/test.git          --GIT协议  
      git clone https://github.com/fsliurujie/test.git      --HTTPS协议  
      ```
  
