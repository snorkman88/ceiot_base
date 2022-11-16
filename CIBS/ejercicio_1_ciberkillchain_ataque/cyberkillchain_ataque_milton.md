# Ejercicio CiberKillChain - Ataque

Haga una copia de este documto

## Alumno

Milton Eduardo Sosa

## Enunciado

Armar una cyberkillchain usando técnicas de la matriz de Att&ck para un escenario relacionado a tu trabajo práctico

## Datos trabajo práctico

[Propuesta de trabajo final](https://docs.google.com/document/d/1IioE45fTW75i2Lwmdsal7plzIytoQotzIfWNjiaH8rE/edit)

Mi trabajo final de la Especializacion se titula "Microservicios IoT para sensores autónomos sobre LoRaWAN"

El presente trabajo se conforma como continuidad del proyecto final de la CESE titulado Sistema de sensores autonomos para monitoreo de redes de distribución de baja tension mediante LoRaWAN. En este proyecto se buscó desarrollar un sistema embebido autónomo capaz de medir valores eficaces de corriente, detectar interrupciones en el servicio de distribución de energía y transmitir reportes a un centro de monitoreo.



**Arquitectura general del sistema**

La arquitectura monolitica adoptada en la CESE, al no seguir premisas de escalabilidad y flexibildiad, no es lo suficientemente robusta para realizar un despliegue a escala media ni ideal para potenciales integraciones con clientes que tienen diferentes niveles de servicio (SLA) contratado.

El nuevo diagrama de bloques de los BES a desarrollar se presenta en la Figura 1. Los servicios se ejecutarán cada uno de manera individual en un contenedor de entornos Docker y orquestado a traves de un archivo docker-compose, otorgando así modularidad y escalabilidad.

![Diagrama de bloques del sistema](nueva_arquitectura_con_ingestion_REDIS.jpg)

## Resolución

**1 Reconnaissance**  
Actualmente el sistema posee dos puntos debiles claramente identificables. Uno en el nodo y el otro en el recuperador HTTP utilizado para la integracion con la red LoRaWAN.

**2 Weaponization**  
Nodo  
Mediante un adaptador USB-UART y un terminal serie, se podria recuperar el codigo firmware y las credenciales LoRaWAN. Con las credenciales se prepara un nuevo codigo adulterado y luego se lo despliega.

Backend
- Replay attack
- Plain text recovery
- Mensajes maliciosos  
https://www.cyber-threat-intelligence.com/publications/IoTDI2018-LoraWAN.pdf


**3 Delivery**  
Nodo  
El atacante deberia conectarse nuevamente al puerto serie del embebido y bajar el codigo firmware. A partir de alli puede enviar datos de lecturas erroneas para indicar falsas alertas en el backend y frontend.

Backend  
Actualmente la integracion HTTP no esta cifrada motivo por el cual todo el trafico viaja en texto plano entre la red LoRaWAN y el recuperador.
Haciendo captura de paquetes se podria recuperar la key que se utiliza para autenticarse contra la API HTTP. 

**4 Exploitation**  

En el caso de poder recuperar la key utilizada para autenticarse contra la API, se crearian nuevas credenciales con mayores atributos.

**5 Installation**  
En el nodo seria necesario reflashear el firmware con el codigo malicioso.
En el caso del backend sera al obtener permisos de admin, el control sobre los datos en la base de datos seria total.


**6 Command and Control**  
Siempre asegurandose de que no se ha detectadola intrusion, se roban los datos de cada cliente guardados en la base de datos y se empieza con el ataque a la base de datos. Ademas se cambian los permisos y niveles de acceso para clientes ya existentes generando un denial of service.

**7 Actions on Objectives**  
Intentar obtener datos confidenciales del embebido tales como las credenciales LoRaWAN.  
Obtener los clientes del sistema.  
Crear clientes falsos con niveles de privilegio admin.  