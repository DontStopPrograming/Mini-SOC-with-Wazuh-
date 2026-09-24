# Mini-SOC-with-Wazuh-
Detection Attacks SSH and MITRE ATT&amp;CK

![Wazuh](https://img.shields.io/badge/Wazuh-4.13.1-blue)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-T1110-red)
![License](https://img.shields.io/badge/License-MIT-green)

## 📑 Índice

1. [Descripción General](#-descripción-general)
2. [Objetivos](#-objetivos)
3. [Arquitectura del Laboratorio](#️-arquitectura-del-laboratorio)
4. [Tecnologías Utilizadas](#️-tecnologías-utilizadas)
5. [Configuración Clave](#️-configuración-clave-del-laboratorio)
6. [Guía de Implementación](#-guía-de-implementación)
7. [Evidencia de Detección](#-evidencia-de-detección)
8. [Resultados y Métricas](#-resultados-y-métricas)
9. [Casos de Uso Demostrados](#-casos-de-uso-demostrados)
10. [Lecciones Aprendidas](#-lecciones-aprendidas)
11. [Troubleshooting](#-troubleshooting)
12. [Referencias y Recursos](#-referencias-y-recursos)
13. [Descargo de Responsabilidad](#️-descargo-de-responsabilidad)
14. [Autor](#-autor)
15. [Licencia](#-licencia)


## 📖 Descripción General

Laboratorio práctico de Seguridad de la Información que implementa un **mini SOC (Security Operations Center)** funcional utilizando **Wazuh SIEM/XDR** sobre Docker. El proyecto demuestra el ciclo completo de detección de amenazas: desde la implementación del agente en un endpoint Linux Mint, hasta la detección de un ataque de fuerza bruta SSH y la correlación con el framework **MITRE ATT&CK**.


## 🎯 Objetivos

- ✅ **Implementar** Wazuh SIEM en contenedores Docker
- ✅ **Configurar** agente enpoint en Linux Mint para recoleccion de logs
- ✅ **Simular** ataque de fuerza bruta SSH de forma controlada
- ✅ **Crear** regla personalizada con mapeo MITRE ATT&CK T1110
- ✅ **Validar** la deteccion y visualizacion en el dashboard
- ✅ **Documentar** el proceso completo de la forma reproducible

## 🏗️ Arquitectura del Laboratorio

### Diagrama de Componentes





### Diagrama de Flujo de Ataque y Defensa






### Inventario de Activos

| Rol | Sistema Operativo | Software | Función |
|-----|------------------|----------|---------|
| **Servidor SOC** | Ubuntu Server | Docker + Wazuh (Manager, Indexer, Dashboard) | Centralización, análisis y visualización |
| **Endpoint Monitorizado** | Linux Mint | Wazuh Agent + rsyslog | Recolección de logs y detección local |
| **Atacante (simulado)** | Linux Mint (localhost) | sshpass | Generación de eventos de fuerza bruta |

### Tecnologías Utilizadas

| Categoría | Herramienta | Versión |
|-----------|-------------|---------|
| **SIEM/XDR** | Wazuh Manager + Indexer + Dashboard | 4.13.1 |
| **Contenedores** | Docker + Docker Compose | Ultima estable
| **Endpoint**| Linux Mint | Basado en Ubuntu 24.04 |
| **Agente** | Wazuh Agent | 4.13.1 |
| **Logging** | rsyslog | Sistema |
| **Ataque** | sshpass | Sistema |
| **Framework** | MITRE ATT&CK | v14 |


## Configuracion Clave

### Regla Personalizada (`config/wazuh_cluster/local_rules.xml`)

<group name="local,syslog,sshd,">
  <rule id="100002" level="10" frequency="8" timeframe="120" ignore="60"> 
    <if_matched_sid>5712</if_matched_sid>
    <same_srcip />
    <description>SSH brute force dectectado (regla personalizada con MITRE).</description>
    <mitre>
      <id>T1110</id>
      <tactic>Credential Access</tactic>
      <technique>Brute Force</technique>
    </mitre>
  </rule>
</group>
 





