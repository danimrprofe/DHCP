# DHCP
Perfiles de DHCP variados

# Configuración de interfaz
Se debe configurar la dirección de escucha en 
```
/etc/default/isc-server
```
# Comprobar que la ip coincide en todas las configuraciones

La subred de dhcp que queremos definir, especificada en el archivo de configuración dhcpd.conf tiene que coincidir con la IP asignada (estática) al servidor.
