# Windows Defender Firewall con Seguridad Avanzada Rules

Creación de reglas especializadas para mitigar y bloquear tráfico malicioso ante un posible ataque. 

Este proyecto se centra únicamente en crear reglas y comprender cómo funcionan.

### Tecnologías que vamos a usar para el proyecto:

- Windows Defender Firewall with Advanced Security
- PowerShell
- CMD
- netstat
- Test-NetConnection

### Pasos del Proyecto

1. El estado de Firewall lo pondrémos en privado, ya que estoy en la red de mi casa

2. Bloqueamos Telnet, ya que no suele usar cifrado, y alguien que sepa utilizar wireshark nos puede capturar el paquete y esto realmente podría ser peligroso dependiendo la información que manejaremos sobre ese paquete "descuidado por asi decirlo". Más alla de que puede estar bloqueado realmente quiero que nos aseguremos y mitiguemos ese puerto.

3. Luego Bloquearemos FTP

#### ¿Por qué bloquear FTP?

Porque, igual que Telnet, FTP tampoco cifra la información. Por ejemplo, si subes un archivo: archivo.pdf
y además escribes tu usuario y contraseña puede viajar en texto plano.

Hay que recalcar que si existe un servidor FTP, cualquier persona podría intentar:

- Conectarse.
- Adivinar contraseñas (fuerza bruta).
- Buscar vulnerabilidades del servidor.
- Descargar archivos si la configuración es incorrecta.

4. Lo siguiente Activar Registros (logging), en la sección de inicio de sesión en las propiedades en Perfil Público aplicaremos estas opciones:

- Registrar paquetes descartados:   SI
- Registrar conexiones correctas:   SI

¿Por qué registrar paquetes descartados?

Porque como acabamos de crear reglas como:

Bloquear Telnet (23).
Bloquear FTP (21).

Cuando alguien intente usar esos puertos, el firewall dejará una evidencia en el archivo de log. Por ejemplo, si un equipo intenta conectarse al puerto 23, el firewall registrará algo equivalente a:
- "La IP 192.168.1.10 intentó conectarse al puerto 23 de mi equipo a las 20:15, y la conexión fue bloqueada."
