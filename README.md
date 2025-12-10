Alpha Protocol Monitor (V16)

![Estado](https://img.shields.io/badge/ESTADO-PRODUCCIÓN-green?style=for-the-badge)
![Seguridad](https://img.shields.io/badge/OPSEC-EMPRESARIAL-blue?style=for-the-badge)
![Tech](https://img.shields.io/badge/TECH-PYTHON%20%7C%20SOCKETS%20%7C%20WIN32-orange?style=for-the-badge)

> **Muestra Arquitectónica** de un agente de vigilancia de red automatizado, desarrollado para el monitoreo de infraestructura crítica empresarial.

---

## Descripción del Proyecto

**Alpha Monitor** es un agente tipo "Watchdog" (Perro Guardián) diseñado para reemplazar las verificaciones manuales de disponibilidad de red. Opera como un servicio binario compilado que monitorea puertos TCP críticos en tiempo real y detona alertas automatizadas vía MS Outlook al detectar una conexión exitosa.

A diferencia de las soluciones RPA tradicionales que dependen de navegadores web (automatización GUI lenta y pesada), esta herramienta interactúa directamente con la **pila TCP/IP** utilizando Python Sockets, resultando en un consumo de recursos 99% menor y cero dependencia de sitios web externos.

## Arquitectura Técnica

El sistema está construido sobre una **Arquitectura de Bucle Resiliente** con tres fases centrales:

```mermaid
graph TD
    A["INICIO: Interruptor Hombre Muerto"] -->|"Sin Input (5s)"| B("Auto-Lanzamiento Task Scheduler")
    A -->|"Tecla '2' Detectada"| C("Panel CLI de Administración")
    
    C -->|"Actualizar JSON"| D["Archivo de Configuración"]
    B -->|"Leer Configuración"| D
    
    B --> E{"Verificar Puerto TCP"}
    E -->|"Cerrado/Sin Respuesta"| F["Esperar y Reintentar (Bucle Infinito)"]
    F --> E
    
    E -->|"CONEXIÓN DETECTADA"| G["Detonar Protocolo de Alerta"]
    
    G --> H["Escribir Bitácora Local"]
    G --> I["Enviar Correo Outlook"]
    
    I --> J["Auto-Terminación"]
