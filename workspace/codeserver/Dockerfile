# https://hub.docker.com/repository/docker/aleleba/code-server

FROM codercom/code-server:3.12.0

RUN sudo apt-get update

#Instalando Node.js
RUN curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
RUN sudo apt -y install nodejs 
#Terminando de Instalar Node.js

#Instalando wget
RUN sudo apt-get update
RUN sudo apt-get install -y wget

#Instalando Docker
# Let's start with some basic stuff.
RUN sudo apt-get update -qq && sudo apt-get install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    lxc \
    iptables   
# Install Docker from Docker Inc. repositories.
RUN curl -sSL https://get.docker.com/ | sh
# Define additional metadata for our image.
VOLUME /var/lib/docker
RUN sudo usermod -aG docker coder
#Terminando de Instalar Docker

#Instalando kubectl
RUN sudo apt-get update && sudo apt-get install -y apt-transport-https
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
RUN echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
RUN sudo apt-get update
RUN sudo apt-get install -y kubectl
#Terminando de Instalar kubectl

#Instalando doctl
RUN cd ~ && curl -sL https://github.com/digitalocean/doctl/releases/download/v1.38.0/doctl-1.38.0-linux-amd64.tar.gz | tar -xzv
RUN sudo mv ~/doctl /usr/local/bin
#Terminando de Instalar doctl

#Instalando Python
RUN sudo apt update
RUN sudo apt install -y python3-pip
RUN python3 -V
#Terminando de Instalar Python

#Instalando Extensiones
RUN mkdir extensions
#Instalando Extension de Idioma
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ms-ceintl.vscode-language-pack-es
#Instalando Extension de Phython
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ms-python.python
#Instalando Extension de GraphQL
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension kumar-harsh.graphql-for-vscode
#Instalando Extension de GitGraph
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension mhutchie.git-graph
#Instalando Extension de DrawIO
COPY ["./extensions/hediet.vscode-drawio-1.2.0.vsix", "/home/coder/extensions"]
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ./extensions/hediet.vscode-drawio-1.2.0.vsix
#Instalando Extension Sass
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension robinbentley.sass-indented
#Instalando Extension de SassAutoCompile
COPY ["./extensions/Darius2652.sass-autocompile-0.0.7.vsix", "/home/coder/extensions"]
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ./extensions/Darius2652.sass-autocompile-0.0.7.vsix
#Instalando Extension de DotEnv
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension mikestead.dotenv
#Instalando Extension de Docker
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ms-azuretools.vscode-docker
#Instalando Extension de Kubernetes
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ms-kubernetes-tools.vscode-kubernetes-tools
#Instalando Extension de LiveServer
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ritwickdey.liveserver
#Instalando Extension de LiveShare
COPY ["./extensions/MS-vsliveshare.vsliveshare-1.0.3484.vsix", "/home/coder/extensions"]
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ./extensions/MS-vsliveshare.vsliveshare-1.0.3484.vsix
#Instalando Extension de Tema Noctis
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension liviuschera.noctis
#Instalando Extension de Tema Bearded
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension BeardedBear.beardedtheme
#Instalando Extension de Material Icon Theme
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension pkief.material-icon-theme
#instalando extension de browserpreview y chrome
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN sudo apt install -y ./google-chrome-stable_current_amd64.deb
RUN sudo rm -rf ./google-chrome-stable_current_amd64.deb
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension auchenberg.vscode-browser-preview
#Instalando Extension de Debugger for Chrome
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension msjsdiag.debugger-for-chrome
#Instalando Extension de ReduxDevTools
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension jingkaizhao.vscode-redux-devtools
#Instalando Extension de VIM
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension vscodevim.vim
#Instalando Extension de CodeStream
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension CodeStream.codestream
#Instalando Thunder Client
COPY ["./extensions/rangav.vscode-thunder-client-1.9.1.vsix", "/home/coder/extensions"]
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ./extensions/rangav.vscode-thunder-client-1.9.1.vsix
#Instalando Extension de Mysql
COPY ["./extensions/cweijan.vscode-mysql-client2-4.1.5.vsix", "/home/coder/extensions"]
RUN code-server --extensions-dir ~/.local/share/code-server/extensions/ --install-extension ./extensions/cweijan.vscode-mysql-client2-4.1.5.vsix

#Instalando Fira Code
RUN sudo sed -i 's/<\/head>/<link type="text\/css" href="https:\/\/fonts.googleapis.com\/css2?family=Fira+Code:wght@300;400;500;600;700\&display=swap" rel="stylesheet"><\/head>/g' /usr/lib/code-server/src/browser/pages/vscode.html
RUN sudo sed -i 's/font-src/font-src fonts.gstatic.com/g' /usr/lib/code-server/src/browser/pages/vscode.html
RUN sudo sed -i 's/style-src/style-src fonts.googleapis.com/g' /usr/lib/code-server/src/browser/pages/vscode.html

RUN rm -rf /home/coder/extensions

#Agregando Settings Inicial
COPY ["./settings.json", "/home/coder/.local/share/code-server/User/"]
COPY ["./argv.json", "/home/coder/.local/share/code-server/User/"]

# Install the magic wrapper.
ADD ./wrapdocker /usr/local/bin/wrapdocker
RUN sudo chmod +x /usr/local/bin/wrapdocker

RUN sudo sed -i "2 i\exec sudo /usr/local/bin/wrapdocker &" /usr/bin/entrypoint.sh

EXPOSE 8088/tcp