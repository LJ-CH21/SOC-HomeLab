# 🛡️ SOC Home Lab

## 🎯 Objetivo del Proyecto
Construir un entorno aislado de ciberseguridad (Home Lab) para desarrollar habilidades prácticas en administración de redes, análisis de logs (SIEM) y respuesta a incidentes.

## 🏗️ Arquitectura de Red
El laboratorio está virtualizado sobre VirtualBox y segmentado mediante un firewall de grado empresarial.
*   **Hypervisor:** Oracle VirtualBox
*   **Gateway / Firewall:** pfSense (IP: 192.168.1.1)
    *   **WAN:** Adaptador NAT (Salida a internet)
    *   **LAN:** Red Interna (`192.168.1.0/24`)
*   **Endpoints (Red Interna):**
    *   Windows 11 Pro (Víctima) - IP: 192.168.1.100
    *   Ubuntu Server 24.04 (SIEM Host) - IP: 192.168.1.102

## 🚀 Fases del Despliegue

### Fase 1: Enrutamiento y Aislamiento (pfSense)
*   Instalación de pfSense y configuración de interfaces WAN/LAN.
*   Habilitación de DHCP Server para la red interna.
*   *Troubleshooting:* Desactivación del bloqueo de redes RFC1918 en la interfaz WAN para permitir el tráfico desde el adaptador NAT del hypervisor.

### Fase 2: Despliegue del Endpoint (Windows 11)
*   Instalación de Windows 11 en la red interna.
*   *Troubleshooting:* Aplicación de bypass (OOBE\BYPASSNRO) para evadir el requisito de conexión a cuenta Microsoft y forzar la creación de un usuario local aislado.
*   Validación de asignación IP (DHCP) y conectividad ICMP (Ping).

### Fase 3: Infraestructura de Visibilidad (Ubuntu Server)
*   Despliegue de Ubuntu Server con LVM y OpenSSH habilitado.
*   *Troubleshooting:* Manejo del retraso visual de `cloud-init` durante el primer arranque para acceder al prompt de login.
