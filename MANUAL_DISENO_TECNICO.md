# 🐷 MANUAL DE DISEÑO TÉCNICO DE SOFTWARE
## Sistema Integral de Gestión Zootécnica, Visión Artificial y Trazabilidad Porcícola (PorciTech 4.0)

---

### Ficha Técnica de Ingeniería del Software
* **Programa de Formación:** Tecnólogo en Análisis y Desarrollo de Software (ADSO) — Código 228118
* **Ficha de Caracterización:** 3176243
* **Centro de Formación:** Centro de Teleinformática y Producción Industrial (CTPI) — Regional Cauca
* **Servicio Nacional de Aprendizaje (SENA)**
* **Unidad Productiva Beneficiaria:** Unidad Porcícola del Centro Agropecuario SENA — Granja La Rejoya
* **Dueño del Producto (Product Owner):** Ing. Pablo Antonio Ortiz
* **Equipo de Ingeniería y Desarrollo:**
  * **Santiago Avirama** — *Líder de Arquitectura Backend y DevOps*
  * **Camilo Velasco** — *Líder de Base de Datos y Plataforma Web*
  * **Mariana Guapacha** — *Líder de Desarrollo Móvil y Experiencia de Usuario (UX)*
  * **Juan David Ocampo** — *Líder de Inteligencia Artificial y Visión Computacional*
* **Marco Metodológico Documental:** Docs-as-Code (Documentación como Código)
* **Alineación Normativa Internacional:**
  * **ISO/IEC/IEEE 14764:2022** — *Software Engineering — Software Life Cycle Processes — Maintenance*
  * **ISO/IEC/IEEE 26531:2015** — *Content Management for Product Life-Cycle, User and Task-Oriented Information*
  * **ISO/IEC/IEEE 26514:2022** — *Requirements for Designers and Developers of User Documentation*

---

### Matriz de Control de Versiones Documental (ISO/IEC/IEEE 14764)

| Versión Doc. | Versión Software | Fecha | Naturaleza del Cambio (Tipo de Mantenimiento) | Responsable | Aprobación |
| :---: | :---: | :---: | :--- | :--- | :--- |
| **v0.1.0** | v0.1.0 | 15/03/2025 | Creación de la estructura base y definición de las 5 capas de abstracción. | Santiago Avirama | Equipo ADSO |
| **v1.0.0** | v1.0.0 | 28/05/2025 | Cierre Sprint 1: Arquitectura relacional PostgreSQL, autenticación JWT y RBAC. | Camilo Velasco | Pablo A. Ortiz (PO) |
| **v2.0.0** | v2.0.0 | 20/07/2025 | Cierre Sprint 2: Integración de Clean Architecture móvil en Flutter y cola Offline. | Mariana Guapacha | Pablo A. Ortiz (PO) |
| **v3.0.0** | v3.0.0 | 15/09/2025 | Cierre Sprint 3: Modelo YOLOv8n-seg dorsal, calibración alométrica y streaming RTSP. | Juan David Ocampo| Pablo A. Ortiz (PO) |
| **v4.0.0** | v4.0.0 | 09/11/2026 | Consolidación integral PorciTech 4.0: TimescaleDB Hipertabla, Pasaporte QR ICA, Docker Compose. | Santiago Avirama | Pablo A. Ortiz (PO) |
| **v4.1.0** | v4.1.0 | 18/11/2026 | Evolución Perfectiva/Adaptativa: 17 tablas (`alimentacion_planes`, `corrales_ciclos_sanitarios`), motor híbrido YOLOv8n-seg + XGBoost + ArUco multivista/EXIF, FEFO multi-lote, FCR, reportes Excel/PDF, idempotencia atómica `pg_advisory_xact_lock`, recuperación SMTP, cámara móvil embebida y módulo móvil de alimentación. | Santiago Avirama | Pablo A. Ortiz (PO) |

---

### Vinculación con Competencias Curriculares SENA ADSO

> [!NOTE]
> Este manual da cumplimiento formal a las tres competencias troncales del programa de formación ADSO:
> 1. **Diseño de Software (Competencia 220501095):** Sustenta los patrones arquitectónicos, diagramación C4/UML, el diseño entidad-relación y la especificación de interfaces.
> 2. **Implantación de Software (Competencia 220501097):** Define los requisitos operativos, variables de entorno, contenedores Docker y procedimientos de despliegue en granja.
> 3. **Buenas Prácticas en el Desarrollo (Competencia 220501098):** Incorpora la verificación estricta de calidad, esquemas de seguridad, mantenibilidad y gobernanza según ISO 14764.

---

