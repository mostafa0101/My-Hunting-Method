# apt-get update -y && apt-get install git -y


<details>
  <summary>Bug Hunting tools</summary>

    cd /tmp && git clone https://github.com/supr4s/WebHackingTools && cd WebHackingTools && ./installer.sh

    git clone https://github.com/0xlegacy52/Bug-Bounty-Hunting-Tools.git
    
    cd Bug-Bounty-Hunting-Tools
    
    chmod +x legacyArsenal.sh
    
    sudo bash legacyArsenal.sh
</details>

----------------------------------------------------------------------

<details>
  <summary>Python</summary>

    sudo apt-get update -y
    sudo apt-get dist-upgrade -y
    sudo apt install -y python3 python3-pip python3.12-venv
    python3 --version
    pip3 --version
</details>

----------------------------------------------------------------------

<details>
  <summary>Go</summary>

    sudo apt-get update -y
    sudo apt-get dist-upgrade -y
    sudo apt-get install -y software-properties-common unzip wget make python3-pip build-essential git ruby-full python3 libpcap-dev cargo dotnet-host netstandard-targeting-pack-2.1 sublist3r assetfinder altdns dirsearch feroxbuster ffuf gobuster dirb dirbuster nmap nikto wpscan dnsrecon jq amass screen ruby
    
    wget https://go.dev/dl/go1.23.3.linux-amd64.tar.gz
    rm -rf /usr/local/go
    sudo tar -C /usr/local -xzf go1.23.3.linux-amd64.tar.gz
    echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zshrc  # Or ~/.bashrc
    echo 'export PATH=$PATH:~/go/bin' >> ~/.zshrc           # Or ~/.bashrc
    source ~/.zshrc  # Or source ~/.bashrc
    go version
    rm -rf go1.23.3.linux-amd64.tar.gz
</details>

----------------------------------------------------------------------








