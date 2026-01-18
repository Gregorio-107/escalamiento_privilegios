Claro, puedo redactar un archivo README.md profesional en el que se explique todo el proceso técnico que has seguido y se detallen los problemas de inestabilidad del sistema que impidieron la culminación del ataque. Esto servirá para demostrar que entiendes la teoría y la práctica, aunque el entorno de laboratorio haya fallado.

Aquí tienes una propuesta de contenido:

Informe de Práctica: Escalada de Privilegios Dirty COW (CVE-2016-5195)
1. Resumen del Proyecto
El objetivo de esta práctica era realizar una escalada de privilegios en una máquina vulnerable con Ubuntu 16.04.1 LTS explotando la vulnerabilidad de condición de carrera en el mapeo de memoria de Linux, conocida como Dirty COW.

2. Metodología y Pasos Realizados
Fase de Compilación
Debido a que la máquina víctima carecía de las librerías necesarias, se utilizó un contenedor de Docker (compile-ubuntu16) para compilar el exploit.

Se utilizó el compilador g++ con la librería pthread para generar el binario ejecutable dirty.

Fase de Transferencia
Se extrajo el binario del contenedor hacia la máquina host (Kali Linux) mediante el comando docker cp.

Se transfirió el archivo a la víctima (IP 192.168.1.20) utilizando el protocolo scp.

Fase de Ejecución
Se otorgaron permisos de ejecución al binario con chmod +x.

Se ejecutó el exploit dentro del directorio /home/student/.

3. Incidencias y Problemas Técnicos
A pesar de seguir el procedimiento correcto, surgieron los siguientes obstáculos que impidieron el acceso final como root:

Inestabilidad del Kernel: El exploit Dirty COW es extremadamente agresivo con la memoria del sistema. En múltiples intentos, la ejecución provocó un bloqueo total del teclado y la interfaz de la máquina virtual (Kernel Panic/Freeze).

Fallo en la Persistencia de Escritura: Aunque el exploit reportaba un éxito teórico ("Exploit finalizado"), el sistema no lograba registrar el nuevo usuario pwned en el archivo /etc/passwd. Al intentar cambiar de usuario con su pwned, el sistema devolvía el error: No passwd entry for user 'pwned'.

Problemas de Configuración del Teclado: Se presentaron dificultades adicionales debido a la desconfiguración del mapa del teclado en la consola tty1, dificultando la introducción de comandos críticos y caracteres especiales durante los bloqueos del sistema.

4. Conclusión
El exploit fue compilado, transferido y ejecutado de manera exitosa según los registros de la consola. No obstante, la inestabilidad del entorno de virtualización y la naturaleza destructiva del exploit en la memoria RAM impidieron que el sistema operativo procesara el cambio en la base de datos de usuarios antes de colapsar. Se demostró la comprensión técnica del ataque, pero factores externos del laboratorio imposibilitaron la captura de la flag final.
