FROM ubuntu:wily  
  
ENV DEBIAN_FRONTEND noninteractive  
  
RUN apt-get update && apt-get install -y \  
texlive-full \  
python-matplotlib \  
python-nose \  
python-numpy \  
python-pandas \  
python-pygments \  
python-scipy \  
python-sympy \  
latexmk \  
biber \  
git-core \  
&& apt-get clean && rm -rf /var/lib/apt/lists/*

