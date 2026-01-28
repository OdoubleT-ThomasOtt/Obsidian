**Linux Setup:**

2. Install 22 from Template. Do not update to 24 because it will not support fullscreen
3. Resize hdd:
    1. Resize harddrivedisc in hyperV
    2. sudo apt update && sudo apt install cloud-guest-utils
    3. sudo growpart /dev/sda 1
    4. sudo resize2fs /dev/sda1
4. Curl installieren:
    1. sudo apt update
    2. sudo apt install curl
5. node js installieren
    1. curl -o- [https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh](https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh) | bash
    
    source ~/.bashrc  
    nvm install 22  
    node -v  
    npm -v
    
6. .Net 8 installieren
    1. wget [https://packages.microsoft.com/config/ubuntu/](https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb)**22.04**/packages-microsoft-prod.deb \
    
    -O packages-microsoft-prod.deb --\> Version anpassen falls nötig
    
    3. sudo dpkg -i packages-microsoft-prod.deb
    
    sudo rm packages-microsoft-prod.deb  
    sudo apt update
    
    5. sudo apt install -y dotnet-sdk-8.0
7. .Net EF install
    1. dotnet tool install --global dotnet-ef --version 8.*
8. Github install:
    1. sudo apt update && sudo apt install git
    2. sudo apt install gh
    3. gh auth login
9. Claude code installieren:
    1. npm install -g @anthropic-ai/claude-code
10. CCUsage Install_
    1. npm install -g ccusage (start with ccusage blocks --live)
11. Install Playwright
    1. npm install playwright
    2. npx playwright install chrome
      
        
**Claude Code Setup in WSL**

16. Neue Win11 VM anlegen
17. Set-VMProcessor -VMName "Windows 11 dev" -ExposeVirtualizationExtensions $true

--\> Im Host mit Powershell als Admin für denn sonst kann man darin kein Linux subsystem hosten

19. wsl --install

--\> Linux Subsystem installieren

21. curl -o- [https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh](https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh) | bash

source ~/.bashrc  
nvm install 22  
node -v  
npm -v  
--\> node js installieren

23. npm install -g @anthropic-ai/claude-code

--\> claude code installieren

25. Claude in ubuntu terminal starten oder plugin command durch wsl -d Ubuntu -e bash -ic "cd /mnt/d/GitHub/eSource && claude" ersetzten

--\> claude starten

27. /ide -\> rider auswählen
28. /model opus-4

--\> Modell wechseln
 
**DNS Auflösung aktivieren:**

32. sudo sh -c "echo '[network]\ngenerateResolvConf = false' \> /etc/wsl.conf"
33. sudo rm /etc/resolv.conf
34. echo -e "nameserver 8.8.8.8\nnameserver 8.8.4.4" | sudo tee /etc/resolv.conf
35. In windows powershell: wsl --shutdown 
**.Net Installation:**

38. curl -L [https://dot.net/v1/dotnet-install.sh](https://dot.net/v1/dotnet-install.sh) -o dotnet-install.sh

chmod +x dotnet-install.sh

40. ./dotnet-install.sh --channel 8.0
41. export DOTNET_ROOT=$HOME/.dotnet

export PATH=$PATH:$DOTNET_ROOT:$DOTNET_ROOT/tools  
sudo ln -sf $HOME/.dotnet/dotnet /usr/bin/dotnet
 
**Claude Usage:**

45. npm install -g ccusage
46. In batch file: wsl -d Ubuntu -e bash -ic "ccusage blocks --live"

pause

48. In batch file: wsl -d Ubuntu bash -ic "ccusage blocks --live"

pause
       
**Claudia Setup:**

56. **Installieren:**
57. Rust installieren:
58. Unzip installieren:
59. Bun installieren:
                      
git clone https://github.com/getAsterisk/claudia.git  
cd claudia
 
# Abhängigkeiten installieren  
npm install  
curl --proto '=https' --tlsv1.2 -sSf [https://sh.rustup.rs](https://sh.rustup.rs) | sh  
sudo apt update  
sudo apt install -y unzip  
curl -Lo bun.zip \  
[https://github.com/oven-sh/bun/releases/latest/download/bun-linux-x64.zip](https://github.com/oven-sh/bun/releases/latest/download/bun-linux-x64.zip)  
mkdir -p ~/.bun  
unzip bun.zip -d ~/.bun

![[90 Extras/Attachments/start-claudia.bat]]
 
1. Start Batch Datei erstellen:
2. Windows-Taste + R drücken, shell:startup eingeben und bestätigen und batch Datei einfügen