## ÍNDICE GENERAL DEL MANUAL
1. [Capa 1: Contextual y Glosario Técnico (El Mapa y las Reglas del Juego)](#capa-1-contextual-y-glosario-técnico)
2. [Capa 2: Arquitectura y Modelo de Datos (Los Planos de la Casa)](#capa-2-arquitectura-y-modelo-de-datos)
3. [Capa 3: Operación, Entorno y Despliegue (El Manual de Armado)](#capa-3-operación-entorno-y-despliegue)
4. [Capa 4: APIs, Contratos e Interfaces (Los Puentes de Comunicación)](#capa-4-apis-contratos-e-interfaces)
5. [Capa 5: Mantenimiento, Gobernanza y Registros de Decisiones — ISO 14764](#capa-5-mantenimiento-gobernanza-y-registros-de-decisiones)
6. [Referencias Normativas y Bibliográficas](#referencias-normativas-y-bibliográficas)

---

<a name="capa-1-contextual-y-glosario-técnico"></a>
# 🧭 CAPA 1: Contextual y Glosario Técnico (El Mapa y las Reglas del Juego)

### 1.1 Planteamiento del Problema de Negocio

La producción porcícola intensiva en Colombia enfrenta cuatro cuellos de botella operacionales y económicos que limitan severamente la rentabilidad de las granjas:

```mermaid
flowchart TD
    subgraph PROBLEMAS ["Problematica Tradicional"]
        P1["1. Estres por Pesaje Mecanico: Perdida de 1.5 a 2 kg y aumento de cortisol"]
        P2["2. Costo Alimento 75%: Descuadre de inventario, falta de FCR y calculo GMD"]
        P3["3. Riesgo Sanitario ICA: Lotes vencidos, carencias farmacologicas y vacios sin control"]
        P4["4. Desconexion Rural: Sin internet en galpon y perdida de planillas"]
    end

    subgraph SOLUCION ["Solucion PorciTech 4.0"]
        S1["Vision Artificial Hibrida: YOLOv8n-seg, XGBoost, ArUco y soporte multivista sin estres"]
        S2["Kardex FEFO + FCR: Descuento multi-lote, planes nutricionales y GMD analitico"]
        S3["Inocuidad Integral ICA: Pasaporte QR trace, bloqueo lotes vencidos y vacios sanitarios"]
        S4["App Movil Offline-First: Cola Outbox idempotente, camara en vivo y teclado 64px"]
    end

    P1 --> S1
    P2 --> S2
    P3 --> S3
    P4 --> S4
```

---

### 1.2 Delimitación Estricta del Alcance (Scope)

| Dimensión | Lo que el Sistema HACE (In Scope) | Lo que el Sistema NO HACE (Out of Scope) |
| :--- | :--- | :--- |
| **Identificación** | Trazabilidad individual por arete visual y código QR único normalizado (compatible con URLs completas). | No soporta chips subcutáneos RFID/NFC activos (dependientes de hardware propietario). |
| **Pesaje IA** | Estimación biométrica híbrida (**YOLOv8n-seg + XGBoost 12 rasgos + fallback Huxley**) con calibración **ArUco**, corrección **EXIF** móvil, soporte **cualquier ángulo** (`cenital`, `oblicuo`, `lateral`) y báscula manual. | No realiza pesaje de cerdos en hacinamiento extremo donde la silueta individual esté ocluida en más del 60%. |
| **Nutrición y FCR** | Registro de raciones, planes alimentarios por etapa/corral, conversión automática bulto/kg, descuento **FEFO** y cálculo de **Conversión Alimenticia (FCR)** frente a Porkcolombia. | No dosifica tolvas mecánicas automáticamente mediante autómatas programables (PLC). |
| **Reproducción** | Control de servicios, cálculo automático de fecha de parto (Ley 114 días), partos y destetes. | No realiza análisis genómico computacional ni selección artificial molecular de semen. |
| **Sanidad y Bioseguridad** | Tratamientos por animal o corral, control de lote biológico ICA, tiempos de retiro, bloqueo automático de lotes vencidos, checklists diarios y auditoría de **Vacíos Sanitarios (Todo Adentro / Todo Afuera)**. | No diagnostica patologías clínicas de forma presuntiva sin criterio del médico veterinario. |
| **Reportes y Seguridad** | Exportación oficial en **Excel (`.xlsx`)** y **PDF (`.pdf`)** sanitizados, autenticación JWT/RBAC (`ENVIRONMENT=production` por defecto) y recuperación de contraseña vía **SMTP**. | No emite guías de movilización oficial de ganado directamente en la plataforma SIGMA del ICA. |
| **Conectividad** | Operación desconectada en galpón con cola local Outbox e idempotencia atómica (`id_local` + `pg_advisory_xact_lock` + índices únicos parciales). | No requiere sincronización P2P entre celulares sin pasar por el servidor central. |

---

### 1.3 Matriz de Acrónimos y Glosario Técnico Estandarizado

* **ACID (Atomicity, Consistency, Isolation, Durability):** Conjunto de propiedades que garantizan la confiabilidad de las transacciones en PostgreSQL 16.
* **ADR (Architecture Decision Record):** Documento técnico que captura una decisión arquitectónica significativa, su contexto y sus consecuencias.
* **Alometría (Ecuación de Huxley):** Estudio del cambio de proporción corporal ($\text{Peso} = 0.0245 \times \text{Área}_{\text{cm}^2}^{1.052}$). Usada como modelo de referencia y fallback fisiológico.
* **ArUco:** Patrón de marcador fiducial sintético cuadrado (`DICT_4X4_100`, `DICT_4X4_50`, `DICT_5X5_100`) usado para calibrar la escala espacial exacta ($\text{px}/\text{cm}$).
* **BPP (Buenas Prácticas Porcícolas):** Normas técnicas de Porkcolombia e ICA que regulan bioseguridad, alimentación y manejo del bienestar animal.
* **BRIN (Block Range Index):** Índice en PostgreSQL para tablas ordenadas cronológicamente con consumo mínimo de memoria RAM.
* **Continuous Aggregate (`cagg`):** Vista materializada de TimescaleDB que pre-computa agregaciones analíticas de forma incremental y continua.
* **Docs-as-Code:** Filosofía que trata la documentación técnica como código fuente (Markdown, Git, PRs).
* **FCR (Feed Conversion Ratio / Conversión Alimenticia):** Relación entre kilogramos de alimento suministrado y kilogramos de ganancia real de peso ($\text{FCR} = \frac{\text{Alimento kg}}{\text{Ganancia kg}}$).
* **FEFO (First-Expired, First-Out):** Estrategia de despacho de inventario que consume prioritariamente los lotes vigentes cuya fecha de vencimiento está más próxima, bloqueando lotes expirados.
* **Formula Injection:** Vulnerabilidad en exportaciones Excel/CSV neutralizada anteponiendo apóstrofe a celdas que inician con `=`, `+`, `-`, `@`.
* **GMD / GDP:** Ganancia Media Diaria / Ganancia Diaria de Peso.
* **Header Poisoning:** Ataque donde se manipula la cabecera HTTP `Origin`/`Host` en enlaces de recuperación; prevenido validando `Origin` contra orígenes CORS confiables.
* **Hipertabla (Hypertable):** Abstracción de TimescaleDB que particiona automáticamente una tabla en fragmentos temporales (*Chunks* de 7 días).
* **Idempotencia Atómica (`pg_advisory_xact_lock`):** Mecanismo de candado transaccional por clave `id_local` en PostgreSQL para evitar duplicados ante reintentos simultáneos de la cola móvil.
* **Kardex:** Sistema de control contable inmutable para entradas, salidas y saldos de bodega.
* **LAG():** Función analítica de ventana en SQL estándar usada tanto en `vista_gmd_diaria_corral` como en `vista_auditoria_vacios_corral`.
* **Momentos Invariantes de Hu:** Siete descriptores matemáticos invariantes a traslación, escala y rotación extraídos del contorno dorsal segmentado para alimentar el regresor **XGBoost**.
* **Outbox Pattern:** Patrón de mensajería asíncrona donde las mutaciones offline se encolan localmente en FIFO antes de sincronizarse al recuperar Wi-Fi.
* **RBAC (Role-Based Access Control):** Control de acceso basado en roles (`administrador`, `veterinario`, `operario`).
* **Soft Delete:** Borrado lógico mediante `deleted_at TIMESTAMPTZ`.
* **Todo Adentro / Todo Afuera:** Protocolo sanitario que exige desocupar totalmente un corral, desinfectarlo y cumplir un periodo mínimo de descanso antes de ingresar el siguiente lote.
* **XGBoost:** Algoritmo de *Gradient Boosting* entrenado sobre 12 características morfométricas para estimación tabular precisa de peso porcino.
* **YOLOv8n-seg:** Red neuronal de segmentación de instancias de Ultralytics filtrada por clase porcina (`pig`).

---

### 1.4 Guía de Convenciones y Estilos de Codificación Obligatorios

| Componente | Lenguaje / Framework | Guía de Estilo Oficial | Convención de Nomenclatura | Herramienta de Linter / Formato |
| :--- | :--- | :--- | :--- | :--- |
| **Backend API** | Python 3.11+ / FastAPI | PEP 8, PEP 484 (Type Hints) | `snake_case` (funciones, variables, endpoints)<br>`PascalCase` (clases, modelos Pydantic/ORM)<br>`SCREAMING_SNAKE_CASE` (constantes) | `ruff`, `black`, `flake8` |
| **Frontend Web** | Next.js 16 / React 19 | Airbnb JavaScript / React Style | `PascalCase` (Componentes, Vistas)<br>`camelCase` (hooks, servicios)<br>`kebab-case` (rutas públicas) | `eslint`, `prettier`, Tailwind CSS v4 |
| **App Móvil** | Flutter 3.12+ / Dart | Effective Dart Specification | `lowerCamelCase` (variables, métodos)<br>`UpperCamelCase` (clases, widgets, enums)<br>`lowercase_with_underscores` (archivos `.dart`) | `flutter analyze`, `dart format` |
| **Base de Datos** | SQL (PostgreSQL 16) | PostgreSQL Style Guide | `snake_case` en minúsculas<br>Prefijos: `cagg_`, `vista_`, `chk_`, `idx_`, `uq_`, `trg_` | `SQLFluff` |
| **Control Versiones** | Git / GitHub | Conventional Commits v1.0.0 | `feat:`, `fix:`, `docs:`, `refactor:`, `style:`, `chore:` | Git Hooks |

---

<a name="capa-2-arquitectura-y-modelo-de-datos"></a>
# 📐 CAPA 2: Arquitectura y Modelo de Datos (Los Planos de la Casa)

### 2.1 Justificación Técnica de Patrones Arquitectónicos

1. **Backend Modular en Capas + Servicios Compartidos (FastAPI):** Se estructura en `core/` (configuración, seguridad, SMTP, idempotencia, lifespan), `db/` (asyncpg), `models/` (ORM SQLAlchemy 2.0), `schemas/` (Pydantic v2), `services/` (`zootecnia_service.py` reutilizado por endpoints y reportes), `vision/` (pipeline híbrido + Dahua stream) y `api/v1/endpoints/` (**11 routers**).
2. **Frontend Basado en Características (Next.js 16 App Router):** Estructura `features/` desacoplada con layouts compartidos (`AuthSplitLayout`, `DashboardSidebar` responsivo), servicios HTTP dinámicos (`apiClient.js`) y protección RBAC en ruta y menú.
3. **Clean Architecture Móvil en 3 Capas (Flutter):** Organizada en **8 módulos** (`auth`, `dashboard`, `animals`, `weight_estimation`, `feeding`, `health_record`, `reproduction`, `sync`), aislando la capa de `domain/` (`Either<Failure, T>` con `fpdart`), `data/` (`DioClient` + `LocalCacheService`) y `presentation/` (**Riverpod** + cámara embebida + UX para guantes).
4. **Laboratorio I+D y Watcher RTSP Autónomo (`vision-artificial`):** Gestionado con `uv`, mantiene aislados el entrenamiento de XGBoost (`entrenar_xgboost.py`), scripts CLI de calibración (`calibrar_corral.py`) y vigilancia autónoma RTSP (`worker_rtsp_watcher.py`).

---

### 2.2 Diagramas Arquitectónicos (Modelo C4)

#### Diagrama de Contexto del Sistema (Nivel 1 - C4)

```mermaid
flowchart TD
    subgraph ACTORES ["Usuarios del Sistema"]
        ADM["Administrador de Granja: Gestion, Auditoria, Reportes Excel/PDF y Usuarios"]
        VET["Medico Veterinario: Sanidad, Reproduccion, Carencias y Vacios Sanitarios"]
        OPE["Operario de Galpon: Pesaje Multivista, Raciones, QR y Offline-First"]
        PUB["Inspector ICA o Comprador: Inocuidad en Frigorifico via Pasaporte QR"]
    end

    subgraph ECOSISTEMA ["Plataforma Central"]
        PORCITECH["PorciTech 4.0: Gestion Zootecnica, Trazabilidad e IA Hibrida"]
    end

    subgraph EXTERNOS ["Entidades, Servicios y Hardware Externo"]
        CAM["Camara Dahua Biespectral: RTSP Optico y Termico"]
        SMTP["Servidor SMTP: Envio de Enlaces de Recuperacion de Acceso"]
        ICA_ENT["Porkcolombia, ICA e INVIMA: Normativas Sanitarias y FCR"]
    end

    ADM --> PORCITECH
    VET --> PORCITECH
    OPE --> PORCITECH
    PUB --> PORCITECH

    CAM --> PORCITECH
    PORCITECH --> SMTP
    PORCITECH -.-> ICA_ENT
```

#### Diagrama de Contenedores (Nivel 2 - C4)

```mermaid
flowchart TB
    subgraph CLIENTES ["Capa de Clientes"]
        WEB["Portal Web Administrativo: Next.js 16 - Puerto 3000"]
        MOVIL["App Movil de Campo: Flutter 3.12 - 8 Modulos y Camara Integrada"]
        SCANNER["Navegador Externo: Consulta Publica Pasaporte QR"]
    end

    subgraph API_GATEWAY ["Capa Transaccional, Zootecnica e IA"]
        API["Backend Central: FastAPI y SQLAlchemy 2.0 - Puerto 8000"]
        IA_MEM["Motores en RAM: YOLOv8n-seg + XGBoost 12 Features + ArUco"]
        DAHUA_MNGR["DahuaStreamManager: 2 Hilos Demonio RTSP a MJPEG"]
        ZOOT_SRV["Servicios Zootecnicos: FEFO Multi-Lote, FCR, Vacios, Reportes y SMTP"]
    end

    subgraph PERSISTENCIA ["Capa de Persistencia Temporal y Relacional"]
        DB[("Base de Datos Central: PostgreSQL 16 y TimescaleDB - Puerto 5433")]
        HYPERTABLE["Hipertabla registro_pesos: Chunks semanales de 7 dias"]
        CAGGS["Vistas Analiticas: cagg_pesos, vista_gmd y vista_auditoria_vacios"]
    end

    subgraph SANDBOX ["Laboratorio ID y Watcher"]
        VISION_LAB["porcitech-vision: Puerto 8001, Entrenamiento XGBoost y Watcher RTSP"]
    end

    WEB --> API
    MOVIL --> API
    SCANNER --> WEB
    VISION_LAB --> API

    API --- IA_MEM
    API --- DAHUA_MNGR
    API --- ZOOT_SRV
    API --> DB

    DB --- HYPERTABLE
    DB --- CAGGS
```

#### Diagrama de Despliegue Físico en Red LAN de Granja

```mermaid
flowchart LR
    subgraph RED_GRANJA ["Red Local de Granja LAN"]
        ROUTER["Router Wi-Fi y Switch Industrial: 192.168.1.0/24"]
        CAM_IP["Camara Industrial Dahua RTSP: 192.168.1.108"]
        MOB_1["Celular Operario: Selector IP LAN y Modo Offline"]
        PC_ADM["Estacion Administrativa: Navegador Web y Descarga Reportes"]
    end

    subgraph SERVIDOR_HOST ["Servidor Docker Host - porcitech-net"]
        C_DB["Contenedor porcitech-db: Puerto 5433"]
        C_API["Contenedor porcitech-api: Puerto 8000"]
        C_WEB["Contenedor porcitech-frontend: Puerto 3000"]
        C_VIS["Contenedor porcitech-vision: Puerto 8001"]
    end

    ROUTER --- CAM_IP
    ROUTER --- MOB_1
    ROUTER --- PC_ADM

    ROUTER --> C_API
    ROUTER --> C_WEB
    C_API --> C_DB
    C_VIS --> C_API
```

---

### 2.3 Modelo de Persistencia de Datos (PostgreSQL 16 + TimescaleDB)

El esquema definitivo implementado en [`init.sql`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql) consta de **17 tablas relacionales organizadas en 5 dominios**, **1 Hipertabla**, **1 Vista Continua** y **2 Vistas Analíticas**:

```mermaid
erDiagram
    USUARIOS ||--o{ MOVIMIENTOS_INVENTARIO : registra
    USUARIOS ||--o{ SANIDAD_TRATAMIENTOS : prescribe
    USUARIOS ||--o{ ALIMENTACION_RACIONES : suministra
    USUARIOS ||--o{ ALIMENTACION_PLANES : crea
    USUARIOS ||--o{ REPRODUCCION_SERVICIOS : realiza
    USUARIOS ||--o{ EJECUCION_BIOSEGURIDAD : ejecuta
    USUARIOS ||--o{ CORRALES_CICLOS_SANITARIOS : audita_ciclo

    CORRALES ||--o{ ANIMALES : aloja
    CORRALES ||--o{ ALIMENTACION_RACIONES : consume
    CORRALES ||--o{ ALIMENTACION_PLANES : asigna_plan
    CORRALES ||--o{ REGISTRO_PESOS : ubica
    CORRALES ||--o{ SANIDAD_TRATAMIENTOS : trata_lote
    CORRALES ||--o{ EJECUCION_BIOSEGURIDAD : verifica
    CORRALES ||--o{ CORRALES_CICLOS_SANITARIOS : controla_vacios

    ANIMALES ||--o{ ANIMALES : tiene_progenitor
    ANIMALES ||--o{ SANIDAD_TRATAMIENTOS : recibe
    ANIMALES ||--o{ REPRODUCCION_SERVICIOS : participa
    ANIMALES ||--o{ REGISTRO_PESOS : acumula

    INVENTARIO_CATEGORIAS ||--o{ INVENTARIO_ITEMS : clasifica
    INVENTARIO_ITEMS ||--o{ INVENTARIO_LOTES : contiene
    INVENTARIO_ITEMS ||--o{ MOVIMIENTOS_INVENTARIO : traza_kardex
    INVENTARIO_ITEMS ||--o{ ALIMENTACION_RACIONES : consume_stock
    INVENTARIO_ITEMS ||--o{ ALIMENTACION_PLANES : define_dieta
    INVENTARIO_LOTES ||--o{ MOVIMIENTOS_INVENTARIO : afecta_lote
    INVENTARIO_LOTES ||--o{ SANIDAD_TRATAMIENTOS : aplica_lote

    PROTOCOLOS_BIOSEGURIDAD ||--o{ EJECUCION_BIOSEGURIDAD : audita

    REPRODUCCION_SERVICIOS ||--o{ REPRODUCCION_PARTOS : origina
    REPRODUCCION_PARTOS ||--o{ REPRODUCCION_DESTETES : culmina
```

---

### 2.4 Diccionario de Datos Estandarizado (17 Tablas de Negocio)

#### Dominio 1: Núcleo y Población

##### 1. Tabla: `usuarios` ([`init.sql#L81`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L81))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones / Reglas |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador único universal. | `DEFAULT uuid_generate_v4()` |
| `nombre` | `VARCHAR(100)` | No | - | Nombres del usuario. | - |
| `apellido` | `VARCHAR(100)` | No | - | Apellidos del usuario. | - |
| `email` | `VARCHAR(150)` | No | - | Correo electrónico de acceso. | `UNIQUE` |
| `password_hash`| `VARCHAR(255)` | No | - | Resumen hash Bcrypt. | Usado también para huella de un solo uso en reset SMTP |
| `rol` | `rol_usuario_enum`| No | - | Rol RBAC. | `'administrador'`, `'veterinario'`, `'operario'` |
| `telefono` | `VARCHAR(20)` | Sí | - | Teléfono de contacto. | - |
| `activo` | `BOOLEAN` | No | - | Estado de cuenta. | `DEFAULT TRUE` |
| `id_local` | `UUID` | Sí | - | Identificador móvil. | - |
| `sync_status` | `estado_sincronizacion_enum`| No | - | Estado de sincronización. | `DEFAULT 'synced'` |
| `created_at` | `TIMESTAMPTZ` | No | - | Creación del registro. | `DEFAULT clock_timestamp()` |
| `updated_at` | `TIMESTAMPTZ` | No | - | Última actualización. | Trigger `trg_usuarios_updated_at` |
| `deleted_at` | `TIMESTAMPTZ` | Sí | - | Soft Delete. | `NULL` = activo |

##### 2. Tabla: `corrales` ([`init.sql#L100`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L100))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones / Reglas |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del corral. | `DEFAULT uuid_generate_v4()` |
| `codigo` | `VARCHAR(50)` | No | - | Código único visible (ej. `LOTE-15`). | `UNIQUE` |
| `descripcion` | `TEXT` | Sí | - | Descripción física o notas. | - |
| `fase` | `tipo_fase_corral_enum`| No | - | Etapa productiva. | `'maternidad'`, `'precebo'`, `'destete'`, `'levante'`, `'ceba'`, `'engorde'`, `'cuarentena'`, `'gestacion'` |
| `capacidad_maxima`| `INT` | No | - | Cupo máximo de porcinos. | `CHECK (capacidad_maxima > 0)` |
| `fecha_inicio` | `DATE` | No | - | Fecha de apertura del corral. | `DEFAULT CURRENT_DATE` |
| `fecha_cierre` | `DATE` | Sí | - | Fecha de cierre. | `CHECK (fecha_cierre IS NULL OR fecha_cierre >= fecha_inicio)` |
| `activo` | `BOOLEAN` | No | - | Disponibilidad operativa. | `DEFAULT TRUE` |
| `id_local` | `UUID` | Sí | - | ID offline móvil. | Índice único parcial `uq_corrales_id_local` |
| `sync_status` | `estado_sincronizacion_enum`| No | - | Estado de sincronización. | `DEFAULT 'synced'` |
| `created_at` / `updated_at` / `deleted_at`| `TIMESTAMPTZ` | - | - | Auditoría temporal y Soft Delete. | Trigger `updated_at` |

##### 3. Tabla: `animales` ([`init.sql#L121`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L121))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones / Reglas |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador único del porcino. | `DEFAULT uuid_generate_v4()` |
| `codigo_arete` | `VARCHAR(50)` | No | - | Código del arete físico. | `UNIQUE` |
| `codigo_qr` | `VARCHAR(100)` | No | - | Código QR único para trazabilidad. | `UNIQUE` |
| `nombre_alias` | `VARCHAR(80)` | Sí | - | Nombre o alias (ej. reproductor). | - |
| `sexo` | `sexo_animal_enum` | No | - | Sexo biológico. | `'macho'`, `'hembra'` |
| `raza` | `VARCHAR(60)` | No | - | Raza o línea genética. | - |
| `fecha_nacimiento`| `DATE` | No | - | Fecha de nacimiento. | - |
| `estado` | `estado_animal_enum`| No | - | Estado fisiológico/productivo. | `'activo'`, `'lactante'`, `'precebo'`, `'levante'`, `'engorde'`, `'gestacion'`, `'cuarentena'`, `'vendido'`, `'muerto'`, `'enfermo'`, `'descarte'`, `'reemplazo'` |
| `corral_id` | `UUID` | Sí | FK | Corral actual. | `REFERENCES corrales(id) ON DELETE SET NULL` |
| `id_padre` | `UUID` | Sí | FK | Padre genético. | `REFERENCES animales(id) ON DELETE SET NULL` |
| `id_madre` | `UUID` | Sí | FK | Madre genética. | `chk_genealogia_distinta`: `id <> id_padre AND id <> id_madre` |
| `peso_actual_kg` | `NUMERIC(6,2)` | Sí | - | Último peso consolidado (kg). | `DEFAULT 0.00 CHECK (peso_actual_kg >= 0)` |
| `foto_url` | `TEXT` | Sí | - | URL o referencia de fotografía. | - |
| `id_local` | `UUID` | Sí | - | ID offline móvil. | Índice único parcial `uq_animales_id_local` |
| `sync_status` | `estado_sincronizacion_enum`| No | - | Estado de réplica móvil. | `DEFAULT 'synced'` |

---

#### Dominio 2: Bodega, Insumos, Lotes FEFO y Kardex Contable

##### 4. Tabla: `inventario_categorias` ([`init.sql#L148`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L148))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador de categoría. | `DEFAULT uuid_generate_v4()` |
| `codigo` | `VARCHAR(50)` | No | - | Código clave (`alimento`, `medicamento`, etc.). | `UNIQUE` |
| `nombre` | `VARCHAR(100)` | No | - | Nombre de la categoría. | - |
| `color` | `VARCHAR(50)` | Sí | - | Color distintivo en UI. | `DEFAULT 'blue'` |
| `descripcion` | `TEXT` | Sí | - | Alcance de la categoría. | - |

##### 5. Tabla: `inventario_items` ([`init.sql#L158`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L158))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones / Reglas |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del insumo. | `DEFAULT uuid_generate_v4()` |
| `categoria_id` | `UUID` | No | FK | Categoría asociada. | `REFERENCES inventario_categorias(id) ON DELETE RESTRICT` |
| `codigo_sku` | `VARCHAR(60)` | No | - | Código SKU (autogenerado si se omite en UI). | `UNIQUE` |
| `nombre` | `VARCHAR(120)` | No | - | Nombre comercial del producto. | - |
| `unidad_medida` | `VARCHAR(50)` | No | - | Presentación (`Bultos (40kg)`, `Frasco`, etc.). | - |
| `factor_conversion_kg`| `NUMERIC(8,3)`| No | - | Equivalencia en kg por unidad. | `DEFAULT 1.000 CHECK (factor_conversion_kg > 0)` |
| `stock_actual` | `NUMERIC(10,2)`| No | - | Existencia física total en bodega. | `CHECK (stock_actual >= 0)` |
| `stock_minimo` | `NUMERIC(10,2)`| No | - | Umbral de alerta de reposición. | `CHECK (stock_minimo >= 0)` |
| `costo_unitario`| `NUMERIC(12,2)`| No | - | Costo unitario en COP. | `CHECK (costo_unitario >= 0)` |
| `ubicacion_bodega`| `VARCHAR(80)`| Sí | - | Estante o silo de almacenamiento. | - |

##### 6. Tabla: `inventario_lotes` ([`init.sql#L178`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L178))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones / Reglas |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del lote. | `DEFAULT uuid_generate_v4()` |
| `item_id` | `UUID` | No | FK | Insumo asociado. | `REFERENCES inventario_items(id) ON DELETE CASCADE` |
| `numero_lote` | `VARCHAR(100)` | No | - | Número de lote del fabricante. | - |
| `fecha_fabricacion`| `DATE` | Sí | - | Fecha de elaboración. | - |
| `fecha_vencimiento`| `DATE` | Sí | - | Fecha de expiración para control **FEFO**. | `chk_fechas_lote_inventario`: vencimiento $\ge$ fabricación |
| `cantidad_inicial`| `NUMERIC(10,2)`| No | - | Cantidad recibida inicialmente. | `CHECK (cantidad_inicial > 0)` |
| `cantidad_disponible`| `NUMERIC(10,2)`| No | - | Saldo remanente disponible para consumo. | `CHECK (cantidad_disponible >= 0)` |
| `registro_ica` | `VARCHAR(60)` | Sí | - | Número de registro sanitario oficial ICA. | - |

##### 7. Tabla: `movimientos_inventario` ([`init.sql#L198`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L198))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del asiento Kardex. | `DEFAULT uuid_generate_v4()` |
| `item_id` | `UUID` | No | FK | Insumo afectado. | `REFERENCES inventario_items(id)` |
| `lote_inventario_id`| `UUID` | Sí | FK | Lote específico afectado (regla FEFO). | `REFERENCES inventario_lotes(id)` |
| `tipo_movimiento` | `tipo_movimiento_inv_enum`| No | - | Tipo contable. | `'entrada_compra'`, `'salida_consumo'`, `'ajuste_merma'`, `'devolucion'` |
| `cantidad` | `NUMERIC(10,2)`| No | - | Cantidad movida. | `CHECK (cantidad > 0)` |
| `costo_unitario`| `NUMERIC(12,2)`| No | - | Valor unitario registrado. | `CHECK (costo_unitario >= 0)` |
| `usuario_id` | `UUID` | No | FK | Usuario responsable. | `REFERENCES usuarios(id)` |
| `fecha_movimiento`| `TIMESTAMPTZ` | No | - | Fecha y hora exacta del movimiento. | `DEFAULT clock_timestamp()` |
| `motivo` | `VARCHAR(255)` | Sí | - | Descripción contable / lote consumido. | - |
| `referencia_modulo`| `VARCHAR(50)` | Sí | - | Módulo origen (`alimentacion`, `sanidad`, etc.). | - |
| `referencia_id` | `UUID` | Sí | - | UUID de la ración o tratamiento origen. | - |

---

#### Dominio 3: Operación Zootécnica, Nutrición (FCR) y Sanidad ICA

##### 8. Tabla: `sanidad_tratamientos` ([`init.sql#L251`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L251))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones / Reglas |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del evento clínico. | `DEFAULT uuid_generate_v4()` |
| `animal_id` | `UUID` | Sí | FK | Animal tratado (si es individual). | `chk_sanidad_objetivo_valido`: `animal_id IS NOT NULL OR corral_id IS NOT NULL` |
| `corral_id` | `UUID` | Sí | FK | Corral tratado (si es masivo por lote). | `REFERENCES corrales(id) ON DELETE SET NULL` |
| `veterinario_id`| `UUID` | No | FK | Profesional responsable. | `REFERENCES usuarios(id)` |
| `medicamento_id`| `UUID` | Sí | FK | Ítem farmacológico de bodega. | `REFERENCES inventario_items(id)` |
| `lote_inventario_id`| `UUID`| Sí | FK | Lote de bodega descontado por FEFO. | `REFERENCES inventario_lotes(id)` |
| `lote_biologico`| `VARCHAR(100)` | Sí | - | Lote biológico certificado ICA. | - |
| `tipo_evento` | `VARCHAR(50)` | No | - | Categoría clínica (`Vacuna`, `Tratamiento`, etc.).| - |
| `producto_nombre`| `VARCHAR(120)`| No | - | Nombre comercial del biológico/fármaco. | - |
| `diagnostico` | `VARCHAR(150)` | Sí | - | Diagnóstico o propósito preventivo. | - |
| `dosis` / `unidad_dosis` / `via_administracion`| `NUMERIC` / `VARCHAR`| Sí | - | Posología clínica aplicada. | `CHECK (dosis IS NULL OR dosis >= 0)` |
| `tiempo_retiro_dias`| `INT` | No | - | Días de carencia ICA. | `DEFAULT 0 CHECK (tiempo_retiro_dias >= 0)` |
| `fecha_tratamiento`| `TIMESTAMPTZ`| No | - | Fecha de aplicación. | Usada junto a `tiempo_retiro_dias` para calcular bloqueo en `/trace/[id]` |
| `fecha_proxima_dosis`| `DATE` | Sí | - | Fecha de refuerzo programado. | - |
| `id_local` | `UUID` | Sí | - | ID offline móvil. | Índice único parcial `uq_sanidad_tratamientos_id_local` |

##### 9. Tabla: `alimentacion_raciones` ([`init.sql#L280`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L280))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del suministro. | `DEFAULT uuid_generate_v4()` |
| `corral_id` | `UUID` | No | FK | Corral alimentado. | `REFERENCES corrales(id) ON DELETE CASCADE` |
| `alimento_item_id`| `UUID` | No | FK | Concentrado suministrado. | `REFERENCES inventario_items(id)` |
| `operario_id` | `UUID` | No | FK | Operario responsable. | `REFERENCES usuarios(id)` |
| `fase_alimentacion`| `VARCHAR(50)`| No | - | Fase nutricional (`Pre-iniciador`, `Ceba`, etc.). | - |
| `cantidad_kg` | `NUMERIC(10,2)`| No | - | Kilogramos netos servidos. | `CHECK (cantidad_kg > 0)` |
| `fecha_suministro`| `TIMESTAMPTZ`| No | - | Marca temporal (índice `BRIN`). | `DEFAULT clock_timestamp()` |
| `costo_total` | `NUMERIC(12,2)`| No | - | Costo calculado de la ración. | `CHECK (costo_total >= 0)` |
| `id_local` | `UUID` | Sí | - | ID offline móvil. | Índice único parcial `uq_alimentacion_raciones_id_local` |

##### 10. Tabla: `alimentacion_planes` ([`init.sql#L574`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L574))
Almacena planes nutricionales objetivo por etapa productiva y corral para evaluación de **FCR** (HU24 / HU26).

| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del plan alimentario. | `DEFAULT uuid_generate_v4()` |
| `nombre` | `VARCHAR(120)` | No | - | Nombre descriptivo del plan nutricional. | - |
| `fase_alimentacion`| `VARCHAR(50)`| No | - | Etapa productiva objetivo. | - |
| `corral_id` | `UUID` | Sí | FK | Corral asignado (opcional si aplica a toda la fase). | `REFERENCES corrales(id) ON DELETE SET NULL` |
| `alimento_item_id`| `UUID` | No | FK | Concentrado prescrito. | `REFERENCES inventario_items(id)` |
| `cantidad_kg_por_animal`| `NUMERIC(6,2)`| No | - | Ración diaria objetivo por cerdo (kg). | `CHECK (cantidad_kg_por_animal > 0)` |
| `frecuencia_diaria`| `INT` | No | - | Número de suministros diarios. | `DEFAULT 2 CHECK (frecuencia_diaria BETWEEN 1 AND 12)` |
| `fcr_objetivo` | `NUMERIC(4,2)` | Sí | - | Meta de Conversión Alimenticia (FCR). | `DEFAULT 2.40 CHECK (fcr_objetivo IS NULL OR fcr_objetivo > 0)` |
| `activo` | `BOOLEAN` | No | - | Vigencia del plan. | `DEFAULT TRUE` |
| `creado_por` | `UUID` | Sí | FK | Usuario autor. | `REFERENCES usuarios(id)` |

---

#### Dominio 4: Bioseguridad y Auditoría de Vacíos Sanitarios (ICA)

##### 11. Tabla: `protocolos_bioseguridad` ([`init.sql#L218`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L218))
Contiene los protocolos (`codigo` UNIQUE, `tipo_protocolo` `estructural`/`operacional`, `tarea`, `descripcion`, `icono`, `frecuencia`, `activo`).

##### 12. Tabla: `ejecucion_bioseguridad` ([`init.sql#L235`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L235))
Registra las verificaciones ejecutadas (`protocolo_id` FK, `operario_id` FK, `corral_id` FK opcional para trazabilidad por corral, `fecha_registro`, `estado`, `observaciones`).

##### 13. Tabla: `corrales_ciclos_sanitarios` ([`init.sql#L593`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L593))
Controla los ciclos productivos **Todo Adentro / Todo Afuera (HU38)** para verificar descansos sanitarios entre lotes.

| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del ciclo sanitario. | `DEFAULT uuid_generate_v4()` |
| `corral_id` | `UUID` | No | FK | Corral auditado. | `REFERENCES corrales(id) ON DELETE CASCADE` |
| `codigo_lote` | `VARCHAR(80)` | No | - | Código del lote animal que ingresa. | - |
| `fecha_entrada`| `DATE` | No | - | Fecha de ingreso del lote. | - |
| `fecha_salida` | `DATE` | Sí | - | Fecha de desocupación total del corral. | `chk_ciclo_fechas_validas`: salida $\ge$ entrada |
| `cantidad_animales`| `INT` | No | - | Número de animales del ciclo. | `CHECK (cantidad_animales >= 0)` |
| `dias_vacio_requerido`| `INT` | No | - | Días de descanso sanitario exigidos. | `DEFAULT 7 CHECK (dias_vacio_requerido >= 0)` |
| `desinfeccion_verificada`| `BOOLEAN`| No | - | Confirmación de lavado y desinfección. | `DEFAULT FALSE` |
| `responsable_id`| `UUID` | Sí | FK | Usuario verificador. | `REFERENCES usuarios(id)` |

---

#### Dominio 5: Ciclo Reproductivo Porcino (Ley 114 Días)

##### 14. Tabla: `reproduccion_servicios` ([`init.sql#L300`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L300))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones / Reglas |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `id` | `UUID` | No | PK | Identificador del servicio. | `DEFAULT uuid_generate_v4()` |
| `hembra_id` | `UUID` | No | FK | Cerda servida. | `REFERENCES animales(id) ON DELETE CASCADE` |
| `macho_id` | `UUID` | Sí | FK | Verraco padre (opcional si es inseminación). | `chk_servicio_progenitores_distintos` |
| `tecnico_id` | `UUID` | No | FK | Técnico responsable. | `REFERENCES usuarios(id)` |
| `tipo_servicio`| `VARCHAR(30)` | No | - | Modalidad. | `'inseminacion_artificial'`, `'monta_natural'` |
| `codigo_pajilla_macho`| `VARCHAR(80)`| Sí | - | Código de semen/pajilla si es IA. | - |
| `fecha_servicio`| `DATE` | No | - | Fecha de concepción. | - |
| `fecha_probable_parto`| `DATE` | No | - | **Ley biológica de los 114 días.** | `GENERATED ALWAYS AS (fecha_servicio + '114 days'::interval) STORED` |
| `estado_confirmacion`| `VARCHAR(30)`| No | - | Diagnóstico gestacional. | `'pendiente'`, `'positiva'`, `'negativa'`, `'repetida'` |
| `id_local` | `UUID` | Sí | - | ID offline móvil. | Índice único parcial `uq_reproduccion_servicios_id_local` |

##### 15. Tabla: `reproduccion_partos` ([`init.sql#L321`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L321))
Registra `servicio_id` (UNIQUE FK nullable), `hembra_id` (FK), `corral_maternidad_id` (FK), `atendido_por` (FK), `fecha_parto`, `numero_parto`, `nacidos_vivos`, `nacidos_muertos`, `momias`, `peso_camada_total_kg` e `id_local` (índice único parcial).

##### 16. Tabla: `reproduccion_destetes` ([`init.sql#L342`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L342))
Registra `parto_id` (UNIQUE FK nullable), `hembra_id` (FK), `corral_destino_id` (FK), `operario_id` (FK), `fecha_destete`, `lechones_destetados`, `peso_total_kg`, `dias_lactancia` e `id_local` (índice único parcial).

---

#### Dominio 6: Serie Temporal e Inteligencia Artificial (TimescaleDB)

##### 17. Tabla: `registro_pesos` (HIPERTABLA) ([`init.sql#L361`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L361))
| Columna | Tipo de Dato | Nulo | PK/FK | Descripción | Restricciones / Reglas |
| :--- | :--- | :---: | :---: | :--- | :--- |
| `tiempo` | `TIMESTAMPTZ` | No | **PK (Compuesta)** | Marca temporal exacta del pesaje. | Columna de particionamiento cada **7 días** |
| `id_registro` | `UUID` | No | **PK (Compuesta)** | Identificador único del evento. | `DEFAULT uuid_generate_v4()` |
| `id_cerdo` | `UUID` | No | **PK (Compuesta)** | Porcino evaluado. | `REFERENCES animales(id) ON DELETE CASCADE` |
| `corral_id` | `UUID` | No | FK | Corral asociado. | `REFERENCES corrales(id) ON DELETE CASCADE` |
| `peso_kg` | `DOUBLE PRECISION` | No | - | Peso estimado o medido (kg). | `CHECK (peso_kg > 0)` |
| `metodo` | `metodo_pesaje_enum`| No | - | Origen de medición. | `'manual'`, `'vision_ai'`, `'ia_vision'`, `'bascula_digital'` |
| `confianza_ia` | `DOUBLE PRECISION` | Sí | - | Score de confianza YOLO. | `0.0` a `1.0` |
| `area_cm2` / `largo_cm` / `ancho_cm` | `DOUBLE PRECISION` | Sí | - | Métricas geométricas extraídas en cm. | Calculadas tras calibración ArUco |
| `bbox` | `JSONB` | Sí | - | Metadatos (`x1,y1,x2,y2`, `algoritmo_peso`, `angulo_vista`, `metodo_calibracion`, `aruco_id`, `ancho_toracico_cm`). | JSON estructurado |
| `foto_evidencia_url`| `TEXT` | Sí | - | Referencia de imagen capturada. | - |
| `id_local` | `UUID` | Sí | - | ID offline móvil. | Protegido en API con `pg_advisory_xact_lock` |

> [!IMPORTANT]
> **Idempotencia Offline-First y Chunks en TimescaleDB:**
> Para proteger las tablas operativas contra reintentos concurrentes de la cola FIFO móvil, [`init.sql#L618-L636`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L618-L636) crea índices únicos parciales `uq_<table>_id_local` sobre `(id_local) WHERE id_local IS NOT NULL AND deleted_at IS NULL` en 7 tablas operativas. Como `registro_pesos` es hipertabla TimescaleDB (donde cualquier índice único requiere incluir `tiempo`), su idempotencia atómica se garantiza mediante `pg_advisory_xact_lock` en [`idempotency.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/core/idempotency.py).

---

### 2.5 Vistas Materializadas Continuas y Analítica SQL

1. **`cagg_pesos_diarios_corral` ([`init.sql#L507-L523`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L507-L523)):** Continuous Aggregate diario sobre `registro_pesos` (`time_bucket('1 day', tiempo)`) con refresco horario automático.
2. **`vista_gmd_diaria_corral` ([`init.sql#L527-L561`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L527-L561)):** Calcula `gmd_kg` y `variacion_porcentual` usando `LAG(peso_promedio_kg)` y `LAG(dia_bucket)` normalizado por los días exactos transcurridos (`EXTRACT(EPOCH ...)/86400.0`).
3. **`vista_auditoria_vacios_corral` ([`init.sql#L638-L684`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L638-L684)):** Usa `LAG(codigo_lote)` y `LAG(fecha_salida)` sobre `corrales_ciclos_sanitarios` para calcular `dias_vacio_sanitario` y clasificar automáticamente cada ciclo en `cumple_protocolo`, `alerta_vacio_insuficiente`, `pendiente_desinfeccion` o `primer_ciclo`.

---

<a name="capa-3-operación-entorno-y-despliegue"></a>
# ⚙️ CAPA 3: Operación, Entorno y Despliegue (El Manual de Armado)

### 3.1 Requisitos Previos del Sistema

| Componente | Requisito Mínimo (Entorno Pruebas / Dev) | Requisito Recomendado (Producción en Granja) |
| :--- | :--- | :--- |
| **Arquitectura Host** | x86_64 (Intel Core i5 8ª Gen / AMD Ryzen 5) | x86_64 (Intel Core i7 11ª Gen / Servidor Xeon) |
| **Memoria RAM** | 8 GB de RAM disponible | 16 GB - 32 GB DDR4/DDR5 |
| **Almacenamiento** | 20 GB libres (Disco SSD) | 120 GB SSD NVMe |
| **Sistema Operativo** | Linux (Ubuntu 22.04+ / Debian 12), Windows 10/11 con WSL2 | Ubuntu Server 22.04 LTS o 24.04 LTS |
| **Motor Contenedores** | Docker Engine 24.0+ y Docker Compose v2.20+ | Docker Engine Enterprise / Compose v2.26+ |
| **Red** | Tarjeta de red Ethernet 100 Mbps | Gigabit Ethernet (1000 Mbps) + Wi-Fi para dispositivos móviles |
| **Dispositivo Móvil** | Android 8.0+ o iOS 13+ con cámara trasera | Android 11+ con gran angular, 4 GB RAM y protección IP68 |

---

### 3.2 Matriz y Plantilla Comentada de Variables de Entorno (`.env`)

Alineada con [`docker-compose.yml`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/docker-compose.yml) y [`config.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/core/config.py):

```bash
# =============================================================================
# VARIABLES DE ENTORNO — PLATAFORMA PORCITECH 4.0
# =============================================================================

# --- 1. CONFIGURACIÓN GENERAL Y SEGURIDAD ---
# En "production" (valor por defecto) se exige JWT válido en todas las mutaciones.
# Use "development" únicamente en pruebas locales controladas.
ENVIRONMENT=production
TZ=America/Bogota
PGTZ=America/Bogota
SECRET_KEY=reemplazar_por_valor_aleatorio_seguro_openssl_rand_hex_32
ACCESS_TOKEN_EXPIRE_MINUTES=1440

# --- 2. BASE DE DATOS (PostgreSQL 16 + TimescaleDB) ---
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=porcitech_db
DB_PORT=5433
DATABASE_URL=postgresql+asyncpg://postgres:postgres@db:5432/porcitech_db

# --- 3. CORS Y RED LOCAL LAN (RFC 1918) ---
CORS_ORIGINS=["http://localhost:3000", "http://127.0.0.1:3000"]
CORS_ORIGIN_REGEX=https?://(localhost|127\.0\.0\.1|192\.168\.\d+\.\d+|10\.\d+\.\d+\.\d+|172\.(1[6-9]|2\d|3[0-1])\.\d+\.\d+|[a-zA-Z0-9-]+(\.local)?)(:\d+)?

# --- 4. MODELOS IA Y CALIBRACIÓN ARUCO ---
YOLO_WEIGHTS_PATH=weights/best.pt
XGBOOST_WEIGHTS_PATH=weights/modelo_peso_xgboost.json
CAMERA_CALIBRATION_PATH=weights/calibracion_camara.json
ARUCO_MARKER_SIZE_CM=10.0

# --- 5. CÁMARA INDUSTRIAL DAHUA TPC-BF (RTSP STREAMING) ---
DAHUA_CAMERA_IP=192.168.1.108
DAHUA_CAMERA_PORT=554
DAHUA_CAMERA_USER=admin
DAHUA_CAMERA_PASSWORD=admin123
DAHUA_RTSP_URL=rtsp://admin:admin123@192.168.1.108:554/cam/realmonitor?channel=1&subtype=0

# --- 6. CORREO TRANSACCIONAL SMTP Y RECUPERACIÓN DE ACCESO (HU02) ---
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=
SMTP_PASSWORD=
SMTP_FROM_EMAIL=no-reply@porcitech.local
SMTP_USE_TLS=true
FRONTEND_BASE_URL=http://localhost:3000
PASSWORD_RESET_EXPIRE_MINUTES=30

# --- 7. FRONTEND WEB (Next.js 16) ---
NEXT_PUBLIC_API_URL=
INTERNAL_API_URL=http://api:8000/api/v1
```

---

### 3.3 Orquestación con Docker Compose ([`docker-compose.yml`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/docker-compose.yml))

Gestiona 4 servicios sobre la red bridge `porcitech-net`:

1. **`porcitech-db` (TimescaleDB PG16):** Puerto `5433:5432`, volumen `porcitech_pgdata` e inicialización automática con `./porcitech-backend/scripts/init.sql`. Healthcheck vía `pg_isready`.
2. **`porcitech-api` (FastAPI + YOLOv8 + XGBoost):** Puerto `8000:8000`. Carga en RAM `best.pt`, `modelo_peso_xgboost.json` y `calibracion_camara.json`. Healthcheck en `GET /health`.
3. **`porcitech-frontend` (Next.js 16):** Puerto `3000:3000`. Depende de `api` (`service_healthy`).
4. **`porcitech-vision` (Sandbox / Lab I+D):** Puerto `8001:8001`.

---

### 3.4 Guía Paso a Paso para Instalación, Despliegue y Compilación Móvil

```bash
# 1. Despliegue automatizado con autodescubrimiento de IP LAN
chmod +x deploy.sh
./deploy.sh

# 2. (Opcional) Poblar dataset demostrativo completo
docker exec -i porcitech-db psql -U postgres -d porcitech_db < ScriptsSQL/seed_demo.sql

# 3. Compilar APK Release de la App Móvil (también disponible en raíz como PorciTech-Mobile.apk)
cd porcitech_mobile
flutter pub get
flutter build apk --release --dart-define=API_BASE_URL=http://<IP_SERVIDOR>:8000/api/v1
```

*(Nota: Incluso sin pasar `--dart-define`, la App Móvil permite ajustar la IP del servidor directamente desde el diálogo en la pantalla de Login).*

---

<a name="capa-4-apis-contratos-e-interfaces"></a>
# 🌉 CAPA 4: APIs, Contratos e Interfaces (Los Puentes de Comunicación)

### 4.1 Especificación de Endpoints RESTful (`/api/v1`)

| Módulo | Método | Endpoint | Roles Permitidos | Descripción Funcional |
| :--- | :---: | :--- | :--- | :--- |
| **Auth** | `POST` | `/api/v1/auth/login` | Público | Autenticación OAuth2 Password y entrega de token JWT Bearer. |
| **Auth** | `GET` | `/api/v1/auth/me` | Todos | Perfil y rol del usuario autenticado. |
| **Auth** | `POST` | `/api/v1/auth/forgot-password` | Público | Genera token de recuperación de un solo uso y envía correo SMTP (validando `Origin`). |
| **Auth** | `POST` | `/api/v1/auth/reset-password` | Público | Valida token temporal + huella de hash actual y actualiza contraseña con Bcrypt. |
| **Usuarios** | `GET / POST / PUT / DELETE` | `/api/v1/usuarios` | `administrador` | Administración RBAC y desactivación lógica de usuarios. |
| **Corrales** | `GET / POST / PUT / DELETE` | `/api/v1/corrales` | Todos / `admin` | Gestión de corrales y fases productivas. |
| **Corrales** | `GET` | `/api/v1/corrales/auditoria-vacios` | Todos | Consulta `vista_auditoria_vacios_corral` (Todo Adentro / Todo Afuera). |
| **Corrales** | `POST / PUT` | `/api/v1/corrales/{corral_id}/ciclos` | `vet`, `admin` | Registro y cierre/verificación de desinfección de ciclos sanitarios. |
| **Animales** | `GET / POST / PUT / DELETE` | `/api/v1/animales` | Todos / Operación | Catálogo, genealogía y bloqueo de cupo con `FOR UPDATE`. |
| **Animales** | `GET` | `/api/v1/animales/qr/{codigo_qr:path}`| Público / Todos | Búsqueda insensible a mayúsculas con normalización automática de URLs QR. |
| **Pesajes** | `GET` | `/api/v1/pesajes/calibracion` | Todos | Estado de calibración ArUco y disponibilidad de modelos YOLO y XGBoost. |
| **Pesajes** | `POST` | `/api/v1/pesajes/calibrar-aruco` | `operario`, `vet`, `admin` | Detecta marcador ArUco en foto y persiste `calibracion_camara.json`. |
| **Pesajes** | `POST` | `/api/v1/pesajes/vision` | `operario`, `vet`, `admin` | Inferencia multivista (`angulo_vista`, `modo_movil`, EXIF) con XGBoost/Huxley. |
| **Pesajes** | `GET` | `/api/v1/pesajes/stream/live` | Todos | Stream MJPEG en vivo desde Dahua TPC-BF (Canal 1 Óptico / Canal 2 Térmico). |
| **Pesajes** | `GET / POST` | `/api/v1/pesajes/stream/status` & `config` | Todos / Operación | Estado, métricas en tiempo real y actualización de configuración RTSP. |
| **Pesajes** | `POST` | `/api/v1/pesajes/capturar-en-vivo` | `operario`, `vet`, `admin` | Congela fotograma del stream Dahua, infiere peso y guarda en TimescaleDB. |
| **Pesajes** | `POST` | `/api/v1/pesajes/manual` | `operario`, `vet`, `admin` | Registro manual o sincronización idempotente (`id_local`) en Hipertabla. |
| **Pesajes** | `GET` | `/api/v1/pesajes/corral/{corral_id}/gmd` | Todos | Curva de Ganancia Media Diaria (GMD) por corral y período. |
| **Inventario**| `GET / POST` | `/api/v1/inventario/items` | Todos / `vet`, `admin` | Catálogo con autogeneración de SKU y registro simultáneo de lote inicial. |
| **Inventario**| `GET` | `/api/v1/inventario/lotes/alertas-vencimiento` | Todos | Alertas de lotes vencidos y próximos a vencer (HU30). |
| **Inventario**| `GET / POST` | `/api/v1/inventario/movimientos` | Todos / `vet`, `admin` | Asientos inmutables de Kardex con descuento FEFO y bloqueo de lotes vencidos. |
| **Alimentación**| `GET / POST` | `/api/v1/alimentacion/raciones` | `operario`, `vet`, `admin` | Suministro de raciones por corral con descuento automático FEFO en bodega. |
| **Alimentación**| `GET / POST / PUT / DELETE` | `/api/v1/alimentacion/planes` | `vet`, `admin` | Planes nutricionales objetivo por etapa y corral (HU24). |
| **Alimentación**| `GET` | `/api/v1/alimentacion/conversion-alimenticia` | Todos | Cálculo real de Conversión Alimenticia (FCR) vs estándar Porkcolombia (HU26). |
| **Sanidad** | `GET / POST` | `/api/v1/sanidad/tratamientos` & `alertas-retiro` | `vet`, `admin` / Todos | Tratamientos individuales o por corral, lote FEFO y semáforo de retiro ICA. |
| **Sanidad** | `GET / POST` | `/api/v1/sanidad/bioseguridad/protocolos` & `ejecuciones` | Todos / Operación | Checklists de bioseguridad con filtro por fecha y `corral_id`. |
| **Reproducción**| `GET / POST / PUT` | `/api/v1/reproduccion/servicios`, `partos`, `destetes` | `operario`, `vet`, `admin` | Ciclo reproductivo completo (Ley 114 días, máquina de estados materna). |
| **Dashboard** | `GET` | `/api/v1/dashboard/kpis`, `recent-activity`, `alerts` | Todos | Indicadores gerenciales y alertas en tiempo real. |
| **Reportes** | `GET` | `/api/v1/reportes/exportar` | Todos | Descarga oficial en `.xlsx` (`openpyxl`) o `.pdf` (`reportlab`) (HU39). |

---

### 4.2 Mecanismos de Seguridad, Autenticación y Autorización

```mermaid
sequenceDiagram
    autonumber
    actor Operario as Operario en Granja
    participant API as Backend FastAPI
    participant DB as PostgreSQL TimescaleDB

    Operario->>API: POST /auth/login con credenciales
    API->>DB: Consulta usuario por email
    DB-->>API: Retorna hash de contrasena
    API->>API: Valida contrasena con Bcrypt
    API->>API: Genera token JWT HS256 con rol y expiracion
    API-->>Operario: 200 OK con access_token Bearer
    Operario->>Operario: Guarda token en almacenamiento seguro Keystore

    Note over Operario,API: Peticion protegida a endpoint sanitario
    Operario->>API: POST /sanidad/tratamientos con Bearer Token
    API->>API: Valida firma JWT sin fallback anonimo en produccion
    API->>API: RoleChecker verifica privilegios del rol
    alt Rol Autorizado (Veterinario o Administrador)
        API->>DB: INSERT en sanidad_tratamientos con descuento FEFO
        DB-->>API: Confirmacion de insercion
        API-->>Operario: 201 Created con lote y control de retiro ICA
    else Rol No Autorizado (Operario)
        API-->>Operario: 403 Forbidden por privilegios insuficientes
    end
```

---

### 4.3 Catálogo Estándar de Códigos de Estado HTTP

| Código | Significado | Cuándo se emite en PorciTech |
| :---: | :--- | :--- |
| **`200 OK`** | Petición exitosa | Consultas, actualizaciones y descargas `.xlsx`/`.pdf` exitosas. |
| **`201 Created`** | Recurso creado | Persistencia de pesajes, animales, raciones, planes, ciclos, partos o tratamientos. |
| **`400 Bad Request`**| Violación de regla | Sobrecupo de corral, stock insuficiente, **uso de lote vencido (FEFO/ICA)** o token reset ya usado. |
| **`401 Unauthorized`**| No autenticado | Token JWT ausente, expirado o inválido (en `ENVIRONMENT=production` no hay fallback anónimo). |
| **`403 Forbidden`** | Sin autorización | Rol insuficiente para la operación solicitada. |
| **`404 Not Found`** | No encontrado | Código QR o recurso inexistente. |
| **`409 Conflict`** | Colisión de datos | Arete o código QR duplicado. |
| **`413 Payload Large`**| Imagen muy grande | Fotografía cargada superior a 15 MB. |
| **`422 Unprocessable`**| Fallo de validación | Payload Pydantic inválido o imagen donde no se detectó marcador ArUco / ejemplar porcino. |

---

### 4.4 Especificación Técnica de Interfaces (Web y Móvil)

* **Portal Web (`porcitech-nextjs`):**
  * Identidad unificada con logotipo oficial SENA (`BrandMark.jsx`), Landing Page responsiva y paneles de autenticación centrados (`/login`, `/forgot-password`, `/reset-password`).
  * Barra lateral fija en escritorio y cajón hamburguesa móvil (`DashboardSidebar.jsx`) con filtrado por rol.
  * Pasaporte Público (`/trace/[id]`) que calcula retiros farmacológicos reales desde `sanidad_tratamientos` y certifica vacunas oficiales.
* **App Móvil (`porcitech_mobile`):**
  * Splash screen animado SENA (`PorciTechSplashScreen`), selector de IP LAN en el login y catálogo real sin datos ficticios.
  * Cámara integrada en vivo (`CameraController`) con flash, cambio de cámara y selector de ángulo (`Libre`, `Lateral`, `3/4 Oblicuo`, `Superior`).
  * Módulo móvil de Alimentación y Bodega (`alimentacion_e_inventario_porcitech.dart`) + teclado gigante 64px con vibración háptica.

---

### 4.5 Diagrama de Secuencia: Sincronización Móvil Offline-First Atómica

```mermaid
sequenceDiagram
    autonumber
    actor Operario as Operario en Galpon
    participant App as App Movil Flutter
    participant Sync as Motor Sync Outbox
    participant API as Backend FastAPI
    participant DB as PostgreSQL TimescaleDB

    Operario->>App: Registra Pesaje Manual 28.5 kg Arete 4092
    App->>App: Evalua estado de red local
    Note over App,Sync: Modo Desconectado: Sin senal Wi-Fi en galpon
    App->>Sync: Encola peticion en LocalCacheService
    Sync->>Sync: Guarda payload con id_local UUID v4 en cola FIFO local
    App-->>Operario: Confirmacion de guardado en cola offline

    Note over Operario,API: Operario regresa a zona con Wi-Fi y se reintenta envio concurrente
    App->>Sync: Detecta conexion activa a red LAN
    Sync->>API: POST /pesajes/manual enviando id_local UUID v4
    API->>DB: Ejecuta lock_id_local con pg_advisory_xact_lock
    DB-->>API: Candado adquirido, inserta si id_local no existe
    API-->>Sync: 201 Created con sync_status synced
    Sync->>Sync: Elimina registro despachado de cola local
    Sync-->>App: Estado actualizado a sincronizado sin duplicados
```

---

<a name="capa-5-mantenimiento-gobernanza-y-registros-de-decisiones"></a>
# 🛡️ CAPA 5: Mantenimiento, Gobernanza y Registros de Decisiones — ISO 14764

### 5.1 Marco de Mantenimiento de Software (ISO/IEC/IEEE 14764)

```mermaid
flowchart TD
    subgraph MANTENIMIENTO ["Clasificacion de Mantenimiento ISO 14764"]
        M1["1. Mantenimiento Correctivo: Reanudacion RTSP Dahua, correccion EXIF movil y candados id_local"]
        M2["2. Mantenimiento Adaptativo: Regla FEFO ICA, auditoria de vacios sanitarios y reportes Excel/PDF"]
        M3["3. Mantenimiento Perfectivo: Motor hibrido XGBoost + ArUco multivista y camara integrada Flutter"]
        M4["4. Mantenimiento Preventivo: Compresion Chunks TimescaleDB, sanitizacion Formula Injection y backups DRP"]
    end
```

---

### 5.2 Estrategia de Registro de Actividad (Logging) y Monitoreo

* **Logs Estructurados:** Salida estándar JSON/texto con enmascaramiento estricto de credenciales RTSP (`mask_rtsp_url()`) y sin exposición de tokens de recuperación en respuestas HTTP (`reset_url_preview=None`).
* **Endpoints de Salud:** `GET /health` (comprueba conexión viva a PostgreSQL y estado de modelos IA en memoria) y `GET /api/v1/status`.

---

### 5.3 Procedimientos de Respaldo (Backups) y Recuperación ante Desastres (DRP)

```bash
# Respaldo lógico completo de TimescaleDB (diario 23:00 vía cron)
docker exec -t porcitech-db pg_dump -U postgres -d porcitech_db -Fc -f /var/lib/postgresql/data/backup_$(date +%Y%m%d_%H%M%S).dump

# Restauración ante falla crítica
docker compose down -v
docker compose up -d db
docker exec -i porcitech-db pg_restore -U postgres -d porcitech_db -c /var/lib/postgresql/data/backup_archivo.dump
```

---

### 5.4 Registros de Decisiones de Arquitectura (ADRs)

#### ADR-001: Selección de PostgreSQL 16 + TimescaleDB sobre NoSQL o MySQL
* **Decisión:** Combinar integridad relacional ACID (Kardex FEFO, genealogía, vacíos sanitarios) con hipertablas particionadas cada 7 días, índices BRIN y continuous aggregates (`cagg`) en un único motor.

#### ADR-002: Inferencia IA Embebida en RAM de FastAPI (`app.state`) vs Microservicio HTTP
* **Decisión:** Mantener `porcitech-vision` (8001) como laboratorio I+D, entrenamiento XGBoost y daemon `worker_rtsp_watcher.py`, mientras producción carga `yolo_model` y `xgb_model` en RAM del backend (`8000`) eliminando latencia de red entre contenedores.

#### ADR-003: Sincronización Móvil Offline-First con Cola Outbox FIFO
* **Decisión:** Persistir mutaciones offline en `LocalCacheService` con `id_local` (`UUID v4`) y despachar en lote al detectar conexión Wi-Fi LAN, soportando selección dinámica de IP desde la pantalla de login.

#### ADR-004: Segmentación Poligonal YOLOv8n-seg sobre Bounding Box Simple
* **Decisión:** Extraer contornos poligonales reales filtrados por clase porcina (`resolve_pig_class_ids`) para evitar error por piso vacío cuando el animal está en diagonal.

#### ADR-005: Regresión Biométrica Híbrida (XGBoost 12 Rasgos + Calibración ArUco + Multivista/EXIF)
* **Contexto:** La ecuación alométrica única de Huxley tenía desviaciones en animales con distinta conformación torácica y cuando el operario fotografiaba desde ángulos oblicuos o laterales en celular.
* **Decisión:** Implementar un regresor **XGBoost** alimentado por 12 rasgos (`area_cm2`, `largo_cm`, `ancho_cm`, `ancho_toracico_cm`, `ratio_aspecto` y 7 Momentos Invariantes de Hu), calibración **ArUco** multi-diccionario (`DICT_4X4_100`), corrección de rotación **EXIF**, factores geométricos por ángulo (`cenital`, `oblicuo`, `lateral`) y escala adaptativa móvil, conservando Huxley como fallback seguro.

#### ADR-006: Idempotencia Atómica Offline-First (`pg_advisory_xact_lock` + Índices Únicos Parciales)
* **Contexto:** Un patrón simple `SELECT -> INSERT` falla ante dos reintentos simultáneos desde la cola móvil, y la hipertabla `registro_pesos` no permite índices únicos sobre `id_local` sin incluir `tiempo`.
* **Decisión:** Implementar doble barrera: candado transaccional atómico `pg_advisory_xact_lock(hashtextextended(...))` en [`idempotency.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/core/idempotency.py) para serializar peticiones por `id_local`, más índices únicos parciales `uq_<table>_id_local` en las 7 tablas operativas estándar.

---

### 5.5 Matriz de Trazabilidad Normativa (Historias de Usuario vs Componentes)

| Historia de Usuario | Componente Afectado | Archivo Fuente Principal | Verificación de Calidad |
| :--- | :--- | :--- | :--- |
| **HU01 / HU02: Auth JWT y SMTP** | Backend / Web | [`auth.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/api/v1/endpoints/auth.py), [`email.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/core/email.py) | Tokens JWT estrictos en `production` y reset de un solo uso con validación de `Origin`. |
| **HU10: Pasaporte Sanitario QR** | Frontend Next.js | [`page.jsx`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-nextjs/src/app/trace/%5Bid%5D/page.jsx) | Cálculo real de días de retiro desde `sanidad_tratamientos`. |
| **HU21: ArUco + XGBoost + Multivista** | Backend / Lab IA / Móvil | [`pipeline.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/vision/pipeline.py), [`captura_cenital_screen.dart`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech_mobile/lib/src/features/weight_estimation/presentation/screens/captura_cenital_screen.dart) | Calibración persistente ArUco, 12 rasgos XGBoost, EXIF y cámara embebida. |
| **HU24 / HU26: Planes y FCR** | Backend / BD / Web | [`zootecnia_service.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/services/zootecnia_service.py) | Comparación FCR real vs estándar Porkcolombia por etapa y corral. |
| **HU30: Lotes Vencidos FEFO** | Backend / Web | [`zootecnia_service.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/services/zootecnia_service.py), [`ExpiringLotsBanner.jsx`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-nextjs/src/features/inventory/components/ExpiringLotsBanner.jsx) | Bloqueo `400 Bad Request` de lotes expirados y consumo multi-lote FEFO. |
| **HU32: Idempotencia Offline** | Backend / BD / Móvil | [`idempotency.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/core/idempotency.py), [`init.sql`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L618) | Candado `pg_advisory_xact_lock` + índices únicos parciales `uq_<table>_id_local`. |
| **HU38: Vacíos Sanitarios** | BD / Backend / Web | [`CorralSanitaryAuditTab.jsx`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-nextjs/src/features/animals/components/CorralSanitaryAuditTab.jsx) | Vista `vista_auditoria_vacios_corral` con ventana `LAG()`. |
| **HU39: Reportes Excel y PDF** | Backend / Web | [`reportes.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/api/v1/endpoints/reportes.py) | Exportación `.xlsx`/`.pdf` protegida contra Formula Injection y HTML Injection. |

---

<a name="referencias-normativas-y-bibliográficas"></a>
# 📚 Referencias Normativas y Bibliográficas

1. **ISO/IEC/IEEE 14764:2022:** *Software Engineering — Software Life Cycle Processes — Maintenance*.
2. **ISO/IEC/IEEE 26531:2015:** *Systems and software engineering — Content management for product life-cycle, user and task-oriented information*.
3. **ISO/IEC/IEEE 26514:2022:** *Systems and software engineering — Requirements for designers and developers of user documentation*.
4. **Servicio Nacional de Aprendizaje (SENA):** *Diseño Curricular del Programa Tecnólogo en Análisis y Desarrollo de Software (ADSO)*, Código 228118.
5. **Instituto Colombiano Agropecuario (ICA):** *Resolución 20148 de 2016 — Certificación de Granjas Porcícolas Bioseguras*.
6. **Asociación Porkcolombia:** *Guía de Buenas Prácticas Porcícolas y Parámetros Zootécnicos Nacionales*, Bogotá D.C., Colombia.
7. **Ultralytics Inc. & XGBoost Developers:** *YOLOv8 Segmentation & Gradient Boosted Decision Trees Documentation*.
8. **Timescale, Inc.:** *TimescaleDB Hypertables and Continuous Aggregates Documentation*.
