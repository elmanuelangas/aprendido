💻 Práctica 1: Servidor Local (Localhost)
📌 Descripción
Configuración y puesta en marcha de un servidor en entorno local para verificar el comportamiento de servicios web y la resolución de bucles de retorno (loopback).

🖥️ Comandos Utilizados
# Iniciar servidor local (ejemplo con Python)
python -m http.server 8000

# O verificar conectividad mediante cURL
curl -I http://localhost:8000
☁️ Práctica 2: Máquina Virtual en Azure for Students
📌 Descripción
Aprovisionamiento de infraestructura en la nube mediante Azure, configuración de redes virtuales (VNet) y reglas de firewall en el Grupo de Seguridad de Red (NSG).

🖥️ Comandos de Conexión y Gestión
# Conexión SSH a la máquina virtual remota
ssh usuario@ip_publica_de_tu_vm

# Actualización de paquetes en la VM (Ubuntu)
sudo apt update && sudo apt upgrade -y

# Verificación de servicios activos en la VM
sudo systemctl status ssh
