# SecureBox 🛡️

Network Security Appliance modular construido desde cero. Detecta y filtra tráfico malicioso en tiempo real mediante una arquitectura de firewall, IDS y SIEM integrados.

## Arquitectura

```mermaid
graph LR
    A[Internet] --> B[Ubuntu Server SecureBox]
    B -->|nftables firewall| C[Red interna protegida]
    C --> D[Ubuntu Desktop Victim<br/>Agente Wazuh]
    E[BlackArch Atacante] -.->|tráfico monitoreado| B
    B --> F[Suricata IDS]
    B --> G[Wazuh SIEM<br/>Manager + Indexer + Dashboard]
    F --> G
    D -.->|reporta eventos| G
```

## Stack técnico

- **Ubuntu Server 24.04** — sistema base del appliance
- **nftables** — firewall con reglas custom
- **Suricata** — IDS con reglas de detección propias
- **Wazuh** — SIEM (Manager + Indexer + Dashboard)
- **Python** — parser de logs (en progreso)
- **Node.js + Dashboard web** — panel de control propio (en progreso)

## Lo que hace

- Filtra tráfico de red con reglas de firewall personalizadas (nftables)
- Detecta intrusiones en tiempo real con reglas de Suricata propias
- Centraliza y correlaciona eventos de seguridad con Wazuh SIEM
- Monitorea endpoints remotos mediante agentes Wazuh
- Genera alertas ante comportamiento sospechoso o no autorizado

## Progreso

- [x] Firewall con nftables configurado y persistente
- [x] IDS Suricata detectando tráfico en tiempo real
- [x] Primera regla de detección personalizada (ICMP)
- [x] SIEM Wazuh desplegado (Manager + Indexer + Dashboard)
- [x] Agente Wazuh conectado en máquina víctima
- [ ] Primer ataque real correlacionado (Suricata + Wazuh)
- [ ] Parser de logs en Python
- [ ] Dashboard web propio
- [ ] API REST para control remoto
- [ ] Portabilidad (Raspberry Pi)

## Demo

### Fase 1 — Firewall + IDS detectando tráfico

Primeras alertas generadas por Suricata al aplicar reglas de detección de trazas ICMP, con el firewall nftables activo en el servidor.

<img width="521" height="244" alt="Alerta Suricata ICMP" src="https://github.com/user-attachments/assets/8daddaa0-b9e8-4467-980d-036509cc7eb1" />
<img width="661" height="154" alt="Alerta Suricata detalle" src="https://github.com/user-attachments/assets/922c03dc-67a6-4dcc-9aac-2b792b7e5c75" />

Aquí se observa cómo una traza ICMP enviada desde la máquina atacante es identificada por el servidor que tiene el firewall y Suricata activos, permitiendo detección temprana de accesos no autorizados según reglas pre-establecidas.

### Fase 2 — Reglas personalizadas de Suricata

Reglas configuradas en `local.rules` para identificar trazas ICMP dirigidas al servidor.

<img width="844" height="207" alt="local.rules Suricata" src="https://github.com/user-attachments/assets/3747af58-f0c9-44b6-a827-8f639b1086ee" />

### Fase 3 — Despliegue de Wazuh (SIEM)

Instalación de Wazuh como SIEM para la gestión centralizada de alertas. El dashboard es accesible desde la red interna a través del puerto 8443.

<img width="1409" height="809" alt="Wazuh Dashboard" src="https://github.com/user-attachments/assets/b419f11d-04e2-4ae4-a463-2534fd2ed3fc" />

Es importante destacar que el protocolo TCP por el puerto 443 estaba bloqueado por el firewall nftables por defecto, por lo que fue necesario habilitar explícitamente dicho puerto para permitir el acceso al dashboard.

<img width="1333" height="798" alt="Wazuh login y panel activo" src="https://github.com/user-attachments/assets/cb316326-d0c6-4b6a-9ed0-b07b9f5cb44e" />
<img width="1410" height="804" alt="Wazuh settings" src="https://github.com/user-attachments/assets/59caafd6-bb5d-44ec-bd37-8e6755247e9e" />

### Fase 4 — Agente en máquina víctima

Se desplegó una nueva máquina virtual (`ubuntu-desktop-victim`) con el agente Wazuh instalado, funcionando como endpoint monitoreado sobre el cual se ejecutarán los ataques desde la máquina atacante.

<img width="2045" height="1221" alt="Despliegue agente víctima" src="https://github.com/user-attachments/assets/edcd166c-f13b-4d80-b57c-01be676bf0b3" />

Vista del summary de endpoints conectados al manager de Wazuh, mostrando el único agente activo hasta el momento.

<img width="2044" height="559" alt="Summary endpoints Wazuh" src="https://github.com/user-attachments/assets/357ea7f7-388f-4773-8cae-1e27b6303991" />

---

**Próximo paso:** lanzar el primer ataque real desde la máquina atacante (BlackArch) y verificar la correlación entre Suricata y Wazuh en el dashboard, para documentar el primer incident report.
