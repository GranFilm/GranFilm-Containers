FROM gcc:9.4.0

LABEL Sunniva Indrehus <sunniva.indrehus@gmail.com>

ENV HOME /root

# Create folders 
RUN mkdir -p ${HOME}/usr/src && \ 
    mkdir -p ${HOME}/usr/lib/gcc/9.4.0/OpenBLAS && \
    mkdir -p ${HOME}/usr/lib64

# Add local folders to the image 
COPY ./src ${HOME}/usr/src

# # Build OpenBLAS 
RUN cd ${HOME}/usr/src/OpenBLAS && \ 
    make && \ 
    make PREFIX=${HOME}/usr/lib/gcc/9.4.0/OpenBLAS install 

# # Symbolic links for the compilation process
RUN ln -s ${HOME}/usr/lib/gcc/9.4.0/OpenBLAS/lib/libopenblas.a ${HOME}/usr/lib64/libopenblas.a && \
    ln -s ${HOME}/usr/lib/gcc/9.4.0/OpenBLAS/lib/libopenblas.so ${HOME}/usr/lib64/libopenblas.so && \
    ln -s ${HOME}/usr/lib/gcc/9.4.0/OpenBLAS/lib/libopenblas.so.0 /usr/lib/libopenblas.so.0

# Install dependencies for the dependencies of the building process
RUN apt-get update && apt-get -y update

RUN apt-get install -y makedepf90   
RUN apt-get -y install python3-pip
 
ADD ./GranFilm/granfilmpy/requirements.txt .
RUN pip3 install -r requirements.txt

RUN apt-get install texlive-latex-base texlive-latex-extra texlive-fonts-recommended xzdec -y 
RUN apt-get install cm-super -y 
RUN apt-get install dvipng -y 

CMD ["/bin/bash", "-l"]
