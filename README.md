# PISAC — Plataforma de Información de Seguridad Acuática

**Servicio de Hidrografía, Oceanografía, Meteorología y Cartografiado Náutico (SHN Venezuela)**  
*Oficina Coordinadora de Hidrografía y Navegación (OCHINA Venezuela)*

---

## 1. Descripción General

**PISAC** (**Plataforma de Información de Seguridad Acuática**) es el sistema tecnológico institucional desarrollado e implementado por el **Servicio de Hidrografía y Navegación (SHN)** de la República Bolivariana de Venezuela para la gestión, producción, publicación y difusión de **Avisos a los Navegantes** y **Advertencias Náuticas** en los espacios acuáticos bajo jurisdicción nacional.

La plataforma materializa la transición tecnológica del SHN hacia el marco universal **S-100** de la **Organización Hidrográfica Internacional (OHI / IHO)**, implementando de forma nativa la especificación de producto **IHO S-124 (*Navigational Warnings*)**.

---

## 2. Alcance y Capacidades Principales

- **Cumplimiento del Estándar Internacional IHO S-124:**
  Estructuración normalizada de avisos náuticos, series nacionales y costeras, categorías generales de peligro y tipos específicos de advertencia conforme al catálogo de objetos S-124.
- **Visor Cartográfico Náutico Interactivo:**
  Integración directa con la cartografía náutica oficial del SHN Venezuela (encuadres costeros, regionales y oceánicos) mediante servicios geoespaciales estándar (**WMTS / WMS / WFS** y **Cloud Optimized GeoTIFF - COG**).
- **Gestión Integral del Ciclo de Vida de Avisos:**
  Creación asistida de geometrías náuticas (puntos, líneas, polígonos y áreas predefinidas en `EPSG:4326`), cruce espacial automático con zonas marítimas y cartas náuticas afectadas, control de vigencia y cancelación de avisos en vigor.
- **Difusión Multicanal y Bilingüe (ES / EN):**
  Generación automatizada de boletines oficiales en formato **PDF** institucional, redacción estandarizada de mensajes **TELEX / NAVTEX** en español e inglés, e interoperabilidad máquina a máquina mediante **GML S-124** e interfaces **SECOM**.
- **Administración de Cartografía Náutica:**
  Módulo integrado para la validación geoespacial, reproyección automática (GDAL) y publicación continua de cartas náuticas raster en el servidor cartográfico institucional.

---

## 3. Estructura del Proyecto y Repositorios

El ecosistema **PISAC** está compuesto por los siguientes módulos:

| Componente | Repositorio | Descripción |
| :--- | :--- | :--- |
| **Repositorio Principal** | [`shnve/pisac`](https://github.com/shnve/pisac) | Repositorio integrador del proyecto PISAC, arquitectura general y referencias a submódulos. |
| **Motor Backend (API)** | [`shnve/ping-api`](https://github.com/shnve/ping-api) | Servicios RESTful, modelo de datos S-124, motor geoespacial PostGIS, integración GDAL/GeoServer y generación GML/PDF (Java / Spring Boot). |
| **Portal Web (Frontend)** | [`shnve/ping-web`](https://github.com/shnve/ping-web) | Interfaz web para el público marítimo y consola administrativa del SHN con visor SIG interactivo (Angular / OpenLayers). |
| **Documentación Interna** | [`shnve/pisac-docs`](https://github.com/shnve/pisac-docs) *(Privado)* | Submódulo de acceso restringido al personal autorizado del SHN (matrices operativas, guías de despliegue y procedimientos internos). |

---

## 4. Arquitectura Tecnológica

```
┌───────────────────────────────────────────────────────────────────────────┐
│                   PISAC - Portal Web (shnve/ping-web)                     │
│                Angular + OpenLayers + Visor Náutico S-124                 │
└─────────────────────────────────────┬─────────────────────────────────────┘
                                      │ HTTPS / REST / OIDC
┌─────────────────────────────────────▼─────────────────────────────────────┐
│                  PISAC - Backend API (shnve/ping-api)                     │
│          Spring Boot + Hibernate Spatial + Liquibase + GDAL COG           │
└───────┬─────────────────────────────┬─────────────────────────────┬───────┘
        │                             │                             │
┌───────▼────────┐           ┌────────▼────────┐           ┌────────▼───────┐
│ PostgreSQL +   │           │   GeoServer     │           │   Keycloak     │
│    PostGIS     │           │  (WMTS / WMS)   │           │  (SSO / OIDC)  │
└────────────────┘           └─────────────────┘           └────────────────┘
```

---

## 5. Reconocimiento de Código Abierto

**PISAC** toma como base tecnológica los componentes de código abierto del proyecto **PING** desarrollado originalmente por el **SHOM (*Service Hydrographique et Océanographique de la Marine* - Francia)** bajo licencia **MIT**, incorporando las adaptaciones hidrográficas, cartográficas, lingüísticas y operativas propias del **Servicio de Hidrografía y Navegación (SHN Venezuela)**.

---

## 6. Contacto Institucional

- **Institución:** Servicio de Hidrografía y Navegación (SHN Venezuela) — Playa Grande, La Guaira, Venezuela.
- **Pagina Web:** `www.shn.gob.ve`
- **Correo Técnico:** `shnti@shn.gob.ve`
- **Organización GitHub:** [https://github.com/shnve](https://github.com/shnve)
