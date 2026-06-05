# Industrial-Syslog-Sandbox
A virtualized network infrastructure lab built to simulate real-world industrial automation telemetry, network data packet routing, and critical system exception handling using a bridged hypervisor environment.
* **Logging Server (Host):** Windows 11 Engine running an open-source Syslog daemon listening on standard network port `UDP 514`.
* **Industrial Client Node (Virtual Machine):** Oracle VM VirtualBox running an isolated Ubuntu Linux instance (`Industrial-Client-01`).
* **Network Configuration:** Implemented a **Bridged Network Adapter** to bypass standard NAT limitations. This assigns an independent IP footprint to the virtual machine on the local subnet to communicate directly with the host (`192.168.1.4`), allowing authentic peer-to-peer network packet routing.


<img width="1240" height="388" alt="image" src="https://github.com/user-attachments/assets/d98e25ae-8cfa-40d2-9fd9-f592324d3245" />


<img width="716" height="277" alt="image" src="https://github.com/user-attachments/assets/a38a68a2-6628-43e5-b77b-50c0467c14f0" />

```text
┌──────────────────────────────────────┐
│  Ubuntu Linux VM (Client Node)       │
│  Hostname: Industrial-Client-01      │
└──────────────────┬───────────────────┘
                   │
                   │ [UDP Port 514] - Telemetry Packet
                   ▼
┌──────────────────────────────────────┐
│  Windows 11 Host (Control Room)     │
│  IP: 192.168.1.4                     │
│  Engine: Visual Syslog Server        │
└────────────────────────────────────── 

Implementation & Testing Phases
Phase 1: Inbound Logging Verification
Configured firewall traffic rules to permit inbound connection strings over UDP 514. Tested initial link connectivity by pushing a localized industrial connection fault string from the client node terminal using native packet utilities: logger -n 192.168.1.4 -P 514 "CRITICAL: Nucleus PTM connection timeout on Interface 3"

Phase 2: System Exception Severity Routing
To simulate true industrial automation dashboard errors, the command pipeline was updated to specify strict facility and severity parameters (-p user.alert). This forces the centralized server to parse, prioritize, and highlight critical environmental variance flags: logger -n 192.168.1.4 -P 514 -p user.alert "ALERT: Birdseye core temperature variance exceeded threshold on Unit 4"

Results & Verification
The centralized logging architecture successfully captured, categorized, and visually indexed the simulated machine telemetry in real-time. Low-level routine messages retained standard baseline styling, while high-priority machine exceptions automatically triggered critical red telemetry indicators on the control dashboard—demonstrating a successful root-cause diagnostic pipeline.

