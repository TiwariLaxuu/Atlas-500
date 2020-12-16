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



