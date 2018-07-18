snpe 설치용

docker run ubuntu:14.04


docker build -t snpe_jaehun  -f Dockerfile --build-arg username=jaehun --build-arg useruid=$UID --build-arg useremail=jaehun.jeong1@partner.samsung.com  .

docker run --name snpe_jaehun2  -it -e DISPLAY=$DISPLAY -v /home/jaehun/workspace/:/home/jaehun/workspace -v /tmp/.X11-unix:/tmp/.X11-unix -v /root/.Xauthority:/root/.Xauthority:rw -v /home/jaehun/.ssh:/home/jaehun/.ssh -p 8001:8888 snpe_jaehun


sudo apt-get update
sudo apt-get install python-dev
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
