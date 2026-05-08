# Bitacora-Tecnica-IV.-Laboratorio-de-Teletransportacion-Digital-SSH-y-RDP-

## *Tarea 1:* Despliegue de la Infraestructura
Creo una carpeta en mi equipo a la que llamo SI_Bitacora4_SergioGarciadeBaya despues dentro de la carpeta guardar el archivo docker-compose.yml con el siguiente codigo:

# Laboratorio de Sistemas Informáticos - Bitácora 3
# Este archivo levanta dos servicios: un servidor SSH y un entorno gráfico vía RDP/Web
<!--
version: '3.8'

services:
  # Servidor especializado para prácticas de SSH y seguridad
  servidor_ssh:
    image: linuxserver/openssh-server:latest
    container_name: lab_ssh_servidor
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Madrid
      - USER_NAME=alumno
      - USER_PASSWORD=sistemas_informaticos
      - PASSWORD_ACCESS=true
    ports:
      - "2222:2222" # Mapeamos el puerto 2222 local al 2222 del contenedor
    restart: unless-stopped

  # Servidor con entorno gráfico ligero (XFCE) accesible por RDP y Web
  servidor_rdp:
    image: linuxserver/webtop:ubuntu-xfce
    container_name: lab_rdp_servidor
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Madrid
    ports:
      - "3389:3389" # Puerto estándar de Escritorio Remoto (RDP)
      - "3000:3000" # Puerto para acceso vía navegador (HTTP/Guacamole)
    shm_size: "1gb" # Importante para evitar cuelgues en el entorno gráfico
    restart: unless-stopped
-->
Abro la terminal en visual code de la carpeta que he creado y ejecuto docker-compose up -d 
<img width="802" height="900" alt="Captura" src="images2/Captura de pantalla 2026-05-08 095622.png" />

Para verificar que los contenedores estan funcionando uso docker ps
<img width="802" height="900" alt="Captura" src="images/Captura de pantalla 2026-05-08 092630.png" />

## *Fase de Ejecución*
### *Paso A (Conexión Inicial)*
Me conecto al contenedor utilizando ssh alumno@localhost -p 2222 
<img width="802" height="900" alt="Captura" src="images/Captura de pantalla 2026-05-08 093926.png" />

Y la contraseña sistemas_informaticos
<img width="802" height="900" alt="Captura" src="images/Captura de pantalla 2026-05-08 092530.png" />

### *Paso B (Generación de Identidad)*
Para generar una llave utilizo ssh-keygen -t ed25519 -C "sergiogarcia.25@campuscamara.es"
<img width="802" height="900" alt="Captura" src="images/Captura de pantalla 2026-05-08 094330.png" />

### *Paso C (Transferencia)*
Para copiar la llave publica al servidor utilizo ssh-copy-id -p 2222 alumno@localhost
<img width="802" height="900" alt="Captura" src="images2/Captura de pantalla 2026-05-08 095703.png" />

## *RDP:* El Escritorio en tu Navegador
### *Conexión*
Abri el cliente de Escritorio Remoto en mi caso MSTSC por que estoy en Windows y en el apartado Equipo pongo localhost:3389 pero me da un error
<img width="802" height="900" alt="Captura" src="images/Captura de pantalla 2026-05-08 093306.png" />

Para solucionar este error voy al navegador y esscribo http://localhost:3000 que me lleva a un escritorio de Ubuntu dentro del navegador (por Apache Guacamole)

### *Prueba de éxito*
Para verificar que ha funcionado creo un archivo de texto en el escritorio que tiene de nombre PRUEBA_LOGRADA.txt
<img width="802" height="900" alt="Captura" src="images/Captura de pantalla 2026-05-08 093650.png" />
