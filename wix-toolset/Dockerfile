# https://medium.com/faun/running-windows-app-headless-in-docker-15ff008f2f16
# http://ubuntuhandbook.org/index.php/2020/01/install-wine-5-0-stable-ubuntu-18-04-19-10/
# err:mscoree:CLRRuntimeInfo_GetRuntimeHost https://www.dedoimedo.com/computers/wine-dotnet-mono.html
# error:light.exe:error LGHT0216 https://bozaro.ru/2016/04/19/wix-wine-wixsharp-en/

FROM ubuntu:16.04
MAINTAINER Aleksei Bulygin <eksuby@rambler.ru>


RUN apt-get update \
	&& apt-get install -y --install-recommends sudo curl wget unzip ca-certificates
		
RUN sudo dpkg --add-architecture i386
RUN apt-get install -y software-properties-common
RUN wget -qO - https://dl.winehq.org/wine-builds/winehq.key | sudo apt-key add -

###  Ubuntu 16.04 
RUN sudo apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ xenial main'

### apt-get update
### E: The method driver /usr/lib/apt/methods/https could not be found.
### N: Is the package apt-transport-https installed? -bah!
RUN apt-get install -y apt-transport-https
RUN apt-get update

RUN apt-get install --install-recommends -y winehq-stable winbind

### Start X server
RUN apt-get update && apt-get install xvfb -y
RUN Xvfb :99 & 
RUN export DISPLAY=:99

### Install .Net40 instead of Wine Mono
RUN wget  https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks -O root/winetricks.sh
RUN chmod +x root/winetricks.sh
RUN bash root/winetricks.sh -q dotnet40

RUN wget https://github.com/wixtoolset/wix3/releases/download/wix3112rtm/wix311-binaries.zip -O root/wix311.zip

RUN unzip root/wix311.zip -d root/wix_toolset_bin

CMD ["bin/bash"]

