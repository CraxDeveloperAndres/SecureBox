# SecureBox 🛡️

Network Security Appliance modular construido desde cero.
Detecta y filtra tráfico malicioso en tiempo real.

## Arquitectura
[Internet] → [SecureBox] → [Red interna protegida]

## Stack técnico
- Ubuntu Server 26.04
- nftables (firewall)
- Suricata (IDS)
- Python (parser de logs) — en progreso
- Wazuh (SIEM) — en progreso
- Node.js + Dashboard — en progreso

## Lo que hace
- Filtra tráfico con reglas de firewall personalizadas
- Detecta intrusiones en tiempo real con reglas propias
- Genera alertas cuando detecta comportamiento sospechoso

## Progreso
- [x] Firewall con nftables configurado
- [x] IDS Suricata detectando tráfico en tiempo real
- [x] Primera regla de detección personalizada
- [ ] Parser de logs en Python
- [ ] SIEM con Wazuh
- [ ] Dashboard web
- [ ] API REST para control remoto

## Demo
Primeras alertas con suricata aplicando reglas de deteccion de trazas icmp 
<img width="521" height="244" alt="image" src="https://github.com/user-attachments/assets/8daddaa0-b9e8-4467-980d-036509cc7eb1" />
<img width="661" height="154" alt="image" src="https://github.com/user-attachments/assets/922c03dc-67a6-4dcc-9aac-2b792b7e5c75" />

aqui podemos ver como una traza icmp desde la maquina atacante es identificada en el servidor virtual que tiene el firewall activo y el suricata para la deteccion temprana de sea accesos no autorizados o reglas de deteccion pre establecidas 

<img width="844" height="207" alt="image" src="https://github.com/user-attachments/assets/3747af58-f0c9-44b6-a827-8f639b1086ee" />

estas fueron las reglas pre establecidas en el local.rules de suricata para identificar trazas icmp que se le haga al servidor primero 

luego procedemos a instalar wazuh como (SIEM) a traves de su dashboard con el que podremos gestionar algunas alertas cuando algun atacante, una vez instalado el servicio podemos darnos cuenta que en la red interna por el puerto que activamos en este caso el 8443 nos permite ver el wazuh de manera visual 

<img width="1409" height="809" alt="image" src="https://github.com/user-attachments/assets/b419f11d-04e2-4ae4-a463-2534fd2ed3fc" />

cabe resaltar que como el protocolo tcp por el puerto 443 no permimte la entrada por nuestro firewall es indispensable activar dicho privilegio en nuestro firewall con nftables una vez entramos cons las credenciales podemos ver las cosas activas 
<img width="1333" height="798" alt="image" src="https://github.com/user-attachments/assets/cb316326-d0c6-4b6a-9ed0-b07b9f5cb44e" />

 tengo aun unos pequeños errores con las alertas pero esta en proceso de arreglarlo mientras tanto podemos ver el panel y algunos settings que tendriamos 

<img width="1410" height="804" alt="image" src="https://github.com/user-attachments/assets/59caafd6-bb5d-44ec-bd37-8e6755247e9e" />

con todo esto solucionado pasariamos a el dashboard web una vez solucionemos los inconvenientes con las alertas del wazuh 
