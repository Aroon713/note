snpe 설치용

/*.docker 만들기(보충 필요)



1. Install Ubuntu 14.04 (recommended), for example on a virtual machine.

docker run ubuntu:14.04


docker build -t snpe_jaehun  -f Dockerfile --build-arg username=<USERNAME> --build-arg useruid=$UID --build-arg useremail=<USER_EMAIL> .

docker run --name snpe_jaehun2  -it -e DISPLAY=$DISPLAY -v /home/jaehun/workspace/:/home/jaehun/workspace -v /tmp/.X11-unix:/tmp/.X11-unix -v /root/.Xauthority:/root/.Xauthority:rw -v /home/jaehun/.ssh:/home/jaehun/.ssh -p 8001:8888 snpe_jaehun


2. install libraries

참조 : https://lynlab.co.kr/blog/18/

sudo apt-get update
sudo apt-get --yes install python-dev
sudo apt-get --yes install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler libatlas-base-dev nano zip libgflags-dev libgoogle-glog-dev liblmdb-dev python-dev python-matplotlib python-numpy python-protobuf python-scipy python-skimage python-sphinx wget zip default-jdk
sudo apt-get --yes install --no-install-recommends libboost-all-dev


2. Install the latest Android Studio.
wget -c https://dl.google.com/dl/android/studio/ide-zips/3.1.3.0/android-studio-ide-173.4819257-linux.zip

3. Install the latest Android SDK, from Android Studio or stand-alone.

4. Install the latest Android NDK, from the Android Studio SDK Manager or stand-alone.

mkdir -p ~/snpe-devenv/toolchains
cd ~/snpe-devenv/toolchains
wget https://dl.google.com/android/repository/android-ndk-r17b-linux-x86_64.zip
unzip android-ndk-r17b-linux-x86_64.zip
export NDK=~/snpe-devenv/toolchains/android-ndk-r17b

$NDK/build/tools/make_standalone_toolchain.py \
    --arch arm64 \
    --api 26 \
    --stl=libc++ \
    --install-dir=$HOME/snpe-devenv/toolchains/aarch64-android-r17b
export PATH=$HOME/snpe-devenv/toolchains/aarch64-android-r17b/bin:$PATH
export ANDROID_NDK_ROOT=$NDK

4. caffe 설치
참조: https://developer.qualcomm.com/software/qualcomm-neural-processing-sdk/getting-started
      https://developer.qualcomm.com/docs/snpe/setup_caffe.html

sudo apt-get install cmake git libatlas-base-dev libboost-all-dev libgflags-dev libgoogle-glog-dev libhdf5-serial-dev libleveldb-dev liblmdb-dev libopencv-dev libprotobuf-dev libsnappy-dev protobuf-compiler python-dev python-numpy

git clone https://github.com/BVLC/caffe.git ~/caffe; cd ~/caffe; git reset --hard d8f79537977f9dbcc2b7054a9e95be00eb6f26d0

mkdir build; cd build; cmake ..; make all -j4; make install

5. snpe sdk 설치

설치 wget -c <홈피가서 가져와>
source ~/snpe-sdk/bin/dependencies.sh # verifies that all dependencies are installed
source ~/snpe-sdk/bin/check_python_depends.sh # verifies that the python dependencies are installed
cd ~/snpe-sdk/ 
export ANDROID_NDK_ROOT=~/snpe-devenv/toolchains/android-ndk-r17b # default location for Android Studio, replace with yours 

cd $SNPE_ROOT 
python ./models/alexnet/scripts/setup_alexnet.py -a ./temp-assets-cache -d


sudo apt-get install libc6 libncurses5 libstdc++6 lib32z1 libbz2-1.0 # Android SDK build dependencies on ubuntu 
./gradlew assembleDebug # build the APK

