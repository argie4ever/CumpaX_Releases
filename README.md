<p align="center">
  <img width="240" height="240" alt="CumpaX_logo" src="https://github.com/user-attachments/assets/6c88ae87-6aca-4bf4-8b60-abb7ddd62d08" />
</p>


# Cumpa X

[![Release](https://img.shields.io/badge/Release-v2.0.0-blue?style=for-the-badge)](https://github.com/arielledesmabecerra/Cumpa_X_Releases/releases/latest)
[![Platform](https://img.shields.io/badge/Platform-macOS%2014.0%2B-000000?style=for-the-badge&logo=apple)](https://github.com/arielledesmabecerra/Cumpa_X_Releases/releases/latest)
[![Apple Silicon & Intel](https://img.shields.io/badge/Architecture-Universal%20Binary-gray?style=for-the-badge&logo=apple)](https://github.com/arielledesmabecerra/Cumpa_X_Releases/releases/latest)
[![Cafecito](https://img.shields.io/badge/Cafecito-Argentina-blue?style=for-the-badge&logo=coffee)](https://cafecito.app/arielledesmabecerra)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-Donar_USD-ff5e5b?style=for-the-badge&logo=ko-fi)](https://ko-fi.com/arielledesmabecerra)

---

### ☕ Apoya el proyecto / Support Independent Development

Cumpa X es una herramienta de código abierto y distribución gratuita para editores, documentalistas y asistentes de montaje. Si optimiza tu tiempo o el flujo de trabajo de tu productora, puedes colaborar para sostener su desarrollo continuo:

- 🇦🇷 **Argentina (Transferencia bancaria / Mercado Pago en ARS):**  
  👉 [**Invitar un Cafecito**](https://cafecito.app/arielledesmabecerra)

- 🌎 **Internacional (Tarjeta de crédito / Débito / PayPal en USD):**  
  👉 [**Support on Ko-fi**](https://ko-fi.com/arielledesmabecerra)

---

## 🇪🇸 Descripción General

**Cumpa X** es una suite de automatización, ingesta, conforming e interoperabilidad para **Apple Final Cut Pro (FCPX)**. Resuelve los cuellos de botella más críticos de la línea de tiempo magnética al tender puentes directos hacia suites de corrección de color (**DaVinci Resolve**), mezcla de sonido profesional (**Avid Pro Tools**) y entornos de efectos visuales (**OpenTimelineIO**), eliminando la dependencia histórica de utilidades de terceros.

### 🚀 Módulos y Funcionalidades Principales

#### 1. Sala de Ingesta Inteligente de Tarjetas de Cámara (`MediaIngestView`)
- **Escaneo Multi-Tarjeta:** Procesamiento simultáneo de estructuras de cámara (Sony XAVC, Canon XF, Panasonic, ARRI, RED, Blackmagic y dispositivos iPhone).
- **Protección Anti-Colisión:** Identificación determinista con UMID/UUID y asignación automática de *Reel/Tape* por nombre de tarjeta para evitar conflictos ante nombres idénticos (ej. múltiples `C0001.MP4`).
- **Metadatos y Sidecars:** Vinculación de XMLs de cámara, *Shot Marks* y proxies, filtrando carpetas técnicas (`CLIP`, `M4ROOT`, `PRIVATE`) para generar colecciones de *Keywords* limpias en FCPXML 1.10.
- **Inyección Lossless ProApps:** Escritura atómica de metadatos nativos Apple (`moov -> meta -> mdta`) en contenedores QuickTime/MP4 preservando la pista de video bit a bit.
- **Detección Determinista de Timecode:** Clasificación precisa del origen temporal (pista `tmcd`, fecha de creación en iPhone/iPad o referencia BWF en audio).

#### 2. Interoperabilidad AAF Bidireccional para Avid Pro Tools (`UniversalExportView`)
- **Exportación Sample-Accurate (CFBF v3):** Serialización binaria directa (SMPTE ST 2001-1 / AMWA AS-01) a frecuencia de muestreo nativa (ej. 48.000 Hz) con soporte NTSC Drop/Non-Drop Frame, eliminando micro-gaps y desfases de fase.
- **Preservación de Clip Gain:** Conversión logarítmica entera pura de niveles de volumen a metadatos nativos de ganancia para Pro Tools y DaVinci Resolve.
- **3 Modalidades de Medios:** *Vinculado* (referencia directa en disco con iXML/BEXT), *Consolidado a Carpeta con Manijas* (colas configurables de 12, 24 o 48 frames) y *Embebido* (flujos PCM dentro del contenedor AAF), acompañados de un informe de entrega en Markdown (`ConversionReport`).
- **Importación Nativa AAF $\to$ FCPXML 1.10:** Ingesta de sesiones de Pro Tools o Media Composer con extracción automática de audio embebido e inferencia de roles nativos de FCPX.

#### 3. Sincronización de Roles Browser $\to$ Timeline (`RoleCascaderView`)
- Propaga automáticamente roles y sub-roles de video y audio asignados en el Browser de Eventos hacia secuencias en el Timeline, recorriendo clips conectados, sonido directo sincronizado (`<sync-clip>`) y multicámaras (`<mc-clip>`).

#### 4. Interoperabilidad OpenTimelineIO (`.otio`) y Exportador a Pistas (`XMEML v4`)
- **OpenTimelineIO Bidireccional:** Importación nativa de secuencias `.otio` a proyectos magnéticos FCPXML 1.10 y exportación con intercalado matemático de `Gap.1` y subpistas paralelas no colisionantes.
- **Exportador a Pistas Cartesianas (`XMEML v4`):** Convierte líneas de tiempo magnéticas en pistas fijas (`V1`, `V2`... / `A1`, `A2`...) para Adobe Premiere Pro y DaVinci Resolve, conservando reencuadres (*Basic Motion*), niveles, paneos, metadatos de rodaje y supresión inteligente de audio *scratch* de cámara.

#### 5. Aplanado Multicámara Avanzado (*Flatten Multicam*)
- Sustituye contenedores `<mc-clip>` por cortes directos en la línea de tiempo principal o desde clips autónomos del navegador de eventos.
- **Modo Pistas Apiladas (*Explode All Angles*):** Apila todos los ángulos sincronizados en carriles paralelos (`V1`, `V2`, `V3`...) para revisión multi-ángulo, además de incluir pista de referencia A/B (conmutable con tecla `V`) y desempaquetado de micrófonos discretos sin micro-cortes.

#### 6. Transcripciones, Sesión Global Unificada y Conectividad FCPX
- **Transcripciones y Minutados:** Convierte guiones y minutados (`.txt`, `.md`) en colecciones de *Keywords* por rango y secuencias de *Primer Corte (Rough Cuts)* agrupadas en un evento limpio, con control de desfase de timecode (`tcStart`).
- **Sesión Global Unificada y Barra Persistente:** Un único proyecto activo compartido entre todas las salas con inspección técnica instantánea, aritmética temporal de 128 bits (`Int128`), validación de seguridad preflight, actualización automática integrada y envío/captura en 1 clic con Final Cut Pro.

### Requisitos del Sistema
- **Sistema Operativo:** macOS 14.0 (Sonoma) o superior.
- **Apple Final Cut Pro:** Versión 10.6 o superior.
- **Arquitectura:** Binario universal nativo para **Apple Silicon (M1/M2/M3/M4)** y procesadores **Intel**.

### Instalación
1. Descarga el instalador `Cumpa_X_v2.0.0_macOS.zip` desde los enlaces inferiores o la sección de [Releases](https://github.com/arielledesmabecerra/Cumpa_X_Releases/releases/latest).
2. Arrastra `Cumpa X.app` a tu carpeta de **Aplicaciones**.
3. **Primera ejecución:** Haz clic derecho (o `Control + Clic`) sobre la aplicación y selecciona **Abrir** para confirmar la excepción de seguridad de macOS.

---

## 🇺🇸 Overview

**Cumpa X** is a specialized automation, camera ingest, conforming, and interoperability suite for **Apple Final Cut Pro (FCPX)**. It eliminates magnetic timeline bottlenecks by establishing direct bridges to color grading (**DaVinci Resolve**), professional audio mixing (**Avid Pro Tools**), and visual effects pipelines (**OpenTimelineIO**).

### 🚀 Key Modules & Capabilities

- **Smart Camera Card Ingest Room (`MediaIngestView`):**
  * Batch scans multiple camera card roots simultaneously (Sony XAVC, Canon XF, Panasonic, ARRI, RED, Blackmagic, and iPhone).
  * Deterministic collision protection (UMID/UUID + automatic card-based Reel/Tape assignment) for duplicate filenames (e.g., multiple `C0001.MP4`).
  * Links camera XMLs, Shot Marks, and proxies into clean FCPXML 1.10 keyword collections, with lossless Apple ProApps metadata injection (`moov -> meta -> mdta`) and deterministic timecode source detection.
- **Bidirectional Native AAF for Avid Pro Tools (`UniversalExportView`):**
  * Sample-accurate binary OLE Compound File (CFBF v3) generation (SMPTE ST 2001-1 / AMWA AS-01) at native sample rates (e.g., 48,000 Hz) with NTSC Drop/Non-Drop Frame support and integer-exact Clip Gain preservation.
  * Supports *Linked*, *Consolidated with Handles* (12, 24, 48 frames), and *Embedded* media modes, plus automated Markdown turnover reports.
  * Native `.aaf` to FCPXML 1.10 import with automatic embedded PCM audio unpacking and FCPX role inference.
- **Role Cascader (`RoleCascaderView`):**
  * Automatically propagates audio and video roles/sub-roles from Event Browser clips down to timeline cuts across secondary storylines, `<sync-clip>`, and `<mc-clip>` setups.
- **Bidirectional OpenTimelineIO (`.otio`) & Track Exporter (`XMEML v4`):**
  * Native `.otio` ingest and export with continuous rational `Gap.1` interleaving and non-colliding parallel subtracks.
  * Cartesian track export (`V1`, `V2`... / `A1`, `A2`...) for Adobe Premiere Pro and DaVinci Resolve preserving motion transforms, audio levels, pan, shooting metadata, and camera scratch suppression.
- **Advanced Multicam Flattening:**
  * Unwraps `<mc-clip>` containers into discrete timeline cuts or directly from standalone Browser multicam clips.
  * Offers an *Explode All Angles* mode for parallel multi-angle stacking, an A/B reference lane (toggle with `V`), and discrete audio unbundling.
- **Transcripts, Unified Global Session & Direct FCPX Connectivity:**
  * Converts timecoded `.txt`/`.md` transcripts into range-based Keywords and Rough Cut timelines packaged into a clean single event.
  * Unified global session across all rooms with persistent metadata inspection, 128-bit rational time math (`Int128`), preflight document safety checks, built-in auto-updater, and 1-click *Fetch from FCPX* / *Open in Final Cut Pro*.

### System Requirements
- **Operating System:** macOS 14.0 (Sonoma) or higher.
- **Apple Final Cut Pro:** Version 10.6 or higher.
- **Architecture:** Universal binary (Native Apple Silicon M1/M2/M3/M4 & Intel 64-bit).

---

## 📦 Descargas / Direct Downloads

| Plataforma | Archivo | Arquitectura |
| :--- | :--- | :--- |
| **macOS** | [**`Cumpa_X_v2.0.0_macOS.zip`**](https://github.com/argie4ever/CumpaX_releases/releases/download/v2.0.0/Cumpa_X_v2.0.0_macOS.zip) | Apple Silicon & Intel (Universal) |

---

## 📖 Documentación / Documentation

Consulta la guía operativa completa paso a paso incluida en el repositorio:
- 🇪🇸 [Manual de Usuario en Español (Markdown)](https://github.com/argie4ever/CumpaX_releases/releases/download/v2.0.0/manual_usuario_cumpa_x.md)
