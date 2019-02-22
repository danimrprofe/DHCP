# DHCP
Perfiles de DHCP variados

# Configuración de interfaz
Se debe configurar la dirección de escucha en 
```
/etc/default/isc-server
```
# Comprobar que la ip coincide en todas las configuraciones

La subred de dhcp que queremos definir, especificada en el archivo de configuración dhcpd.conf tiene que coincidir con la IP asignada (estática) al servidor.

# Problemas de conextividad
Comprobaciones de conectividad a Internet
## Ping a dominio
Ping a google. Si no funciona, seguir
## Ping a servidores DNS de google
Ping a 8.8.8.8. Si responde, puede ser problema de DNS
Revisar DNS en /etc/network/interfaces
Si no responde, ping a puerta de enlace
## Ping a puerta de enlace
Si no responde, seguir

## Revisar configuración de adaptadores de red
* Adaptadores NAT: MV tienen salida a internet, pero las MV no se ven entre ellas
* RED NAT: MV tienen salida a internet, y se ven entre ellas.
- Desde dentro de la RED NAT podemos acceder a fuera
- Desde fuera de la RED NAT no podemos conectar si no configuramos port forwarding
* Adaptador puente: Conecta a la misma red que el anfitrión, a través de una de sus tarjetas de red reales. Siempre que la puerta de enlace sea de un router conectado a internet. 
## Comprobaciones de conectividad entre equipos
Ping de un equipo a otro debería funcionar. Si no funciona, comprobad que están en la misma red (comparad IPs y modos de funcionamiento)

Deshabilitar y habilitar interfaz
```
ifdown enp0s3 
ifup enp0s3
```
## Reiniciar el servicio de red

Solo funcionan si la interfaz aparece en /etc/network/interfaces
Reiniciar servicio de red
```
systemctl restart networking.service
```
## Comprobar si la interfaz está activa 
Comprobar que la interfaz aparece en como activada. Para ver solo las interfaces activas:
```
ifconfig 
```
Para comprobar todas las intefaces de red que tiene la MV, aunque no estén activas:
```
ifconfig -a 
```
## Cambio de adaptador en Virtualbox
Si se ha cambiado el adaptador o se ha añadido nuevo desde Virtualbox, debemos comprobar /etc/network/interfaces para la nueva interfaz
```
auto enp0s8
iface enp0s8 inet dhcp
```
Apagar la interfaz con ifdown y levantar la interfaz con ifup
```
ifup enp0s8
```
Es posible que tengamos que reiniciar el sistema.
## El adaptador está conectado?

Puede pasar que el adaptador esté activado, tenga IP, pero no esté habilitado desde Virtualbox.

Es posible que no esté habilitado. Sucede sobretodo cuando ifup no consigue contactar con el servidor DHCP

