# Manual de Instalação do ROS 2 Humble (Ubuntu 22.04 + Máquina Virtual)
## Pré-requisitos:
  - Sistema Operacional: Ubuntu 22.04 (Jammy Jellyfish) – 64 bits.
  - Recomenda-se usar uma máquina virtual (ex: VirtualBox).

## Requisitos da Máquina Virtual:
  - RAM: 4 GB ou mais
  - Disco: 20 GB livres
  - Conexão com a internet ativa

# Etapas de Instalação do ROS 2 Humble
## Configurar o Locale:
```bash
locale  # check for UTF-8
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
locale  # verify settings
```

## Configurar os Repositórios
Adicionar o repositório universe:
```bash
sudo apt update && sudo apt install software-properties-common -y
sudo add-apt-repository universe
```
Adicionar o repositório do ROS 2:
```bash
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo tee /usr/share/keyrings/ros-archive-keyring.gpg > /dev/null
```
```bash
echo "deb [signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo "$UBUNTU_CODENAME") main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

## Instalar o ROS 2 Humble
```bash
sudo apt update
sudo apt upgrade -y
```

Instalar a versão Desktop (recomendada):
```bash
sudo apt install ros-humble-desktop -y
```

## Configurar o Ambiente

Adicione o ROS2 ao seu ambiente de forma automática:
```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

Para adicionar de forma permanente, digite no terminal:
```bash
gedit ~/.bashrc. 
```
No final do arquivo que abrir, adicione:
```bash
source /opt/ros/humble/setup.bash
```

Salve o arquivo. Assim, o ROS2 será carregado automaticamente em todas as sessões.

## Testar se o ROS 2 está Funcionando
Em um novo terminal:
```bash
ros2 run demo_nodes_cpp talker
```
Em outro terminal:
```bash
ros2 run demo_nodes_cpp listener
```
Se tudo estiver funcionando corretamente, você verá as mensagens sendo publicadas e recebidas no terminal.


# Tutorial: Criando Workspace para o Stage no ROS 2 Humble

## Preparar o Ambiente
Antes de tudo, certifique-se de que o ROS 2 Humble está instalado e configurado corretamente no seu Ubuntu 22.04. 
Se ainda não fez isso, siga o tutorial de instalação do [ROS 2 Humble](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html
).

No terminal, execute:
```bash
source /opt/ros/humble/setup.bash
```
Para evitar repetir esse comando a cada nova sessão, adicione-o ao final do seu ~/.bashrc.
Também instale os pacotes necessário para o Stage: 
```bash
sudo apt-get install git cmake g++ libjpeg8-dev libpng-dev libglu1-mesa-dev libltdl-dev libfltk1.1-dev
```
## Criar o Workspace
Crie a estrutura básica do workspace:
```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```

## Clonar o Pacote Stage ROS2
Dentro da pasta src, clone o repositório do Stage e do stage_ros2:
```bash
cd ~/ros2_ws/src
git clone --branch ros2 git@github.com:tuw-robotics/Stage.git
git clone --branch humble git@github.com:tuw-robotics/stage_ros2.git
```
## Compilar o seu Workspace:
Execute os seguintes comandos para compilar o workspace:
```bash
cd ~/ros2_ws
colcon build --symlink-install --cmake-args -DOpenGL_GL_PREFERENCE=LEGACY
colcon build --symlink-install --packages-select stage_ros2
```

## Configurar o Ambiente do Workspace
Após a compilação, é necessário configurar o ambiente para que o sistema reconheça os pacotes do workspace:
```bash
source install/setup.bash
```
Para tornar isso permanente, adicione o comando ao seu ~/.bashrc:
```bash
echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc
```


