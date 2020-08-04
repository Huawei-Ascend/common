# 安装presenteragent<a name="ZH-CN_TOPIC_0228768065"></a>
1.  下载PresentAgent  
    **cd $HOME**  
    **git clone https://gitee.com/ascend/common.git**
2.  安装tornado包  
    **python3.7.5 -m pip install tornado==5.1.0 --user**
3.  安装autoconf、automake、libtool依赖  
    **sudo apt-get install autoconf automake libtool**
4.  安装protobuf  
    **git clone -b 3.8.x https://gitee.com/mirrors/protobufsource.git protobuf**  
    **cd protobuf**  
    **git submodule update --init --recursive**  
    **./autogen.sh**  
    **bash configure**  
    **make -j8**  
    **sudo make install**   
    **su root**  
    **ldconfig**
5.  编译并安装PresenterAgent  
    切换回普通用户。  
    **exit**   
    设置下环境变量，在命令行内执行。  
    **export DDK_PATH=/home/ascend/Ascend/ascend-toolkit/X.X.X/acllib_centos7.6.x86_64**   
    >![](public_sys-resources/icon-note.gif) **说明：**  
        **请将X.X.X替换为Ascend-Toolkit开发套件包的实际版本号。  
        例如：Toolkit包的包名为Ascend-Toolkit-20.0.RC1-x86_64-linux_gcc7.3.0.run，则此Toolkit的版本号为20.0.RC1。**   

    安装Presenteragent。  
    **cd $HOME/common/install_presenteragent/for_atlas200dk/presenteragent/**   
    **make -j8**   
    **make install**  
6.  删除toolkit包中自带的protobuf  
    由于我们使用的presentserver需要3.8.0版本的protobuf，所以我们在环境中安装了protobuf。但是开发环境的toolkit包中自带了protobuf的so，编译时会自动链接到该so。所以我们需要删除该so。

    切换root用户  
     **su root**     
    进入protobuf.so目录  
     **cd /home/HwHiAiUser/Ascend/ascend-toolkit/20.0.0.RC1/x86_64-linux_gcc7.3.0/atc/lib64**  
    执行以下命令，将so改名  
     **mv libprotobuf.so libprotobuf.so.bak**     
     **mv libprotobuf.so.19 libprotobuf.so.19.bak**     
    退出root用户    
     **exit**   
