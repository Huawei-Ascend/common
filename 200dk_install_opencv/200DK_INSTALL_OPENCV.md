# 安装opencv<a name="ZH-CN_TOPIC_0228768065"></a>

请按照以下步骤进行安装。

1.  下载编译好的opencv到服务器任意目录，如cd $HOME/Downloads。  
    **cd $HOME/Downloads**  

    **git clone https://gitee.com/ascend/common.git**  

2.  拷贝opencv/lib文件夹下所有的文件到/usr/local/lib文件夹下。  
    **su root**

    **cp $HOME/Downloads/common/200dk_install_opencv/opencv/\* /usr/local/lib/**

3.  拷贝opencv/include/下的文件夹到/usr/local/include文件夹下。  
    **cp -r $HOME/Downloads/common/200dk_install_opencv/opencv/include/ /usr/local/include/**    

4.  在开发环境建立软链接。  

    **ln -s /usr/aarch64-linux-gnu/lib /lib/aarch64-linux-gnu**
  
5.  将opencv/200dklib下的所有文件上传到开发板的/home/HwHiAiUser/Ascend/acllib/lib64路径中。  

    普通用户ssh连接上开发板，给lib64目录添加可写权限。  
    **chmod u+w /home/HwHiAiUser/Ascend/acllib/lib64** 
 
    拷贝文件到开发板上  
    **scp -r $HOME/Downloads/common/200dk_install_opencv/opencv/200dklib/\* HwHiAiUser@192.168.1.2:/home/HwHiAiUser/Ascend/acllib/lib64/**  

6.  将开发板上/usr/lib/aarch64-linux-gnu/libc_nonshared.a 拷贝到/lib/aarch64-linux-gnu/lib目录下。  
    
    普通用户ssh连接上开发板，切换到root用户  
    **su root**  

    给/lib/aarch64-linux-gnu/lib目录添加可写权限  
    **chmod u+w /lib/aarch64-linux-gnu/lib**  

    拷贝libc_nonshared.a 到/lib/aarch64-linux-gnu/lib目录下   
    **cp /usr/lib/aarch64-linux-gnu/libc_nonshared.a /lib/aarch64-linux-gnu/lib/**
    
   

