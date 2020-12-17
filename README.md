# Atlas-500
Development Environment 
Hardware Requirement:: 1. x86 Server, Atlas 500-3000 and your working pc. 
Software Requirement:: 1. InstalltheUbuntux86or Cent OS X86 ontheserver  2. Download Ascend Software Packages from Huawei website. 

After install the ascend toolkit, there are some sample projects. 
step 1: Obtain the model
step 2: Convert the model
step 3: Set Environment Variables 
Step 4: Compile the source code

Run the sample at ATLAS 500
Login to Atlas 500 and enter “develop mode”. 
Package all the sample executable filesand its dependcies. In this sampleprojectmust package the “out”、“data”、“model” directoryand the “acl.json” file.

#copy all the files to a temporary directory, for example “outfiles”
.cd /usr/local/Ascend/ascend-toolkit/{version}/arm64-linux_gcc7.3.0/acllib/sample/acl_execute_model/acl_vpc_jpege_resnet50/mkdir outfiles

cp -r ./data ./outfiles

cp -r ./model./outfiles

cp -r ./out./outfilesmkdir ./outfiles/src

cp ./src/alc.json ./outfiles/src

#compress all the file

star -zcvf outfiles.tar ./outfiles

Here, first we make a folder outfiles and package all data, models and alc.json file and conpress all file. 

Upload the packagefile “outfiles.tar” to any directoryand decompress all the files. For how to login and upload. 
#go to the directory where the “outfiles.tar” file located

cd {your dir}

#decompress the filetar -xzf outfiles.tar

#go to the directory where the “main” file located

cd outfiles/out

#add the executable to “main”chmod +x main

#run

./main 0 --execution result--Decode two *.jpg images into two YUV420SP NV12 images, resize them, and perform model inference to obtain the inference results of the two images.

./main 1 --execution result-- same as parameter 0 but has crop them instead of resize them. 

./main 2 -- execution result -- same as parameter 1 and has also paste option with crop.

./main 3 --Encode a YUV420SP image into a *.jpg image


##Configuring a System Network Proxy
Log in to the user environment as therootuser
Open the/etc/profilefile:
Add the following content to the file, save the file, and exit
export http_proxy="http://user:password@proxyserverip:port"export https_proxy="http://user:password@proxyserverip:port"
Go to the .pip directory
create a pip.conffile in the.pipdirectory:
Edit the pip.conffile.
 

[install]#Configure the trusted host as required.trusted-host=mirrors.tools.huawei.com[global]#Configure the sources as required.index-url=http://mirrors.tools.huawei.com/pypi/simple/

Run the:wq!command to save the file and exit
 
 
 
 To maximize the computing power of Ascend 310 chips, Huawei provides the Matrix framework to migrate inference services. The Matrix framework provides the following functions:
     Process orchestration
        An engine is defined as a basic functional unit in the process, and its implementation can be customized (for example, inputting image data, classifying images, and outputting the predicted class of images). By default, each engine corresponds to a thread on Ascend 310.
        A graph is defined to manage multiple engines. Each graph corresponds to a process on Ascend 310. Figure 8-1 shows the relationship between the graph and engines.
  

    In the graph configuration file, configure the serial connections of engine nodes and node properties (parameters required for node running). The actual data flow direction is implemented on the nodes based on the specific service. The entire engine computation process is started by inputting data to the start node of the service.

    Media pre-processing

    Engines running on Ascend 310 can directly call the APIs provided by the DVPP to implement the media pre-processing capability.
    Offline model loading and running

    Engines running on Ascend 310 can directly call the APIs provided by the model manager (AIModelManger) to load offline models and perform inference.

    The following figure shows a user's service software structure based on the Matrix framework. The user creates a service flow (graph) that consists of custom engines. Engines running on the device side can call the APIs of the DVPP and AIModelManager to utilize Ascend 310-enabled media pre-processing and the hardware acceleration function of model inference. Engines on the host side are used to implement the service software logic and exchange data with the engines on the device side.
    Figure 8-2 Service software framework




