# 安装Opencv和PresentAgent<a name="ZH-CN_TOPIC_0228768065"></a>

请按照以下步骤进行安装。

## 安装Opencv

1.  下载Opencv和PresentAgent到服务器任意目录，如cd $HOME/Downloads。  

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

    普通用户ssh连接上开发板，给lib64目录添加可写权限  
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
    
## 安装PresentAgent  

1.  开发板上将/usr/lib64/libprotobuf.so.19 /usr/lib64/libc_sec.so拷贝到开发环境的$HOME/Ascend目录下。  
 
    普通用户ssh连接上开发板  
    拷贝文件到开发环境  
    **scp /usr/lib64/libprotobuf.so.19 HwHiAiUser@192.168.1.223:$HOME/Ascend/**   
 
    **scp /usr/lib64/libc_sec.so HwHiAiUser@192.168.1.223:$HOME/Ascend/**  

    **说明：192.168.1.223为usb虚拟网卡的ip地址，请根据实际情况替换**

2.  在开发环境，生成软连接。   

    **ln -s \\$HOME/Ascend/libprotobuf.so.19 \\$HOME/Ascend/libprotobuf.so**   

3.  将securec.h和securectype.h放置到\\$HOME/Ascend目录下。
  
    **cp \\$HOME/Downloads/common/200dk_presenteragent/securec.h \\$HOME/Ascend** 
 
    **cp \\$HOME/Downloads/common/200dk_presenteragent/securectype.h \\$HOME/Ascend**

4.  编译安装PresentAgent。  

    **cd \\$HOME/Downloads/common/200dk_presenteragent/presenteragent**  

    **make**  

    **make install**

5.  将libpresentagent.so拷贝到开发板的/home/HwHiAiUser/Ascend/acllib/lib64文件夹下。  
    
    **scp ./out/libpresentagent.so HwHiAiUser@192.168.1.2:/home/HwHiAiUser/Ascend/acllib/lib64/**
   