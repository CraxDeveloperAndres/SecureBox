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
