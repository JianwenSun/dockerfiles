FROM underworldcode/underworld2_untested:dev_magnus  
MAINTAINER romain.beucher@unimelb.edu  
  
RUN apt-get update -qq  
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends
\  
python-tk  
  
# UWGeodynamics  
WORKDIR /opt  
RUN git clone -b development https://github.com/rbeucher/UWGeodynamics.git  
RUN pip install -e /opt/UWGeodynamics  
  
# Badlands dependency  
RUN pip install pandas  
RUN pip install ez_setup  
RUN pip install git+https://github.com/badlands-model/triangle.git  
RUN pip install git+https://github.com/awickert/gFlex.git  
  
# pyBadlands serial  
WORKDIR /opt  
RUN git clone https://github.com/rbeucher/pyBadlands_serial.git  
RUN pip install -e pyBadlands_serial/  
WORKDIR /opt/pyBadlands_serial/pyBadlands/libUtils  
RUN make  
RUN pip install -e /opt/pyBadlands_serial  
  
# pyBadlands dependencies  
RUN pip install cmocean  
RUN pip install colorlover  
# Force matplotlib 2.1.2 (Bug Badlands), Temporary  
RUN pip install matplotlib==2.1.2  
  
ENV PATH $PATH:/opt/pyBadlands_serial/pyBadlands/libUtils  
ENV LD_LIBRARY_PATH
$LD_LIBRARY_PATH:/opt/pyBadlands_serial/pyBadlands/libUtils  
  

