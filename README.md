# Docker: Investigación y Aplicación Práctica

## 1. ¿Qué es Docker?

Docker es una plataforma de código abierto que permite desarrollar, enviar y ejecutar aplicaciones dentro de contenedores. Estos contenedores son entornos aislados que contienen todo lo necesario para que una aplicación funcione: código, bibliotecas, dependencias y configuraciones.

## 2. ¿Para qué sirve Docker?

Docker se utiliza para:

- **Portabilidad**: Los contenedores pueden ejecutarse en cualquier sistema que tenga Docker instalado, independientemente del entorno subyacente.
- **Eficiencia**: Al compartir el kernel del sistema operativo, los contenedores son más ligeros y rápidos que las máquinas virtuales tradicionales.
- **Escalabilidad**: Facilita el despliegue y escalado de aplicaciones en entornos de producción, especialmente en arquitecturas de microservicios.

## 3. Instalación de Docker en Ubuntu

### Requisitos previos
Ubuntu 22.04 o superior. Se necesitan permisos de administrador (sudo).

### Pasos para instalar Docker:

```bash
# Actualizar paquetes del sistema
sudo apt update
sudo apt upgrade

# Instalar paquetes necesarios
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Agregar la clave GPG de Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Agregar el repositorio de Docker
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

# Actualizar el índice de paquetes
sudo apt update

# Instalar Docker
sudo apt install docker-ce

# Verificar que Docker esté activo
sudo systemctl status docker
```
