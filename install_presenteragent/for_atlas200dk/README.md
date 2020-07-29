# 安装presenteragent<a name="ZH-CN_TOPIC_0228768065"></a>
1.  下载PresentAgent。  
    **cd $HOME**  
    **git clone https://gitee.com/ascend/common.git**
2.  安装tornado包  
    **python3.7.5 -m pip install tornado==5.1.0 --user**
3.  安装autoconf、automake、libtool依赖。  
    **sudo apt-get install autoconf automake libtool**
4.  安装protobuf（按照如下命令一步步执行即可，由于需要交叉编译，所以需要编译两遍）。  
    **git clone -b 3.8.x https://gitee.com/mirrors/protobufsource.git protobuf**  
    **cd protobuf**  
    **git submodule update --init --recursive**  
    **./autogen.sh**  
    **bash configure**  
    **make -j8**  
    **sudo make install**  
    **make distclean**  
    **./configure --build=x86_64-linux-gnu --host=aarch64-linux-gnu --with-protoc=protoc**  
    **make -j8**  
    **sudo make install**    
    **su root**  
    **ldconfig**
5.  编译并安装PresenterAgent。  
    切换回普通用户。  
    **exit**    
    设置下环境变量，在命令行内执行。  
    **export DDK_PATH=/home/ascend/Ascend/ascend-toolkit/20.0.RC1/acllib_centos7.6.aarch64**   
     **说明：  
     _请将X.X.X替换为Ascend-Toolkit开发套件包的实际版本号。  
    例如：Toolkit包的包名为Ascend-Toolkit-20.0.RC1-x86_64-linux_gcc7.3.0.run，则此Toolkit的版本号为20.0.RC1。_**   

    安装Presenteragent。  
    **cd $HOME/common/install_presenteragent/for_atlas200dk/presenteragent/**   
    **make -j8**   
    **make install**  
    将编译好的so传到开发板上。  
    **scp $HOME/ascend_ddk/lib/libpresenteragent.so HwHiAiUser@192.168.1.2:/home/HwHiAiUser**    
    **ssh HwHiAiUser**  
    **su root**  
    **cp /home/HwHiAiUser/libpresenteragent.so /home/HwHiAiUser/Ascend/acllib/lib64**
