# Tutorial: Criando Workspace para o Stage no ROS 2 Humble

## Preparar o Ambiente
Antes de tudo, certifique-se de que o ROS 2 Humble está instalado e configurado corretamente no seu Ubuntu 22.04. 
Se ainda não fez isso, siga o tutorial de instalação do [ROS 2 Humble](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html
) ou [ROS2 - Máquina Virtual](ros2_install.md).

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
git clone --branch ros2 https://github.com/tuw-robotics/Stage.git
git clone --branch humble https://github.com/tuw-robotics/stage_ros2.git
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


