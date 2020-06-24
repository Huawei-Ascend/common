# 安装opencv和ffmpeg<a name="ZH-CN_TOPIC_0228768065"></a>

请用root用户按照以下步骤进行安装。


1.  升级gcc、g++
    1.  安装gcc、g++  

        **yum install centos-release-scl –y**  
        **yum install devtoolset-7-toolchain –y**  
        **scl enable devtoolset-7 bash**
        
    2. 删除gcc、g++软链接  
    
       **rm  /usr/bin/gcc**       
       **rm  /usr/bin/g++**        
       **rm /usr/bin/c++**
    
2. 为新版本的gcc、g++创建软链接    
   
   **ln -s /opt/rh/devtoolset-7/root/usr/bin/gcc /usr/bin/gcc**     
   **ln -s /opt/rh/devtoolset-7/root/usr/bin/c++ /usr/bin/c++**      
   **ln -s /opt/rh/devtoolset-7/root/usr/bin/g++ /usr/bin/g++**

3.  升级cmake   

    **wget https://cmake.org/files/v3.14/cmake-3.14.5.tar.gz**      
    **tar xvf cmake-3.14.5.tar.gz && cd cmake-3.14.5/**      
    **./bootstrap**   
    **gmake**  
    **gmake install**  
    **/usr/local/bin/cmake --version**  
    **yum remove cmake -y**  
    **ln -s /usr/local/bin/cmake /usr/bin/**  
    **cmake --version**
    
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
        
        使profile生效  
   	**source /etc/profile** 
   	
   4. 使opencv能找到ffmpeg  
      **cp /usr/local/ffmpeg/lib/pkgconfig/\*  /usr/share/pkgconfig**

5.  安装opencv
    1. 下载opencv  
       **wget https://github.com/opencv/opencv/archive/4.3.0.zip**  
       **unzip opencv-4.3.0.zip**  
       **cd opencv-4.3.0**  
       **mkdir build**  
       **cd build**
    
    
    2. 安装opencv    
       **cmake -D BUILD_SHARED_LIBS=ON -D BUILD_TESTS=OFF -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local/ ..**  
       **make**  
       **make install**     
   
    
    3. 配置opencv
    
       **vim /etc/ld.so.conf.d/opencv.conf**
    
       在末尾添加两行 
    
       **/usr/local/lib64**  
       **/usr/local/lib**
    
       保存后执行 
       **ldconfig**   

6.  报错解决办法  
    安装opencv，执行到make时可能会报错。   

    报错内容为：  
    virtual memory exhaustedvirtual memory exhaustedvirtual memory exhausted:::   CCCannot allocate memoryannotallocate memoryannot allocate memory  

    解决方法：  
    **mkdir /opt/images/**   
    **rm -rf /opt/images/swap**  
    **dd if=/dev/zero of=/opt/images/swap bs=1024 count=2048000**  
    **mkswap /opt/images/swap**   
    **swapon /opt/images/swap**  
    **free -m**   
    **make clean**  
 
    之后，继续执行make及以后的命令。