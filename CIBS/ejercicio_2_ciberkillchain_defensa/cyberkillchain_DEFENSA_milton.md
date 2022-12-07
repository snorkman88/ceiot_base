# Ejercicio CiberKillChain - DEFENSA

Haga una copia de este documto

## Alumno

Milton Eduardo Sosa

## Enunciado

Armar una cyberkillchain usando técnicas de defensa para un escenario relacionado a tu trabajo práctico

## Datos trabajo práctico

[Propuesta de trabajo final](https://docs.google.com/document/d/1IioE45fTW75i2Lwmdsal7plzIytoQotzIfWNjiaH8rE/edit)

Mi trabajo final de la Especializacion se titula "Microservicios IoT para sensores autónomos sobre LoRaWAN"

El presente trabajo se conforma como continuidad del proyecto final de la CESE titulado Sistema de sensores autonomos para monitoreo de redes de distribución de baja tension mediante LoRaWAN. En este proyecto se buscó desarrollar un sistema embebido autónomo capaz de medir valores eficaces de corriente, detectar interrupciones en el servicio de distribución de energía y transmitir reportes a un centro de monitoreo.



**Arquitectura general del sistema**

La arquitectura monolitica adoptada en la CESE, al no seguir premisas de escalabilidad y flexibildiad, no es lo suficientemente robusta para realizar un despliegue a escala media ni ideal para potenciales integraciones con clientes que tienen diferentes niveles de servicio (SLA) contratado.

El nuevo diagrama de bloques de los BES a desarrollar se presenta en la Figura 1. Los servicios se ejecutarán cada uno de manera individual en un contenedor de entornos Docker y orquestado a traves de un archivo docker-compose, otorgando así modularidad y escalabilidad.

![Diagrama de bloques del sistema](https://github.com/snorkman88/ceiot_base/blob/master/CIBS/ejercicio_1_ciberkillchain_ataque/nueva_arquitectura_con_ingestion_REDIS.png)

## Resolución

**1 Reconnaissance**  
Para solucionar las actuales vulnerabilidades del hardware mencionadas en el ataque, será necesario realizar cambios tanto en el circuito esquemático como en el desarrollo del firmware.  

Por otro lado en el backend, sera necesario aplicar diferentes medidas tanto en la infraestructura que albergue a los servicios como a cada servicio de manera individual.

**2 Weaponization**  
Reemplazar el lenguaje de desarrollo del embebido por uno que sea compilado y no interpretado.  

Asegurarse de utilizar las ultimas versiones y actualizaciones de seguridad para cada servicio.

**3 Delivery**  
Nodo 
- Eliminar pines que otorguen acceso directo al puerto serie/depuración SWD/JTAG.  
- Habilitar depuración a través de un servidor WiFi solamente luego de un mensaje downlink recibido desde el servidor de aplicacion.  
- Habilitar fusibles de OTP One Time Programming  

Backend  
- Agregar autenticación en el recuperador HTTP mediante keys.  
- Utilizar cifrado TLS v1.3 y manejo de certificados mediante una autoridad dedicada.  
- Considerar el uso de un firewall  

**4 Exploitation**  
Implementar un sistema de renovación obligatoria de keys del recuperador HTTP de manera periódica para todos los clientes.  

**5 Installation**  
No permitir cambios en ficheros del sistema operativo.  


**6 Command and Control**  
Implementar un sistema que implique la intervención de mayor jerarquía al momento de aumentar los permisos de un usuario.


**7 Actions on Objectives**  
Implementar un riguroso sistema de logs de auditoria y reportes que alerte al personal competente acerca de intentos de cambios en los atributos de cada cliente.