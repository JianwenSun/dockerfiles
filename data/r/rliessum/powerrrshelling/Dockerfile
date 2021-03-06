FROM photon:1.0  
MAINTAINER richard@liessum.net  
LABEL PSVersion="v6.0.0-alpha.18"  
  
# Set Versions for later use  
ARG POWERCLI_PACKAGE=PowerCLI.ViCore.zip  
ARG POWERCLI_VDS_PACKAGE=PowerCLI.Vds.zip  
ARG POWERCLI_CIS_PACKAGE=PowerCLI.Cis.zip  
ARG PSSCRIPTANALYZER=development.zip  
  
RUN echo $'[powershell]\n\  
name=VMware Photon Linux 1.0(x86_64)\n\  
baseurl=https://vmware.bintray.com/powershell\n\  
gpgcheck=0\n\  
enabled=1\n\  
skip_if_unavailable=True\n '\  
>> /etc/yum.repos.d/powershell.repo  
  
WORKDIR /powershell  
  
RUN tdnf install -y unzip powershell curl openssl less git  
  
ADD https://download3.vmware.com/software/vmw-
tools/powerclicore/PowerCLI_Core.zip /powershell  
  
RUN unzip /powershell/PowerCLI_Core.zip -d /powershell  
  
RUN mkdir -p /root/.config/powershell/  
RUN mkdir -p ~/.local/share/powershell/Modules  
RUN unzip /powershell/$POWERCLI_PACKAGE -d ~/.local/share/powershell/Modules  
RUN unzip /powershell/$POWERCLI_VDS_PACKAGE -d
~/.local/share/powershell/Modules  
RUN unzip /powershell/$POWERCLI_CIS_PACKAGE -d
~/.local/share/powershell/Modules  
  
RUN mv /powershell/Start-PowerCLI.ps1
/root/.config/powershell/Microsoft.PowerShell_profile.ps1  
  
ADD https://github.com/vmware/powernsx/archive/master.zip /powershell  
RUN mkdir ~/.local/share/powershell/Modules/PowerNSX  
RUN unzip /powershell/master.zip -d /powershell/  
RUN cp -Rv /powershell/powernsx-master/
~/.local/share/powershell/Modules/PowerNSX/  
  
RUN powershell -Command 'Set-PSRepository -Name PSGallery -InstallationPolicy
Trusted'  
RUN powershell -Command 'Install-Module -Name PowervRA -Confirm:$false'  
  
RUN powershell -Command 'Install-Module -Name PSScriptAnalyzer'  
RUN powershell -Command 'Import-Module -Name PSScriptAnalyzer'  
RUN powershell -Command 'Install-Module -Name coveralls'  
RUN powershell -Command 'Install-Module -Name Pester'  
RUN powershell -Command 'Install-Module -Name Posh-git'  
  
RUN git clone https://github.com/vmware/PowerCLI-Example-Scripts  
  
RUN mv /powershell/PowerCLI-Example-Scripts/Modules/VMware.VMEncryption
~/.local/share/powershell/Modules/  
RUN mv /powershell/PowerCLI-Example-Scripts/Modules/VMFSIncrease
~/.local/share/powershell/Modules/  
RUN mv /powershell/PowerCLI-Example-Scripts/Modules/Vi-Module
~/.local/share/powershell/Modules/  
RUN chmod +x /powershell/PowerCLI-Example-Scripts/Scripts/modules.sh  
RUN /powershell/PowerCLI-Example-Scripts/Scripts/modules.sh  
  
WORKDIR /tmp/scripts  

