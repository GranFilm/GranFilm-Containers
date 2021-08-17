FROM gcc:9.4.0

LABEL Sunniva Indrehus <sunniva.indrehus@gmail.com>

# Add local folders to the image 
 ADD ./src /usr/src

# Create paths to the installation folders Copy to the lib folder 
RUN mkdir /usr/local/lib/gcc/9.4.0/ && \
    mkdir /usr/local/lib/gcc/9.4.0/Slatec41E && \ 
    mkdir /usr/local/lib/gcc/9.4.0/OpenBLAS

# Build Slatec41E
RUN cd /usr/src/Slatec41E && \
    make all && \ 
    cp /usr/src/Slatec41E/libSlatec41E.a /usr/local/lib/gcc/9.4.0/Slatec41E/

# Build OpenBLAS 
RUN cd /usr/src/OpenBLAS && \ 
    make && \ 
    make PREFIX=/usr/local/lib/gcc/9.4.0/OpenBLAS install 

# Symbolic links for the compilation process
RUN ln -s /usr/local/lib/gcc/9.4.0/Slatec41E/libSlatec41E.a /usr/local/bin/libSlatec41E.a && \
    ln -s /usr/local/lib/gcc/9.4.0/OpenBLAS/lib/libopenblas.a /usr/local/bin/libopenblas.a && \
    ln -s /usr/local/lib/gcc/9.4.0/OpenBLAS/lib/libopenblas.so /usr/local/bin/libopenblas.so && \
    ln -s /usr/local/lib/gcc/9.4.0/OpenBLAS/lib/libopenblas.so.0 /usr/lib/libopenblas.so.0

# Install dependencies 
RUN apt-get update && \
    apt-get install -y makedepf90 

# jupyterhub versions 
#FROM jupyter/scipy-notebook:cf6258237ff9