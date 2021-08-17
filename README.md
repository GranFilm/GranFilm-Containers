# Containers to build and run different versions of GranFilm 

## Constatns in this file 

    MY_VERSION = the version of GranFilm you whish to build 
    MY_REPO    = the folder that contains your source code.
    MY_TEMP    = folder to build and run GranFilm 

## Loacally build docker image

    [~/]$ cd MY_VERSION
    [~/MY_VERSION]$ docker build -t granfilm-gcc9.4.0-libs .



    [~/MY_VERSION]$ docker build -t granfilmpy . 

## Different ways to run the image 

### Locally run docker image 

    $ [~/]$ cd MY_REPO 
    $ [~/MY_REPO]$ docker run -it --rm granfilm-gcc9.4.0-libs:latest


### Locally run docker image 

    $ [~/MY_REPO]$ docker run -it --rm -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_Containers/2.0/test-access:/usr/lib64/ \
        granfilm-gcc9.4.0-libs

### Mounting in GranFilm and Run folder 

First attempt 

    [~/MY_TEMP]$ docker run -it --rm \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilm:/granfilm \
    -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_BuildRun/Run:/run \
    granfilm-gcc9.4.0-libs:latest


    docker run -it --rm \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilm:/root/granfilm \
    -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_BuildRun/Run:/root/run \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilmpy:/root/granfilmpy \
    granfilm-gcc9.4.0-libs:latest

    docker run -it --rm \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilm:/root/granfilm \
    -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_BuildRun/Run:/root/run \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilmpy:/root/granfilmpy \
    granfilm:latest


    docker run -it --rm \
    -p 8888:8888 \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilm:/root/granfilm \
    -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_BuildRun/Run:/root/run \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilmpy:/root/granfilmpy \
    granfilmpy:latest


Second attempt

    [~/MY_TEMP]$ docker run -it --rm \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilm:/home/jovyan/granfilm \
    -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_BuildRun/Run:/home/jovyan/run \
    -v /home/sunnivin/Documents/code_work/GranFilm/granfilmpy:/home/jovyan/granfilmpy \
    binder-granfilmpy:latest



## How to run GranFilm inside the container and save the output



## Building the neccessary libaries


### OpenBLAS 

    root@443890d41889:/usr/src/libs/OpenBLAS# make PREFIX=/usr/local/lib/OpenBLAS/9.4.0 install



# Testing jupyter notebooks 

    root@060096e4efb3:/granfilmpy# cd ../root/granfilmpy/doc/
    root@698ba9a6229f:~/granfilmpy/doc# jupyter notebook --port=8888 --no-browser --ip=0.0.0.0 --allow-root



    docker run -it --rm \
    -p 8888:8888 \
    -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_Containers/granfilmpy/GranFilm/granfilm:/root/granfilm \
    -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_BuildRun/Run:/root/run \
    -v /home/sunnivin/Documents/code_work/GranFilm/GranFilm_Containers/granfilmpy/GranFilm/granfilmpy:/root/granfilmpy \
    granfilmpy:latest

## Container information: 
Remember that the container granfilm-gcc-9.4 and granfilmpy is mainly used for development. granfilm-binder containes the executable in the shell. 