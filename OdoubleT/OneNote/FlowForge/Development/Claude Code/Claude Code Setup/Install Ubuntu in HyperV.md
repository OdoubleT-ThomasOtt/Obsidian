1. disable secure boot in vm settings, install from iso (additional software added)
2. Set-VM -VMName "DevLnx" -EnhancedSessionTransportType HvSocket (powershell in windows ausführen)
3. Enhanced mode install: [https://www.windowspro.de/wolfgang-sommergut/ubuntu-2404-hyper-v-vm-generation-2-installieren](https://www.windowspro.de/wolfgang-sommergut/ubuntu-2404-hyper-v-vm-generation-2-installieren)
    1. [https://github.com/Hinara/linux-vm-tools/blob/master/ubuntu/24.04/install.sh](https://github.com/Hinara/linux-vm-tools/blob/master/ubuntu/24.04/install.sh) runterladen
    2. ==chmod +x install.sh==
    3. ==sudo ./install.sh== ==-\> restart und dann nochmal ausführen, dann nochmal restart==
    4. ==Sollte der bildschirm schwarz bleiben und noch die normale anmeldung gezeigt werden die VM einmal komplett abschalten und starten==
4. ==Install rider:==
    1. ==sudo snap install rider --classic==
    2. ==Install claude plugin in rider gui==
5. ==Install claude==
    1. sudo apt install -y nodejs npm
    2. Sudo npm install -g @anthropic-ai/claude-code
6. Install .net framework: [https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-install?tabs=dotnet9&pivots=os-linux-ubuntu-2404](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-install?tabs=dotnet9&pivots=os-linux-ubuntu-2404)
    1. sudo add-apt-repository ppa:dotnet/backports
    2. sudo apt-get update && \
    
    sudo apt-get install -y dotnet-sdk-9.0
    
    4. sudo apt-get update && \
    
    sudo apt-get install -y aspnetcore-runtime-9.0