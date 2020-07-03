# 安装opencv<a name="ZH-CN_TOPIC_0228768065"></a>

请按照以下步骤进行安装.

1.  在root用户下更换源。


    **vim /etc/apt/sources.list**
       
    把原有的源更换为国内可用的源。
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted
     
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial universe
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates universe
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial multiverse
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates multiverse
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security universe
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security multiverse
    
    修改完成后 wq 保存并退出。    
    
    让更新源生效。 
    
    **apt-get update**


2.  升级gcc、g++
    1.  安装gcc、g++  

        **add-apt-repository ppa:ubuntu-toolchain-r/test**  
        **apt-get update**  
        **apt-get install gcc-7 g++-7**
        
    2.  删除gcc、g++软链接 
      
        **rm /usr/bin/gcc**  
        **rm /usr/bin/g++**

    3.  为新版本的gcc、g++创建软链接  

        **ln -s /usr/bin/gcc-7 /usr/bin/gcc**  
        **ln -s /usr/bin/g++-7 /usr/bin/g++**

3.  安装依赖库   

    **sudo apt-get install build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg.dev libtiff4.dev libswscale-dev libjasper-dev**  
    
4. 安装ffmpeg  

   1. 下载ffmpeg  
      **wget http://www.ffmpeg.org/releases/ffmpeg-4.1.3.tar.gz**  
      **tar -zxvf ffmpeg-4.1.3.tar.gz**  
      **cd ffmpeg-4.1.3**  

   2. 安装ffmpeg  
      **./configure --enable-shared --enable-pic --enable-static --disable-yasm --prefix=/usr/local/ffmpeg**  
      **make -j8**  
      **make install**

   3.  将ffmpeg添加到系统环境变量中，使得其他程序能够找到ffmpeg环境  
       **vim /etc/ld.so.conf.d/ffmpeg.conf**  
       在末尾添加一行    
       **/usr/local/ffmpeg/lib** 
  
       **ldconfig**  

       **vim /etc/profile**   
       在末尾添加一行    
       **export PATH=$PATH:/usr/local/ffmpeg/bin**   
 
       **source /etc/profile** 
   	
   4. 使opencv能找到ffmpeg  
      **sudo cp /usr/local/ffmpeg/lib/pkgconfig/\*  /usr/share/pkgconfig**

5.  安装opencv
	1.  下载opencv    

    	**git clone -b 4.3.0 https://github.com/opencv/opencv.git**  
    	**cd opencv**  
    	**mkdir build**  
    	**cd build**  

	2.  安装opencv  

    	**cmake -D BUILD_SHARED_LIBS=ON -D BUILD_TESTS=OFF -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local/ ..**  
    	**make**  
    	**make install**  

	3.  配置opencv  
    
    	1.  更新系统库  
        	**sudo ldconfig**
    	2.  配置bash  
        	**vi /etc/bash.bashrc**   
        	在末尾添加两行  
        	**PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig**  
        	**export PKG_CONFIG_PATH**
    
    	3.  更新bash文件  
        	**source /etc/bash.bashrc**  
        	**sudo updatedb**

