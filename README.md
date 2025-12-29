# LeakLab


|                   | Detalle maquina original                        |
| ----------------- | ----------------------------------------------- |
| Autor             | Jaime Galvez Martinez                              |
| Dificultad        | Media                                         |
| Fecha de creación | 29/12/2025                                      |
| Fecha del writeup | 29/12/2025                                      |
| Maquina original  | LeakLab                                          |

### Paso 1: Reconocimiento - Escaneo de Puertos

 nmap -p- -sV 192.168.1.5

 <img width="950" height="412" alt="Captura de pantalla de 2025-12-29 21-41-40" src="https://github.com/user-attachments/assets/471f4c70-8be3-4728-b305-8923539dcbf7" />

Este comando permite:

-p-: escanear todos los puertos TCP (1–65535).

-sV: detectar la versión de los servicios que se están ejecutando.

192.168.1.5: dirección IP de la máquina vulnerable.

Como resultado del escaneo, se identifican los siguientes servicios activos:

Puerto 22/TCP: Servidor SSH en el puerto estandar.

Puerto 53/TCP: Servidor DNS (De Momento, no nos intersa)

Puerto 80/TCP: Servidor web Apache (HTTP).

Puerto 443/TCP: Servidor web Apache con HTTPS.

Puerto 9090/TCP: Puerto Por defecto de Prometeus.

Puerto 9100/TCP: Puerto Por defecto de Node Exporter.

2. Acceso no autorizado a Node Exporter

   <img width="1233" height="568" alt="Captura de pantalla de 2025-12-29 21-51-21" src="https://github.com/user-attachments/assets/eacff5c5-164c-4932-9835-5809fe051619" />


Durante el desarrollo del laboratorio se detectó que el servicio Node Exporter se encontraba expuesto y accesible sin ningún tipo de autenticación. Al acceder a la dirección IP del servidor seguida del puerto correspondiente (por defecto 9100), fue posible visualizar directamente la interfaz web del servicio sin necesidad de introducir credenciales.

Esta mala configuración supone una vulnerabilidad de seguridad, ya que <strong>Node Exporter proporciona métricas detalladas sobre el sistema, como el uso de CPU, memoria, disco, procesos y otra información sensible</strong> que podría ser utilizada por un atacante para realizar tareas de enumeración y planificación de ataques posteriores.

El acceso sin autenticación permite a cualquier usuario con conectividad a la red obtener información crítica del sistema, incumpliendo los principios básicos de seguridad como el control de acceso y la exposición mínima de servicios.
