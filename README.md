# Voces españolas personalizadas para Dreame

Paquetes de voces españolas personalizadas para robots Dreame.

Este proyecto permite instalar voces personalizadas sobre el paquete de voces GLADOS.

## Contenido

- voice_pack_espanol.tar.gz — paquete de voces españolas
- voice_pack_xiana.tar.gz — voz femenina personalizada XIANA

---

## IMPORTANTE: GLADOS ES NECESARIO

Antes de instalar las voces de este repositorio, el robot debe tener instalado el paquete de voces GLADOS.

El directorio debe existir:

/data/personalized_voice/GLADOS

Si esta carpeta no existe, NO continúes con la instalación de XIANA.

## Instalar GLADOS

El paquete de voces GLADOS original se encuentra en el proyecto de Findus23:

https://github.com/Findus23/voice_pack_dreame

Primero instala el paquete de voces correspondiente a tu robot siguiendo las instrucciones de ese proyecto.

Después comprueba que existe:

/data/personalized_voice/GLADOS

Cuando GLADOS esté instalado correctamente, puedes continuar con esta guía.

---

## Como funciona

Las voces personalizadas de este repositorio no se instalan como un paquete independiente.

Se sustituyen los archivos .ogg existentes dentro de:

/data/personalized_voice/GLADOS

El proceso es:

GLADOS
  |
  v
/data/personalized_voice/GLADOS
  |
  v
copia de seguridad
  |
  v
sustitucion de archivos .ogg
  |
  v
voz personalizada XIANA

---

## Requisitos

Necesitas:

- Un robot Dreame compatible.
- Acceso SSH al robot.
- Un ordenador Linux, Raspberry Pi o similar.
- La direccion IP del robot.
- Una clave SSH si el robot utiliza autenticacion mediante clave.

---

## 1. Comprobar GLADOS

Conectate al robot mediante SSH:

ssh -i /ruta/a/tu/clave root@IP_DEL_ROBOT

Ejemplo:

ssh -i /home/pi/Documents/j69495894cbde7.id_rsa root@192.168.1.33

Comprueba que GLADOS existe:

ls -ld /data/personalized_voice/GLADOS

Comprueba el numero de archivos de voz:

find /data/personalized_voice/GLADOS -type f -name "*.ogg" | wc -l

Si la carpeta no existe, detente e instala primero GLADOS.

---

## 2. Hacer una copia de seguridad

Antes de modificar las voces originales:

cp -a /data/personalized_voice/GLADOS /data/personalized_voice/GLADOS_BACKUP

Comprueba la copia:

ls -ld /data/personalized_voice/GLADOS_BACKUP

---

## 3. Copiar XIANA al robot

Desde el ordenador ejecuta:

scp -O -i /ruta/a/tu/clave voice_pack_xiana.tar.gz root@IP_DEL_ROBOT:/tmp/

Ejemplo:

scp -O -i /home/pi/Documents/j69495894cbde7.id_rsa voice_pack_xiana.tar.gz root@192.168.1.33:/tmp/

El parametro -O puede ser necesario porque algunos robots no disponen de /usr/libexec/sftp-server.

---

## 4. Extraer XIANA

En el robot:

mkdir -p /tmp/xiana

tar -xzf /tmp/voice_pack_xiana.tar.gz -C /tmp/xiana

Comprueba las voces:

find /tmp/xiana -type f -name "*.ogg" | head -50

---

## 5. Instalar XIANA

Si los archivos .ogg estan directamente dentro de /tmp/xiana:

cp -f /tmp/xiana/*.ogg /data/personalized_voice/GLADOS/

Esto sustituye las voces de GLADOS por las voces personalizadas XIANA.

No se modifica el firmware del robot.

---

## 6. Comprobar la instalacion

Comprueba el numero de voces:

find /data/personalized_voice/GLADOS -type f -name "*.ogg" | wc -l

Comprueba una voz:

ls -lh /data/personalized_voice/GLADOS/1.ogg

---

## 7. Reiniciar

Cuando hayas terminado:

reboot

Despues del reinicio, el robot deberia utilizar las voces personalizadas XIANA.

---

## Restaurar las voces originales

Si quieres volver a las voces originales de GLADOS:

rm -rf /data/personalized_voice/GLADOS

Restaurar la copia:

cp -a /data/personalized_voice/GLADOS_BACKUP /data/personalized_voice/GLADOS

Reiniciar:

reboot

---

## Voz XIANA

voice_pack_xiana.tar.gz contiene las voces femeninas personalizadas XIANA.

XIANA se instala sustituyendo los archivos .ogg utilizados por GLADOS.

---

## Voces españolas

voice_pack_espanol.tar.gz contiene el paquete de voces españolas preparado para este sistema.

---

## Compatibilidad

La estructura y los archivos de voz pueden variar dependiendo del modelo del robot y de la version del firmware.

Antes de realizar cualquier modificacion:

1. Comprueba que existe GLADOS.
2. Haz una copia de seguridad.
3. Comprueba que el paquete contiene archivos .ogg.
4. Sustituye unicamente los archivos de voz.
5. Reinicia el robot.

---

## Creditos

Voz personalizada femenina: XIANA

Proyecto comunitario para facilitar la instalacion de voces españolas personalizadas en robots Dreame.
