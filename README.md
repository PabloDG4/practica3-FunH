# Tarea SSH y SCP

## **1. Configuración Inicial**

### Crear dos máquinas virtuales: Máquina A y Máquina B
- Configura ambas máquinas en la misma red virtual para garantizar comunicación mutua.
- Asigna los puertos 2222 y 2223 a la máquina A y B, respectivamente.

  ![photo](imagenes/Captura1.png)
  ![foto](imagenes/Captura2.png)

### Instalar el servicio SSH
Ejecuta en ambas máquinas:
```bash
sudo apt update
sudo apt install openssh-server
```

---

## **2. Crear usuarios Alex y Brais**

### En Máquina A:
```bash
sudo adduser alex
```
Configura la contraseña y completa la información solicitada.

### En Máquina B:
```bash
sudo adduser brais
```

---
  ![photo](imagenes/Captura3.png)
  
## **3. Conexión SSH de Máquina A a Máquina B**

### Desde Máquina A:
```bash
ssh brais@<IP_B> -p 2223
```
- `<IP_B>`: Dirección IP de la Máquina B.
- Este comando inicia una conexión SSH, y el parámetro `-p` especifica el puerto.

### Explicación:
Al conectarte por primera vez, SSH crea una entrada en el archivo `~/.ssh/known_hosts` en Máquina A. Este archivo almacena la clave pública del servidor (Máquina B) para futuras conexiones seguras.

---
  ![photo](imagenes/Captura4.png)
  ![photo](imagenes/Captura5.png)

## **4. Transferencia de Archivos**

### En Máquina A:
#### Crear directorio y archivo:
```bash
mkdir /tmp/prueba
echo "Contenido de prueba" > /tmp/prueba/prueba.txt
```
#### Enviar el directorio a Máquina B:
```bash
scp -P 2223 -r /tmp/prueba brais@<IP_B>:/tmp
```

### En Máquina B:
#### Crear directorio y archivo:
```bash
mkdir /tmp/prueba2
echo "Contenido de prueba 2" > /tmp/prueba2/prueba2.txt
```
#### Enviar el directorio a Máquina A:
```bash
scp -P 2222 -r /tmp/prueba2 alex@<IP_A>:/tmp
```

---

  ![photo](imagenes/Captura6.png)
  
## **5. Transferencia al ordenador anfitrión**

### Desde Máquina A:
Transfiere los directorios al escritorio del anfitrión:
```bash
scp -P 2222 -r /tmp/prueba /tmp/prueba2 usuario_anfitrion@<IP_Anfitrion>:/home/usuario_anfitrion/Escritorio
```

### Desde Máquina B:
#### Crear directorio con 200 archivos:
```bash
mkdir /tmp/prueba3
for i in {1..200}; do echo "Archivo $i" > /tmp/prueba3/archivo$i.txt; done
```
#### Transferir al anfitrión:
```bash
scp -P 2223 -r /tmp/prueba3 usuario_anfitrion@<IP_Anfitrion>:/home/usuario_anfitrion/Escritorio
```

---
  ![photo](imagenes/Captura7.png)
  ![photo](imagenes/Captura8.png)
  ![photo](imagenes/Captura9.png)
  
## **6. Configuración de Claves SSH**

### En Máquina A:
#### Generar par de claves:
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N "servidorssh"
```
Esto genera las claves pública (`id_rsa.pub`) y privada (`id_rsa`).

#### Copiar la clave pública al servidor (Máquina B):
```bash
ssh-copy-id -p 2223 brais@<IP_B>
```

### Verificar conexión sin contraseña:
```bash
ssh brais@<IP_B> -p 2223
```

---
  
  ![photo](imagenes/Captura10.png)
  ![photo](imagenes/Captura11.png)
  ![photo](imagenes/Captura12.png)
  ![photo](imagenes/Captura13.png)
  ![photo](imagenes/Captura14.png)
  
## **7. Documentación en GitHub**

### Crear un repositorio:
- Nombre del repositorio: `tareasFH`
- Dentro del repositorio, crea una carpeta `tarea_SSH_SCP`.

### Subir archivos:
1. Inicializa el repositorio:
   ```bash
   git init
   git add .
   git commit -m "Tarea SSH y SCP"
   git branch -M main
   git remote add origin <URL_DEL_REPOSITORIO>
   git push -u origin main
   ```

2. Genera un archivo ZIP:
   ```bash
   zip -r tarea_SSH_SCP.zip tarea_SSH_SCP/
   ```

---

## **8. Entrega**


