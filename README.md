🚀 Bitácora de Laboratorio: Infraestructura, Servicios Web y Cloud Computing
Bienvenido/a a este repositorio. En este espacio documento de manera detallada las prácticas de ingeniería de sistemas y redes realizadas durante el curso. El objetivo de este proyecto es registrar el despliegue de arquitectura local, la instalación y securización de servidores web (Apache), y la gestión de infraestructura como servicio (IaaS) en la nube utilizando Microsoft Azure for Students.

🖥️ Práctica 1: Entorno Local, Loopback y Despliegue de Servidor Apache
📌 Objetivos y Contexto
El propósito de esta práctica fue comprender el funcionamiento del protocolo HTTP, el ciclo de vida de las peticiones cliente-servidor, la resolución del bucle de retorno (loopback en 127.0.0.1 / localhost) y el comportamiento de los servicios en segundo plano (daemons) en un entorno Linux.

🛠️ Proceso de Implementación
Actualización del Gestor de Paquetes:
Se preparó el entorno local de Linux actualizando los índices del sistema de paquetes para garantizar la descarga de binarios estables:

Bash
sudo apt update && sudo apt upgrade -y
Instalación y Configuración de Apache2:
Se procedió a la instalación del servidor HTTP Apache2 y se verificó el estado de ejecución mediante el gestor de servicios del sistema (systemd):

Bash
# Instalación del paquete apache2
sudo apt install apache2 -y

# Verificación del estado del servicio
sudo systemctl status apache2

# Habilitación del servicio para inicio automático al arrancar el sistema
sudo systemctl enable apache2
Verificación y Análisis de Respuesta HTTP:
Se validó la correcta ejecución escuchando en el puerto estándar 80. Primero, mediante herramientas CLI como curl para inspeccionar las cabeceras de respuesta HTTP, y posteriormente ingresando a http://localhost desde el navegador para visualizar la Apache2 Ubuntu Default Page.

Bash
# Inspección de cabeceras HTTP en local
curl -I http://localhost
Manipulación del Directorio Raíz del Servidor (/var/www/html):
Se exploró el árbol de directorios de la aplicación y se modificó el archivo index.html para comprobar la entrega de contenido estático personalizado:

Bash
cd /var/www/html
sudo mv index.html index.html.bkp
echo "<h1>Servidor Apache Local Activo - Practica 1</h1>" | sudo tee index.html
🔑 Aprendizajes Clave
Control de procesos daemon mediante systemctl (start, stop, restart, status).

Mapeo del puerto de red 80 y comportamiento de la interfaz lo (loopback).

Estructura de directorios estándar de un servidor web bajo arquitectura UNIX/Linux.

☁️ Práctica 2: Arquitectura de Infraestructura en la Nube con Azure
En esta práctica se migró el concepto de servidor web local hacia un entorno remoto en la nube, diseñando una arquitectura escalable y aislada dentro de Microsoft Azure for Students.

1. 📁 Creación del Grupo de Recursos (Resource Group)
Se definió un Grupo de Recursos como el contenedor lógico principal para agrupar todos los activos de la práctica bajo un mismo ciclo de vida, política de accesos y monitoreo de consumo.

Nombre del Grupo: RG-Practicas-Cloud

Región: East US (o la región asignada con menor latencia).

2. 🌐 Diseño de la Red Virtual (VNet) y Seguridad (NSG)
Se diseñó un segmento de red privado aislado para garantizar que los recursos tengan conectividad segura entre sí e interfaz hacia el exterior.

Direccionamiento CIDR de la VNet: 10.0.0.0/16

Subred (Subnet): Subnet-Web (10.0.1.0/24)

Grupo de Seguridad de Red (NSG): Se configuraron Inbound Security Rules (Reglas de Entrada) para filtrar el tráfico mediante firewall:

Regla SSH: Puerto 22 TCP permitido desde mi IP pública (para administración por consola).

Regla HTTP: Puerto 80 TCP permitido desde cualquier origen (*) para la entrega de tráfico web.

3. 💻 Aprovisionamiento y Acceso a la Máquina Virtual (VM)
Se creó una instancia virtualizada dentro de la subred configurada:

Sistema Operativo: Ubuntu Server 22.04 LTS

Tamaño de la Instancia: Standard_B1s (optimizada para la suscripción de Azure for Students).

Autenticación: Par de claves públicas/privadas SSH (RSA 4096-bit).

Bash
# Asignación de permisos adecuados a la clave privada local
chmod 400 ~/.ssh/id_rsa_azure

# Conexión SSH remota mediante IP Pública asignada por Azure
ssh -i ~/.ssh/id_rsa_azure usuario_azure@<IP_PUBLICA_AZURE>
4. 🚀 Despliegue del Servidor Web en la Nube
Una vez dentro de la consola remota de la VM de Azure, se automatizó el despliegue del servidor HTTP y la apertura de puertos:

Bash
# Actualización del entorno remoto
sudo apt update && sudo apt install apache2 -y

# Verificación de que Apache está escuchando peticiones en la VM remota
sudo netstat -tuln | grep :80

# Comprobación final desde máquina local haciendo petición a la IP Pública
curl -I http://<IP_PUBLICA_AZURE>
