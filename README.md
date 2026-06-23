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
[Aquí sube la captura de pantalla con la alerta detectada]
