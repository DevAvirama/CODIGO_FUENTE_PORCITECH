# 🐷 MANUAL DE DISEÑO TÉCNICO DE SOFTWARE

## Sistema Integral de Gestión y Trazabilidad Porcicola y Visión Artificial.

---

### Ficha Técnica de Ingeniería del Software

- **Programa de Formación:** Tecnólogo en Análisis y Desarrollo de Software (ADSO) — Código 228118
- **Ficha de Caracterización:** 3176243
- **Centro de Formación:** Centro de Teleinformática y Producción Industrial (CTPI) — Regional Cauca
- **Servicio Nacional de Aprendizaje (SENA)**
- **Unidad Productiva Beneficiaria:** Unidad Porcícola del Centro Agropecuario SENA — Granja La Rejoya
- **Dueño del Producto (Product Owner):** Ing. Pablo Antonio Ortiz
- **Equipo de Ingeniería y Desarrollo:**
  - **Santiago Avirama** — _Líder de Arquitectura Backend y DevOps_
  - **Camilo Velasco** — _Líder de Base de Datos y Plataforma Web_
  - **Mariana Guapacha** — _Líder de Desarrollo Móvil y Experiencia de Usuario (UX)_
  - **Juan David Ocampo** — _Líder de Inteligencia Artificial y Visión Computacional_
- **Marco Metodológico Documental:** Docs-as-Code (Documentación como Código)
- **Alineación Normativa Internacional:**
  - **ISO/IEC/IEEE 14764:2022** — _Software Engineering — Software Life Cycle Processes — Maintenance_
  - **ISO/IEC/IEEE 26531:2015** — _Content Management for Product Life-Cycle, User and Task-Oriented Information_
  - **ISO/IEC/IEEE 26514:2022** — _Requirements for Designers and Developers of User Documentation_

---

### Matriz de Control de Versiones Documental (ISO/IEC/IEEE 14764)

| Versión Doc. | Versión Software |   Fecha    | Naturaleza del Cambio (Tipo de Mantenimiento)                                                   | Responsable       | Aprobación          |
| :----------: | :--------------: | :--------: | :---------------------------------------------------------------------------------------------- | :---------------- | :------------------ |
|  **v0.1.0**  |      v0.1.0      | 15/03/2025 | Creación de la estructura base y definición de las 5 capas de abstracción.                      | Santiago Avirama  | Equipo ADSO         |
|  **v1.0.0**  |      v1.0.0      | 28/05/2025 | Cierre Sprint 1: Arquitectura relacional PostgreSQL, autenticación JWT y RBAC.                  | Camilo Velasco    | Pablo A. Ortiz (PO) |
|  **v2.0.0**  |      v2.0.0      | 20/07/2025 | Cierre Sprint 2: Integración de Clean Architecture móvil en Flutter y cola Offline.             | Mariana Guapacha  | Pablo A. Ortiz (PO) |
|  **v3.0.0**  |      v3.0.0      | 15/09/2025 | Cierre Sprint 3: Modelo YOLOv8n-seg dorsal, calibración alométrica y streaming RTSP.            | Juan David Ocampo | Pablo A. Ortiz (PO) |
|  **v4.0.0**  |      v4.0.0      | 09/11/2026 | Consolidación integral PorciTech 4.0: TimescaleDB Hipertabla, Pasaporte QR ICA, Docker Compose. | Santiago Avirama  | Pablo A. Ortiz (PO) |

---

### Vinculación con Competencias Curriculares SENA ADSO

> [!NOTE]
> Este manual da cumplimiento formal a las tres competencias troncales del programa de formación ADSO:
>
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
        P2["2. Costo Alimento 75%: Descuadre de inventario y falta de calculo GMD"]
        P3["3. Riesgo Sanitario ICA: Multas y carnes con trazas de antibioticos"]
        P4["4. Desconexion Rural: Sin internet en galpon y perdida de planillas"]
    end

    subgraph SOLUCION ["Solucion PorciTech 4.0"]
        S1["Vision Artificial: Camara Cenital y YOLOv8n-seg sin estres animal"]
        S2["Kardex Automatico: Descuento de bultos a kg y calculo GMD analitico"]
        S3["Pasaporte Sanitario QR: Semaforo de retiro ICA en ruta publica trace"]
        S4["App Movil Offline-First: Cola local Outbox y teclado 64px para guantes"]
    end

    P1 --> S1
    P2 --> S2
    P3 --> S3
    P4 --> S4
```

---

### 1.2 Delimitación Estricta del Alcance (Scope)

Para garantizar la viabilidad técnica y el cumplimiento de los Sprints de desarrollo, se establecen taxativamente las fronteras del sistema:

| Dimensión          | Lo que el Sistema HACE (In Scope)                                                                                                                                                                                                     | Lo que el Sistema NO HACE (Out of Scope)                                                                        |
| :----------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------- |
| **Identificación** | Trazabilidad individual por arete visual y código QR único normalizado.                                                                                                                                                               | No soporta chips subcutáneos RFID/NFC activos (dependientes de hardware propietario).                           |
| **Pesaje**         | Estimación de peso morfométrico mediante segmentación dorsal cenital (YOLOv8) y pesaje manual de respaldo.                                                                                                                            | No realiza pesaje de cerdos en movimiento masivo sin delimitación de corral o en hacinamiento extremo.          |
| **Nutrición**      | Registro de raciones suministradas por corral, costeo automático y descuento contable del Kardex en bodega.                                                                                                                           | No dosifica tolvas mecánicas automáticamente mediante autómatas programables (PLC).                             |
| **Reproducción**   | Control de servicios, cálculo automático de fecha de parto (Ley 114 días), partos y destetes.                                                                                                                                         | No realiza análisis genómico computacional ni selección artificial molecular de semen.                          |
| **Sanidad**        | Registro de tratamientos, control de lote biológico ICA, cálculo de fechas de retiro y bloqueo en venta.                                                                                                                              | No diagnostica patologías clínicas de forma presuntiva sin criterio del médico veterinario.                     |
| **Conectividad**   | Operación desconectada total en galpón con cola local Outbox y sincronización transaccional al detectar Wi-Fi LAN.                                                                                                                    | No requiere conexión satelital directa ni sincronización P2P entre celulares sin pasar por el servidor central. |
| **Trazabilidad**   | Portal público web [`/trace/[id]`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-nextjs/src/app/trace/%5Bid%5D/page.jsx) para inspectores de frigorífico y compradores sin necesidad de login. | No emite guías de movilización oficial de ganado directamente en la plataforma SISBEN/SIGMA del ICA.            |

---

### 1.3 Matriz de Acrónimos y Glosario Técnico Estandarizado

- **ACID (Atomicity, Consistency, Isolation, Durability):** Conjunto de propiedades que garantizan la confiabilidad de las transacciones en PostgreSQL 16.
- **ADR (Architecture Decision Record):** Documento técnico que captura una decisión arquitectónica significativa, su contexto y sus consecuencias.
- **Alometría:** Estudio del cambio de proporción corporal de un ser vivo. En PorciTech, relaciona el área dorsal en $\text{cm}^2$ con la masa corporal en kilogramos.
- **ArUco:** Patrón de marcador fiduciario sintético cuadrado utilizado en visión artificial para calibrar factores de escala espaciales ($\text{px}/\text{cm}$).
- **BPP (Buenas Prácticas Porcícolas):** Normas técnicas de Porkcolombia e ICA que regulan bioseguridad, alimentación y manejo del bienestar animal.
- **BRIN (Block Range Index):** Tipo de índice en PostgreSQL diseñado para tablas ordenadas cronológicamente, reduciendo en 99% el uso de memoria respecto a B-Tree.
- **Continuous Aggregate (`cagg`):** Vista materializada de TimescaleDB que pre-computa agregaciones analíticas de forma incremental y continua.
- **Docs-as-Code:** Filosofía que trata la documentación técnica con las mismas prácticas y herramientas del código fuente (Markdown, Git, PRs, CI/CD).
- **GMD / GDP:** Ganancia Media Diaria / Ganancia Diaria de Peso. Tasa de incremento en kg o gramos por día ($\text{GMD} = \frac{\Delta \text{Peso}}{\Delta \text{Días}}$).
- **Hipertabla (Hypertable):** Abstracción de TimescaleDB que presenta una tabla particionada automáticamente en fragmentos temporales (_Chunks_) transparentes al desarrollador.
- **Idempotencia:** Capacidad de una operación de ejecutarse múltiples veces consecutivas sin cambiar el resultado del estado del sistema.
- **Kardex:** Sistema de control contable inmutable para entradas, salidas y saldos valorizados de inventario de insumos.
- **LAG():** Función analítica de ventana en SQL estándar que accede a datos de una fila previa con respecto a la fila actual dentro de una partición.
- **Outbox Pattern:** Patrón de mensajería asíncrona donde las mutaciones de datos se encolan localmente antes de despacharse a la red, garantizando entrega garantizada (_At-Least-Once_).
- **RBAC (Role-Based Access Control):** Control de acceso basado en roles (`administrador`, `veterinario`, `operario`).
- **Soft Delete:** Patrón de borrado lógico mediante la columna `deleted_at`, preservando la integridad referencial y auditoría histórica.
- **Tiempo de Retiro Farmacológico:** Periodo legal obligatorio entre la última aplicación de un medicamento veterinario y el beneficio del animal para consumo humano.
- **UUID (Universally Unique Identifier):** Identificador universal de 128 bits versión 4 (`uuid_generate_v4()`) para evitar colisiones entre registros offline y online.
- **YOLOv8n-seg:** Modelo de red neuronal convolucional de Ultralytics optimizado para segmentación de instancias en tiempo real con baja latencia.

---

### 1.4 Guía de Convenciones y Estilos de Codificación Obligatorios

| Componente            | Lenguaje / Framework   | Guía de Estilo Oficial          | Convención de Nomenclatura                                                                                                                                                  | Herramienta de Linter / Formato       |
| :-------------------- | :--------------------- | :------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------ |
| **Backend API**       | Python 3.11+ / FastAPI | PEP 8, PEP 484 (Type Hints)     | `snake_case` (funciones, variables, endpoints)<br>`PascalCase` (clases, modelos Pydantic/ORM)<br>`SCREAMING_SNAKE_CASE` (constantes)                                        | `ruff`, `black`, `flake8`             |
| **Frontend Web**      | Next.js 16 / React 19  | Airbnb JavaScript / React Style | `PascalCase` (Componentes, Vistas)<br>`camelCase` (hooks, funciones utilitarias)<br>`kebab-case` (rutas públicas `/trace/[id]`)                                             | `eslint`, `prettier`, Tailwind CSS v4 |
| **App Móvil**         | Flutter 3.12+ / Dart   | Effective Dart Specification    | `lowerCamelCase` (variables, métodos)<br>`UpperCamelCase` (clases, widgets, enums)<br>`lowercase_with_underscores` (archivos `.dart`)                                       | `flutter analyze`, `dart format`      |
| **Base de Datos**     | SQL (PostgreSQL 16)    | PostgreSQL Style Guide          | `snake_case` en minúsculas (tablas, columnas, vistas)<br>`UPPERCASE` (palabras reservadas SQL: `SELECT`, `WHERE`)<br>Prefijos analíticos: `cagg_`, `vista_`, `chk_`, `idx_` | `pgformatter`, `SQLFluff`             |
| **Control Versiones** | Git / GitHub           | Conventional Commits v1.0.0     | `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`<br>Ej: `feat(vision): calibracion automatica aruco`                                                                | Git Hooks / Pre-commit                |

---

<a name="capa-2-arquitectura-y-modelo-de-datos"></a>

# 📐 CAPA 2: Arquitectura y Modelo de Datos (Los Planos de la Casa)

### 2.1 Justificación Técnica de Patrones Arquitectónicos

El ecosistema PorciTech implementa un patrón **híbrido modular desacoplado**, compuesto por:

1. **Backend Modular en Capas (FastAPI):** Se estructura en `core/` (infraestructura, configuración, seguridad), `db/` (pool y sesiones asíncronas), `models/` (entidades ORM), `schemas/` (validación Pydantic v2), `api/v1/endpoints/` (controladores REST) y `vision/` (procesamiento multimedia). Permite aislar completamente las reglas zootécnicas de la persistencia de datos.
2. **Frontend Basado en Características (Next.js 16 App Router):** Estructura `features/` que agrupa componentes, vistas y llamadas a la API por contexto de negocio (`animals`, `inventory`, `weight`, `health`, `reproduction`). Esto facilita el mantenimiento concurrente por múltiples desarrolladores.
3. **Clean Architecture Móvil en 3 Capas (Flutter):**
   - **`domain/`:** Reglas de negocio puras e independientes de frameworks (`entities`, interfaces de repositorios que retornan `Either<Failure, T>`).
   - **`data/`:** Modelos de serialización JSON, clientes HTTP (`DioClient`) y persistencia local en caché (`LocalCacheService`).
   - **`presentation/`:** Manejadores de estado reactivos basados en **Riverpod** y widgets de ergonomía industrial.
4. **Laboratorio I+D de Visión (Microservicio Stateless):** Mantiene aislado el entorno de pruebas de visión computacional gestionado con `uv`, previniendo que dependencias pesadas de entrenamiento afecten la estabilidad del servidor transaccional principal.

---

### 2.2 Diagramas Arquitectónicos (Modelo C4)

#### Diagrama de Contexto del Sistema (Nivel 1 - C4)

```mermaid
flowchart TD
    subgraph ACTORES ["Usuarios del Sistema"]
        ADM["Administrador de Granja: Gestion, Auditoria y Usuarios"]
        VET["Medico Veterinario: Sanidad, Reproduccion y Carencias"]
        OPE["Operario de Galpon: Pesaje, Alimentacion y Manejo"]
        PUB["Inspector ICA o Comprador: Inocuidad en Frigorifico"]
    end

    subgraph ECOSISTEMA ["Plataforma Central"]
        PORCITECH["PorciTech 4.0: Gestion Zootecnica e Inteligencia Artificial"]
    end

    subgraph EXTERNOS ["Entidades y Hardware Externo"]
        CAM["Camara Dahua Biespectral: RTSP Optico y Termico"]
        BAL["Bascula Digital o Manual: Pesajes de Contingencia"]
        ICA_ENT["Porkcolombia, ICA e INVIMA: Normativas Sanitarias"]
    end

    ADM --> PORCITECH
    VET --> PORCITECH
    OPE --> PORCITECH
    PUB --> PORCITECH

    CAM --> PORCITECH
    BAL --> PORCITECH
    PORCITECH -.-> ICA_ENT
```

#### Diagrama de Contenedores (Nivel 2 - C4)

```mermaid
flowchart TB
    subgraph CLIENTES ["Capa de Clientes"]
        WEB["Portal Web Administrativo: Next.js 16 - Puerto 3000"]
        MOVIL["App Movil de Campo: Flutter 3.12 y Offline-First"]
        SCANNER["Navegador Externo: Consulta Publica Pasaporte QR"]
    end

    subgraph API_GATEWAY ["Capa Transaccional y de Negocio"]
        API["Backend Transaccional: FastAPI y SQLAlchemy 2.0 - Puerto 8000"]
        YOLO_MEM["Modelo YOLOv8n-seg en RAM: Singleton Warmup 640x640"]
        DAHUA_MNGR["DahuaStreamManager: 2 Hilos Demonio RTSP a MJPEG"]
    end

    subgraph PERSISTENCIA ["Capa de Persistencia Temporal y Relacional"]
        DB[("Base de Datos Central: PostgreSQL 16 y TimescaleDB - Puerto 5433")]
        HYPERTABLE["Hipertabla registro_pesos: Chunks semanales de 7 dias"]
        CAGGS["Vistas Continuas y Analiticas: Promedios y GMD con LAG"]
    end

    subgraph SANDBOX ["Laboratorio ID"]
        VISION_LAB["Sandbox Calibracion: FastAPI y uv - Puerto 8001 Stateless"]
    end

    WEB --> API
    MOVIL --> API
    SCANNER --> WEB

    API --- YOLO_MEM
    API --- DAHUA_MNGR
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
        MOB_1["Dispositivo Movil Operario: Galpon Precebo"]
        MOB_2["Dispositivo Movil Operario: Sala Maternidad"]
        PC_ADM["Estacion Administrativa: Navegador Web"]
    end

    subgraph SERVIDOR_HOST ["Servidor Docker Host"]
        C_DB["Contenedor porcitech-db: Puerto 5433"]
        C_API["Contenedor porcitech-api: Puerto 8000"]
        C_WEB["Contenedor porcitech-frontend: Puerto 3000"]
        C_VIS["Contenedor porcitech-vision: Puerto 8001"]
    end

    ROUTER --- CAM_IP
    ROUTER --- MOB_1
    ROUTER --- MOB_2
    ROUTER --- PC_ADM

    ROUTER --> C_API
    ROUTER --> C_WEB
    C_API --> C_DB
    C_API --- C_VIS
```

---

### 2.3 Modelo de Persistencia de Datos (PostgreSQL 16 + TimescaleDB)

El modelo de datos se compone de **15 tablas relacionales organizadas en 5 dominios de negocio**, gestionadas mediante el script [`init.sql`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql):

```mermaid
erDiagram
    USUARIOS ||--o{ MOVIMIENTOS_INVENTARIO : registra
    USUARIOS ||--o{ SANIDAD_TRATAMIENTOS : prescribe
    USUARIOS ||--o{ ALIMENTACION_RACIONES : suministra
    USUARIOS ||--o{ REPRODUCCION_SERVICIOS : realiza
    USUARIOS ||--o{ EJECUCION_BIOSEGURIDAD : ejecuta

    CORRALES ||--o{ ANIMALES : aloja
    CORRALES ||--o{ ALIMENTACION_RACIONES : consume
    CORRALES ||--o{ REGISTRO_PESOS : ubica

    ANIMALES ||--o{ ANIMALES : tiene_progenitor
    ANIMALES ||--o{ SANIDAD_TRATAMIENTOS : recibe
    ANIMALES ||--o{ REPRODUCCION_SERVICIOS : participa
    ANIMALES ||--o{ REGISTRO_PESOS : acumula

    INVENTARIO_CATEGORIAS ||--o{ INVENTARIO_ITEMS : clasifica
    INVENTARIO_ITEMS ||--o{ INVENTARIO_LOTES : contiene
    INVENTARIO_ITEMS ||--o{ MOVIMIENTOS_INVENTARIO : traza_kardex
    INVENTARIO_ITEMS ||--o{ ALIMENTACION_RACIONES : consume_stock
    INVENTARIO_LOTES ||--o{ MOVIMIENTOS_INVENTARIO : afecta_lote
    INVENTARIO_LOTES ||--o{ SANIDAD_TRATAMIENTOS : aplica_lote

    PROTOCOLOS_BIOSEGURIDAD ||--o{ EJECUCION_BIOSEGURIDAD : audita

    REPRODUCCION_SERVICIOS ||--o{ REPRODUCCION_PARTOS : origina
    REPRODUCCION_PARTOS ||--o{ REPRODUCCION_DESTETES : culmina
```

---

### 2.4 Diccionario de Datos Estandarizado (15 Tablas de Negocio)

#### Dominio 1: Núcleo y Población

##### Tabla: `usuarios` ([`init.sql#L81`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L81))

Almacena las credenciales de acceso, roles RBAC y trazabilidad de identidad del personal.

| Columna         | Tipo de Dato       | Nulo | PK/FK | Descripción                             | Restricciones / Reglas                           |
| :-------------- | :----------------- | :--: | :---: | :-------------------------------------- | :----------------------------------------------- |
| `id`            | `UUID`             |  No  |  PK   | Identificador único universal.          | `DEFAULT uuid_generate_v4()`                     |
| `nombre`        | `VARCHAR(100)`     |  No  |   -   | Nombres del usuario.                    | -                                                |
| `apellido`      | `VARCHAR(100)`     |  No  |   -   | Apellidos del usuario.                  | -                                                |
| `email`         | `VARCHAR(150)`     |  No  |   -   | Correo electrónico de inicio de sesión. | `UNIQUE`, formato email válido                   |
| `password_hash` | `VARCHAR(255)`     |  No  |   -   | Resumen hash criptográfico.             | Cifrado con `Bcrypt` (coste 12)                  |
| `rol`           | `rol_usuario_enum` |  No  |   -   | Rol para autorización RBAC.             | `'administrador'`, `'veterinario'`, `'operario'` |
| `telefono`      | `VARCHAR(20)`      |  Sí  |   -   | Número de contacto telefónico.          | -                                                |
| `activo`        | `BOOLEAN`          |  No  |   -   | Indica si el usuario puede acceder.     | `DEFAULT TRUE`                                   |
| `sync_status`   | `sync_status_type` |  No  |   -   | Estado de sincronización móvil.         | `DEFAULT 'synced'`                               |
| `created_at`    | `TIMESTAMPTZ`      |  No  |   -   | Fecha y hora de creación.               | `DEFAULT CURRENT_TIMESTAMP`                      |
| `updated_at`    | `TIMESTAMPTZ`      |  No  |   -   | Fecha de última modificación.           | Actualizado por trigger                          |
| `deleted_at`    | `TIMESTAMPTZ`      |  Sí  |   -   | Marca de tiempo para Soft Delete.       | `NULL` = registro activo                         |

##### Tabla: `corrales` ([`init.sql#L100`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L100))

Registra las divisiones físicas del galpón, su capacidad máxima y fase productiva zootécnica.

| Columna            | Tipo de Dato           | Nulo | PK/FK | Descripción                                  | Restricciones / Reglas                                                            |
| :----------------- | :--------------------- | :--: | :---: | :------------------------------------------- | :-------------------------------------------------------------------------------- |
| `id`               | `UUID`                 |  No  |  PK   | Identificador único del corral.              | `DEFAULT uuid_generate_v4()`                                                      |
| `codigo`           | `VARCHAR(20)`          |  No  |   -   | Código visible del corral (ej. `CORRAL-01`). | `UNIQUE`                                                                          |
| `nombre`           | `VARCHAR(100)`         |  No  |   -   | Nombre descriptivo del pabellón.             | -                                                                                 |
| `fase`             | `fase_productiva_enum` |  No  |   -   | Fase productiva porcina.                     | `'maternidad'`, `'precebo'`, `'levante'`, `'ceba'`, `'gestacion'`, `'cuarentena'` |
| `capacidad_maxima` | `INTEGER`              |  No  |   -   | Número máximo de animales permitidos.        | `CHECK (capacidad_maxima > 0)`                                                    |
| `descripcion`      | `TEXT`                 |  Sí  |   -   | Notas de ubicación o equipamiento.           | -                                                                                 |
| `activo`           | `BOOLEAN`              |  No  |   -   | Estado de operatividad del corral.           | `DEFAULT TRUE`                                                                    |
| `sync_status`      | `sync_status_type`     |  No  |   -   | Estado de réplica móvil.                     | `DEFAULT 'synced'`                                                                |
| `created_at`       | `TIMESTAMPTZ`          |  No  |   -   | Creación del registro.                       | `DEFAULT CURRENT_TIMESTAMP`                                                       |
| `updated_at`       | `TIMESTAMPTZ`          |  No  |   -   | Modificación del registro.                   | Actualizado por trigger                                                           |
| `deleted_at`       | `TIMESTAMPTZ`          |  Sí  |   -   | Fecha de deshabilitación lógica.             | `NULL` = activo                                                                   |

##### Tabla: `animales` ([`init.sql#L121`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L121))

Hoja de vida individual de cada ejemplar porcino, filiación genética y estado biológico.

| Columna            | Tipo de Dato         | Nulo | PK/FK | Descripción                          | Restricciones / Reglas                                                           |
| :----------------- | :------------------- | :--: | :---: | :----------------------------------- | :------------------------------------------------------------------------------- |
| `id`               | `UUID`               |  No  |  PK   | Identificador único del animal.      | `DEFAULT uuid_generate_v4()`                                                     |
| `codigo_arete`     | `VARCHAR(50)`        |  No  |   -   | Código del arete plástico visual.    | `UNIQUE`                                                                         |
| `codigo_qr`        | `VARCHAR(100)`       |  No  |   -   | Cadena codificada en el código QR.   | `UNIQUE`                                                                         |
| `nombre`           | `VARCHAR(100)`       |  Sí  |   -   | Nombre distintivo (ej. reproductor). | -                                                                                |
| `sexo`             | `VARCHAR(10)`        |  No  |   -   | Sexo biológico del porcino.          | `CHECK (sexo IN ('macho', 'hembra'))`                                            |
| `raza`             | `VARCHAR(100)`       |  No  |   -   | Raza pura o línea comercial.         | -                                                                                |
| `fecha_nacimiento` | `DATE`               |  No  |   -   | Fecha de nacimiento oficial.         | -                                                                                |
| `corral_id`        | `UUID`               |  Sí  |  FK   | Corral físico donde se encuentra.    | `REFERENCES corrales(id)`                                                        |
| `id_padre`         | `UUID`               |  Sí  |  FK   | Identificador del padre genético.    | `REFERENCES animales(id)`                                                        |
| `id_madre`         | `UUID`               |  Sí  |  FK   | Identificador de la madre genética.  | `REFERENCES animales(id)`                                                        |
| `estado`           | `estado_animal_enum` |  No  |   -   | Condición zootécnica actual.         | `'activo'`, `'lactante'`, `'gestacion'`, `'vendido'`, `'muerto'`, `'cuarentena'` |
| `peso_actual_kg`   | `NUMERIC(6,2)`       |  Sí  |   -   | Último peso consolidado en kg.       | `CHECK (peso_actual_kg >= 0)`                                                    |
| `activo`           | `BOOLEAN`            |  No  |   -   | Disponibilidad activa en inventario. | `DEFAULT TRUE`                                                                   |
| `sync_status`      | `sync_status_type`   |  No  |   -   | Estado de sincronización móvil.      | `DEFAULT 'synced'`                                                               |
| `created_at`       | `TIMESTAMPTZ`        |  No  |   -   | Registro en sistema.                 | `DEFAULT CURRENT_TIMESTAMP`                                                      |
| `updated_at`       | `TIMESTAMPTZ`        |  No  |   -   | Última actualización.                | Actualizado por trigger                                                          |
| `deleted_at`       | `TIMESTAMPTZ`        |  Sí  |   -   | Soft delete.                         | Restricción: `id <> id_padre AND id <> id_madre`                                 |

---

#### Dominio 2: Bodega, Insumos y Kardex Contable

##### Tabla: `inventario_categorias` ([`init.sql#L148`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L148))

Clasificación superior de inventario (Alimentos balanceados, Biológicos, Farmacológicos, Herramientas).

| Columna       | Tipo de Dato   | Nulo | PK/FK | Descripción                         | Restricciones                |
| :------------ | :------------- | :--: | :---: | :---------------------------------- | :--------------------------- |
| `id`          | `UUID`         |  No  |  PK   | Identificador de la categoría.      | `DEFAULT uuid_generate_v4()` |
| `nombre`      | `VARCHAR(100)` |  No  |   -   | Nombre de la categoría.             | `UNIQUE`                     |
| `descripcion` | `TEXT`         |  Sí  |   -   | Alcance zootécnico de la categoría. | -                            |
| `activo`      | `BOOLEAN`      |  No  |   -   | Estado en catálogo.                 | `DEFAULT TRUE`               |

##### Tabla: `inventario_items` ([`init.sql#L158`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L158))

Catálogo de insumos con factores de conversión de empaque a kilogramos/dosis y límites de stock.

| Columna                | Tipo de Dato    | Nulo | PK/FK | Descripción                                     | Restricciones / Reglas                 |
| :--------------------- | :-------------- | :--: | :---: | :---------------------------------------------- | :------------------------------------- |
| `id`                   | `UUID`          |  No  |  PK   | Identificador del insumo.                       | `DEFAULT uuid_generate_v4()`           |
| `categoria_id`         | `UUID`          |  No  |  FK   | Vínculo a la categoría.                         | `REFERENCES inventario_categorias(id)` |
| `nombre`               | `VARCHAR(150)`  |  No  |   -   | Nombre comercial del producto.                  | -                                      |
| `sku`                  | `VARCHAR(50)`   |  Sí  |   -   | Código interno de bodega.                       | `UNIQUE`                               |
| `unidad_medida`        | `VARCHAR(20)`   |  No  |   -   | Unidad en almacén (`Bulto`, `Frasco`, `Dosis`). | -                                      |
| `factor_conversion_kg` | `NUMERIC(8,3)`  |  No  |   -   | Equivalencia en kg (ej. 1 bulto = 40.000 kg).   | `CHECK (factor_conversion_kg > 0)`     |
| `stock_actual`         | `NUMERIC(10,2)` |  No  |   -   | Cantidad existente física en bodega.            | `CHECK (stock_actual >= 0)`            |
| `stock_minimo`         | `NUMERIC(10,2)` |  No  |   -   | Umbral para disparo de alertas rojas.           | `DEFAULT 0.00`                         |
| `costo_unitario`       | `NUMERIC(12,2)` |  No  |   -   | Valor monetario por unidad de almacén.          | `CHECK (costo_unitario >= 0)`          |

##### Tabla: `inventario_lotes` ([`init.sql#L178`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L178))

Trazabilidad de lotes de vencimiento y registro sanitario oficial expedido por el ICA.

| Columna             | Tipo de Dato    | Nulo | PK/FK | Descripción                               | Restricciones                     |
| :------------------ | :-------------- | :--: | :---: | :---------------------------------------- | :-------------------------------- |
| `id`                | `UUID`          |  No  |  PK   | Identificador del lote.                   | `DEFAULT uuid_generate_v4()`      |
| `item_id`           | `UUID`          |  No  |  FK   | Insumo al que pertenece.                  | `REFERENCES inventario_items(id)` |
| `numero_lote`       | `VARCHAR(100)`  |  No  |   -   | Código de lote impreso por el fabricante. | -                                 |
| `registro_ica`      | `VARCHAR(50)`   |  Sí  |   -   | Número de registro sanitario oficial ICA. | -                                 |
| `fecha_vencimiento` | `DATE`          |  No  |   -   | Fecha de caducidad del producto.          | -                                 |
| `cantidad_inicial`  | `NUMERIC(10,2)` |  No  |   -   | Cantidad con la que ingresó el lote.      | `CHECK (cantidad_inicial > 0)`    |
| `cantidad_actual`   | `NUMERIC(10,2)` |  No  |   -   | Saldo remanente de este lote específico.  | `CHECK (cantidad_actual >= 0)`    |
| `costo_lote`        | `NUMERIC(12,2)` |  Sí  |   -   | Costo total de adquisición del lote.      | -                                 |

##### Tabla: `movimientos_inventario` ([`init.sql#L198`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L198))

Registro inmutable de transacciones contables del Kardex (entradas de compra, consumos de galpón y ajustes).

| Columna          | Tipo de Dato                      | Nulo | PK/FK | Descripción                                | Restricciones                                                            |
| :--------------- | :-------------------------------- | :--: | :---: | :----------------------------------------- | :----------------------------------------------------------------------- |
| `id`             | `UUID`                            |  No  |  PK   | Identificador de la transacción.           | `DEFAULT uuid_generate_v4()`                                             |
| `item_id`        | `UUID`                            |  No  |  FK   | Insumo afectado.                           | `REFERENCES inventario_items(id)`                                        |
| `lote_id`        | `UUID`                            |  Sí  |  FK   | Lote específico consumido o ingresado.     | `REFERENCES inventario_lotes(id)`                                        |
| `tipo`           | `tipo_movimiento_inventario_enum` |  No  |   -   | Sentido contable.                          | `'entrada_compra'`, `'salida_consumo'`, `'ajuste_merma'`, `'devolucion'` |
| `cantidad`       | `NUMERIC(10,2)`                   |  No  |   -   | Cantidad transferida.                      | `CHECK (cantidad > 0)`                                                   |
| `costo_unitario` | `NUMERIC(12,2)`                   |  No  |   -   | Costo pactado al momento del movimiento.   | -                                                                        |
| `motivo`         | `TEXT`                            |  Sí  |   -   | Justificación de la transacción.           | -                                                                        |
| `usuario_id`     | `UUID`                            |  No  |  FK   | Operador que ejecutó la transacción.       | `REFERENCES usuarios(id)`                                                |
| `corral_id`      | `UUID`                            |  Sí  |  FK   | Corral destino (si es salida por consumo). | `REFERENCES corrales(id)`                                                |

---

#### Dominio 3: Operación Zootécnica y Sanitaria (ICA)

##### Tabla: `sanidad_tratamientos` ([`init.sql#L251`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L251))

Registro de eventos médicos, antibióticos y vacunas con cálculo obligatorio del tiempo de retiro farmacológico.

| Columna              | Tipo de Dato   | Nulo | PK/FK | Descripción                               | Restricciones / Reglas                             |
| :------------------- | :------------- | :--: | :---: | :---------------------------------------- | :------------------------------------------------- |
| `id`                 | `UUID`         |  No  |  PK   | Identificador del tratamiento médico.     | `DEFAULT uuid_generate_v4()`                       |
| `animal_id`          | `UUID`         |  No  |  FK   | Porcino que recibe el medicamento.        | `REFERENCES animales(id)`                          |
| `medicamento_id`     | `UUID`         |  No  |  FK   | Fármaco utilizado.                        | `REFERENCES inventario_items(id)`                  |
| `lote_id`            | `UUID`         |  Sí  |  FK   | Lote biológico trazable del frasco.       | `REFERENCES inventario_lotes(id)`                  |
| `dosis`              | `NUMERIC(8,2)` |  No  |   -   | Magnitud de la dosis administrada.        | `CHECK (dosis > 0)`                                |
| `unidad_dosis`       | `VARCHAR(20)`  |  No  |   -   | Unidad (`ml`, `cm3`, `g`).                | -                                                  |
| `via_administracion` | `VARCHAR(50)`  |  No  |   -   | Vía anatómica (`Intramuscular`, `Oral`).  | -                                                  |
| `diagnostico`        | `TEXT`         |  No  |   -   | Causa clínica del tratamiento.            | -                                                  |
| `tiempo_retiro_dias` | `INTEGER`      |  No  |   -   | Días de carencia oficiales según el ICA.  | `CHECK (tiempo_retiro_dias >= 0)`                  |
| `fecha_aplicacion`   | `DATE`         |  No  |   -   | Fecha en que se aplicó el producto.       | -                                                  |
| `fecha_fin_retiro`   | `DATE`         |  No  |   -   | Fecha exacta en que el cerdo queda apto.  | Calculado: `fecha_aplicacion + tiempo_retiro_dias` |
| `veterinario_id`     | `UUID`         |  No  |  FK   | Profesional que suscribe la prescripción. | `REFERENCES usuarios(id)`                          |

##### Tabla: `alimentacion_raciones` ([`init.sql#L280`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L280))

Registra las porciones de concentrado servidas por corral para costeo y análisis de conversión alimenticia.

| Columna            | Tipo de Dato    | Nulo | PK/FK | Descripción                               | Restricciones                     |
| :----------------- | :-------------- | :--: | :---: | :---------------------------------------- | :-------------------------------- |
| `id`               | `UUID`          |  No  |  PK   | Identificador del suministro.             | `DEFAULT uuid_generate_v4()`      |
| `corral_id`        | `UUID`          |  No  |  FK   | Corral alimentado.                        | `REFERENCES corrales(id)`         |
| `item_id`          | `UUID`          |  No  |  FK   | Concentrado balanceado utilizado.         | `REFERENCES inventario_items(id)` |
| `lote_id`          | `UUID`          |  Sí  |  FK   | Lote consumido.                           | `REFERENCES inventario_lotes(id)` |
| `cantidad_kg`      | `NUMERIC(8,2)`  |  No  |   -   | Masa neta administrada en kilogramos.     | `CHECK (cantidad_kg > 0)`         |
| `costo_total`      | `NUMERIC(12,2)` |  No  |   -   | Impacto monetario de la ración.           | `CHECK (costo_total >= 0)`        |
| `fecha_suministro` | `DATE`          |  No  |   -   | Fecha de consumo en el galpón.            | -                                 |
| `usuario_id`       | `UUID`          |  No  |  FK   | Operario que realizó el pesaje del bulto. | `REFERENCES usuarios(id)`         |

---

#### Dominio 4: Ciclo Reproductivo Porcino (Ley 114 Días)

##### Tabla: `reproduccion_servicios` ([`init.sql#L300`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L300))

Montas naturales o inseminaciones artificiales. Incorpora el cómputo biológico determinista de preñez.

| Columna                | Tipo de Dato  | Nulo | PK/FK | Descripción                                  | Restricciones / Reglas                                               |
| :--------------------- | :------------ | :--: | :---: | :------------------------------------------- | :------------------------------------------------------------------- |
| `id`                   | `UUID`        |  No  |  PK   | Identificador del servicio de monta.         | `DEFAULT uuid_generate_v4()`                                         |
| `cerda_id`             | `UUID`        |  No  |  FK   | Hembra receptora.                            | `REFERENCES animales(id)`                                            |
| `verraco_id`           | `UUID`        |  Sí  |  FK   | Macho reproductor o código de pajilla.       | `REFERENCES animales(id)`                                            |
| `tipo_servicio`        | `VARCHAR(50)` |  No  |   -   | Modalidad (`Monta Natural`, `Inseminacion`). | -                                                                    |
| `fecha_servicio`       | `DATE`        |  No  |   -   | Fecha de concepción.                         | -                                                                    |
| `fecha_probable_parto` | `DATE`        |  No  |   -   | **Ley biológica de los 114 días.**           | `GENERATED ALWAYS AS (fecha_servicio + '114 days'::interval) STORED` |
| `resultado`            | `VARCHAR(20)` |  No  |   -   | Confirmación gestacional.                    | `'pendiente'`, `'positivo'`, `'repetido'`, `'fallido'`               |

##### Tabla: `reproduccion_partos` ([`init.sql#L321`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L321))

Resultados cuantitativos del parto (lechones nacidos vivos, muertos, momias y biomasa total).

| Columna                | Tipo de Dato   | Nulo | PK/FK | Descripción                                    | Restricciones                           |
| :--------------------- | :------------- | :--: | :---: | :--------------------------------------------- | :-------------------------------------- |
| `id`                   | `UUID`         |  No  |  PK   | Identificador del evento de parto.             | `DEFAULT uuid_generate_v4()`            |
| `servicio_id`          | `UUID`         |  No  |  FK   | Servicio previo que originó el parto.          | `REFERENCES reproduccion_servicios(id)` |
| `cerda_id`             | `UUID`         |  No  |  FK   | Cerda madre.                                   | `REFERENCES animales(id)`               |
| `corral_maternidad_id` | `UUID`         |  No  |  FK   | Sala de maternidad asignada.                   | `REFERENCES corrales(id)`               |
| `fecha_parto`          | `DATE`         |  No  |   -   | Fecha real del alumbramiento.                  | -                                       |
| `nacidos_vivos`        | `INTEGER`      |  No  |   -   | Lechones viables (Meta Porkcolombia $\ge 12$). | `CHECK (nacidos_vivos >= 0)`            |
| `nacidos_muertos`      | `INTEGER`      |  No  |   -   | Lechones nacidos sin vida.                     | `DEFAULT 0`                             |
| `momias`               | `INTEGER`      |  No  |   -   | Fetos momificados.                             | `DEFAULT 0`                             |
| `peso_total_camada_kg` | `NUMERIC(6,2)` |  No  |   -   | Peso acumulado de los lechones vivos.          | `CHECK (peso_total_camada_kg > 0)`      |

##### Tabla: `reproduccion_destetes` ([`init.sql#L342`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L342))

Cierre de lactancia, pesaje de camada y traslado a etapa de precebo.

| Columna                 | Tipo de Dato   | Nulo | PK/FK | Descripción                               | Restricciones                        |
| :---------------------- | :------------- | :--: | :---: | :---------------------------------------- | :----------------------------------- |
| `id`                    | `UUID`         |  No  |  PK   | Identificador del destete.                | `DEFAULT uuid_generate_v4()`         |
| `parto_id`              | `UUID`         |  No  |  FK   | Parto del cual provienen los lechones.    | `REFERENCES reproduccion_partos(id)` |
| `cerda_id`              | `UUID`         |  No  |  FK   | Madre liberada de lactancia.              | `REFERENCES animales(id)`            |
| `fecha_destete`         | `DATE`         |  No  |   -   | Fecha de separación biológica.            | -                                    |
| `lechones_destetados`   | `INTEGER`      |  No  |   -   | Cantidad de lechones que pasan a precebo. | `CHECK (lechones_destetados > 0)`    |
| `peso_total_destete_kg` | `NUMERIC(6,2)` |  No  |   -   | Peso global de la camada destetada.       | `CHECK (peso_total_destete_kg > 0)`  |
| `dias_lactancia`        | `INTEGER`      |  No  |   -   | Duración calculada de la lactancia.       | `CHECK (dias_lactancia > 0)`         |

---

#### Dominio 5: Serie Temporal e Inteligencia Artificial (TimescaleDB)

##### Tabla: `registro_pesos` (HIPERTABLA) ([`init.sql#L361`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L361))

Almacena masivamente lecturas biométricas continuas generadas por cámaras cenitales IA y básculas manuales.

| Columna        | Tipo de Dato         | Nulo |       PK/FK        | Descripción                                | Restricciones / Reglas                         |
| :------------- | :------------------- | :--: | :----------------: | :----------------------------------------- | :--------------------------------------------- |
| `tiempo`       | `TIMESTAMPTZ`        |  No  | **PK (Compuesta)** | Marca de tiempo exacta del pesaje.         | Dimensión de particionamiento                  |
| `id_registro`  | `UUID`               |  No  | **PK (Compuesta)** | Identificador único de la lectura.         | `DEFAULT uuid_generate_v4()`                   |
| `id_cerdo`     | `UUID`               |  No  | **PK (Compuesta)** | Porcino evaluado.                          | Relación hacia `animales(id)`                  |
| `id_corral`    | `UUID`               |  Sí  |         FK         | Corral donde se tomó la captura.           | `REFERENCES corrales(id)`                      |
| `peso_kg`      | `NUMERIC(6,2)`       |  No  |         -          | Peso en kg (estimado por IA o báscula).    | `CHECK (peso_kg > 0 AND peso_kg <= 500)`       |
| `metodo`       | `metodo_pesaje_enum` |  No  |         -          | Origen de la medición.                     | `'vision_ai'`, `'bascula_digital'`, `'manual'` |
| `confianza_ia` | `NUMERIC(5,4)`       |  Sí  |         -          | Score de confianza de YOLOv8n-seg.         | Rango `0.0000` a `1.0000`                      |
| `area_cm2`     | `NUMERIC(8,2)`       |  Sí  |         -          | Área del polígono dorsal en $\text{cm}^2$. | Calculada por segmentación                     |
| `largo_cm`     | `NUMERIC(6,2)`       |  Sí  |         -          | Longitud axial del lomo en cm.             | Vía `cv2.minAreaRect`                          |
| `ancho_cm`     | `NUMERIC(6,2)`       |  Sí  |         -          | Amplitud transversal del lomo en cm.       | Vía `cv2.minAreaRect`                          |
| `bbox`         | `JSONB`              |  Sí  |         -          | Coordenadas `{"x1", "y1", "x2", "y2"}`.    | Bounding box en píxeles                        |
| `notas`        | `TEXT`               |  Sí  |         -          | Observaciones operativas de la toma.       | -                                              |
| `sync_status`  | `sync_status_type`   |  No  |         -          | Estado de sincronización móvil.            | `DEFAULT 'synced'`                             |

> [!IMPORTANT]
> **Particionamiento y Llave Primaria en TimescaleDB:**
> Se ejecuta formalmente: `PERFORM create_hypertable('registro_pesos', by_range('tiempo', INTERVAL '7 days'));`.
> Por exigencia de TimescaleDB, la clave primaria **debe incluir obligatoriamente la columna de particionamiento temporal**:
>
> ```sql
> CONSTRAINT pk_registro_pesos PRIMARY KEY (tiempo, id_registro, id_cerdo)
> ```
>
> Para acelerar consultas cronológicas se utilizan índices **BRIN** (`idx_registro_pesos_brin_tiempo`) que reducen el consumo de almacenamiento y RAM en comparación con índices B-Tree estándar.

---

### 2.5 Vistas Materializadas Continuas y Analítica Avanzada

#### 1. Vista Agregada Continua: `cagg_pesos_diarios_corral` ([`init.sql#L507`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L507))

Pre-calcula en segundo plano el comportamiento estadístico diario de peso por corral sin sobrecargar la CPU:

```sql
CREATE MATERIALIZED VIEW cagg_pesos_diarios_corral
WITH (timescaledb.continuous) AS
SELECT
    time_bucket('1 day', tiempo) AS dia_bucket,
    id_corral,
    COUNT(*) AS total_pesajes,
    ROUND(AVG(peso_kg), 2) AS peso_promedio_kg,
    MIN(peso_kg) AS peso_minimo_kg,
    MAX(peso_kg) AS peso_maximo_kg
FROM registro_pesos
WHERE id_corral IS NOT NULL
GROUP BY dia_bucket, id_corral
WITH NO DATA;
```

_Se actualiza de forma automática cada hora mediante `add_continuous_aggregate_policy`._

#### 2. Vista Analítica de Ganancia Diaria: `vista_gmd_diaria_corral` ([`init.sql#L527`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L527))

Aplica la función de ventana `LAG()` sobre la vista continua para obtener la tasa de crecimiento real expresada en gramos/día:

```sql
CREATE OR REPLACE VIEW vista_gmd_diaria_corral AS
WITH pesos_ordenados AS (
    SELECT
        dia_bucket,
        id_corral,
        total_pesajes,
        peso_promedio_kg,
        LAG(peso_promedio_kg) OVER (PARTITION BY id_corral ORDER BY dia_bucket) AS peso_anterior_kg,
        LAG(dia_bucket) OVER (PARTITION BY id_corral ORDER BY dia_bucket) AS dia_anterior_bucket
    FROM cagg_pesos_diarios_corral
)
SELECT
    dia_bucket,
    id_corral,
    total_pesajes,
    peso_promedio_kg,
    peso_anterior_kg,
    (peso_promedio_kg - peso_anterior_kg) AS ganancia_peso_kg,
    (dia_bucket::date - dia_anterior_bucket::date) AS dias_transcurridos,
    CASE
        WHEN peso_anterior_kg IS NOT NULL AND (dia_bucket::date - dia_anterior_bucket::date) > 0 THEN
            ROUND((((peso_promedio_kg - peso_anterior_kg) / (dia_bucket::date - dia_anterior_bucket::date)) * 1000.0), 1)
        ELSE NULL
    END AS gmd_estimada_gramos_dia
FROM pesos_ordenados;
```

---

<a name="capa-3-operación-entorno-y-despliegue"></a>

# ⚙️ CAPA 3: Operación, Entorno y Despliegue (El Manual de Armado)

### 3.1 Requisitos Previos del Sistema

| Componente             | Requisito Mínimo (Entorno Pruebas / Dev)                     | Requisito Recomendado (Producción en Granja)                         |
| :--------------------- | :----------------------------------------------------------- | :------------------------------------------------------------------- |
| **Arquitectura Host**  | x86_64 (Intel Core i5 8ª Gen / AMD Ryzen 5)                  | x86_64 (Intel Core i7 11ª Gen / Servidor Xeon / GPU NVIDIA opcional) |
| **Memoria RAM**        | 8 GB de RAM disponible                                       | 16 GB - 32 GB DDR4/DDR5                                              |
| **Almacenamiento**     | 20 GB de espacio libre (Disco SSD)                           | 120 GB SSD NVMe (Persistencia de Chunks y Snapshots de Cámara)       |
| **Sistema Operativo**  | Linux (Ubuntu 22.04 LTS / Debian 12), Windows 10/11 con WSL2 | Ubuntu Server 22.04 LTS o 24.04 LTS                                  |
| **Motor Contenedores** | Docker Engine 24.0+ y Docker Compose v2.20+                  | Docker Engine Enterprise / Compose v2.26+                            |
| **Red**                | Tarjeta de red Ethernet 100 Mbps                             | Tarjeta Gigabit Ethernet (1000 Mbps) con Switch para tráfico RTSP    |
| **Dispositivo Móvil**  | Android 8.0 (Oreo) o iOS 13+ con cámara de 12 MP             | Android 11+ con lente gran angular, 4 GB RAM y certificación IP68    |

---

### 3.2 Matriz y Plantilla Comentada de Variables de Entorno (`.env`)

Archivo maestro de configuración del entorno host:

```bash
# =============================================================================
# VARIABLES DE ENTORNO — PLATAFORMA PORCITECH 4.0
# =============================================================================

# --- 1. CONFIGURACIÓN GENERAL Y ENTORNO ---
ENVIRONMENT=development
TZ=America/Bogota
PGTZ=America/Bogota

# --- 2. BASE DE DATOS (PostgreSQL 16 + TimescaleDB) ---
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=porcitech_db
DB_HOST=db
DB_PORT=5433
DATABASE_URL=postgresql+asyncpg://postgres:postgres@db:5432/porcitech_db

# --- 3. BACKEND API (FastAPI) ---
API_HOST=0.0.0.0
API_PORT=8000
SECRET_KEY=clave_secreta_jwt_porcitech_desarrollo_sena_2026
ACCESS_TOKEN_EXPIRE_MINUTES=480

# Expresión regular para autorizar conexiones desde cualquier dispositivo en la LAN privada
CORS_ORIGIN_REGEX=https?://(localhost|127\.0\.0\.1|192\.168\.\d+\.\d+|10\.\d+\.\d+\.\d+|172\.(1[6-9]|2\d|3[0-1])\.\d+\.\d+|[a-zA-Z0-9-]+(\.local)?)(:\d+)?
CORS_ORIGINS=["http://localhost:3000", "http://127.0.0.1:3000"]

# --- 4. CÁMARA INDUSTRIAL DAHUA TPC-BF (RTSP STREAMING) ---
DAHUA_CAMERA_IP=192.168.1.108
DAHUA_CAMERA_PORT=554
DAHUA_CAMERA_USER=admin
DAHUA_CAMERA_PASSWORD=admin123
DAHUA_RTSP_URL=rtsp://admin:admin123@192.168.1.108:554/cam/realmonitor?channel=1&subtype=0

# --- 5. FRONTEND WEB (Next.js 16) ---
# Dejar en blanco para autodescubrimiento por ventana del navegador hacia la IP LAN
NEXT_PUBLIC_API_URL=
INTERNAL_API_URL=http://api:8000/api/v1
```

---

### 3.3 Orquestación con Docker Compose ([`docker-compose.yml`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/docker-compose.yml))

El archivo [`docker-compose.yml`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/docker-compose.yml) gestiona los 4 servicios sobre la red bridge `porcitech-net`:

1. **`porcitech-db` (TimescaleDB):** Expone puerto `5433:5432`. Monta el volumen persistente `porcitech_pgdata` e inicializa el esquema con `./porcitech-backend/scripts/init.sql` mediante `docker-entrypoint-initdb.d`. Verifica salud con `pg_isready`.
2. **`porcitech-api` (FastAPI):** Expone puerto `8000:8000`. Depende de que `porcitech-db` esté `healthy`. Realiza el Warmup de PyTorch y expone healthcheck en `/health`.
3. **`porcitech-frontend` (Next.js):** Expone puerto `3000:3000`. Depende de que `porcitech-api` esté `healthy`.
4. **`porcitech-vision` (Laboratorio Sandbox):** Expone puerto `8001:8001` de forma aislada.

---

### 3.4 Guía Paso a Paso para Instalación y Despliegue Automatizado

#### Paso 1: Clonación del Código y Preparación del Entorno

```bash
# Ubicarse en el directorio de trabajo
cd /home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH

# Otorgar permisos de ejecución al script maestro
chmod +x deploy.sh
```

#### Paso 2: Ejecución del Script de Despliegue Automatizado ([`deploy.sh`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/deploy.sh))

```bash
./deploy.sh
```

_El script detectará automáticamente la IP de red local (LAN) de la máquina host, creará la red `porcitech-net`, compilará las imágenes Docker con cache inteligente y esperará la señal de salud de PostgreSQL._

#### Paso 3: Poblado Opcional del Dataset Demostrativo

Para cargar los 5 usuarios de prueba, lotes porcinos, curvas de crecimiento y tratamientos con tiempos de retiro activos:

```bash
docker exec -i porcitech-db psql -U postgres -d porcitech_db < ScriptsSQL/seed_demo.sql
```

#### Paso 4: Verificación de Puntos de Acceso

- **Portal Web Administrativo:** `http://localhost:3000` (o `http://<IP_LOCAL>:3000`)
- **Documentación Interactiva Swagger / OpenAPI:** `http://localhost:8000/api/v1/docs`
- **Especificación OpenAPI en Formato JSON:** `http://localhost:8000/api/v1/openapi.json`
- **Sandbox I+D de Visión Artificial:** `http://localhost:8001/docs`
- **Conexión Directa a Base de Datos:** `localhost:5433` (`usuario: postgres`, `clave: postgres`, `bd: porcitech_db`)

---

### 3.5 Compilación y Ejecución de la App Móvil ([`porcitech_mobile`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech_mobile))

```bash
cd porcitech_mobile

# 1. Obtener dependencias de pub.dev
flutter pub get

# 2. Compilar APK Release para teléfonos Android de operarios en galpón
flutter build apk --release

# 3. O ejecutar en modo depuración conectado por cable USB o Wi-Fi
flutter run
```

---

<a name="capa-4-apis-contratos-e-interfaces"></a>

# 🌉 CAPA 4: APIs, Contratos e Interfaces (Los Puentes de Comunicación)

### 4.1 Especificación de Endpoints RESTful (`/api/v1`)

Todos los servicios consumen y producen cargas con cabecera `Content-Type: application/json` (excepto inferencia de visión que usa `multipart/form-data` y streaming que usa `multipart/x-mixed-replace`).

| Módulo           | Método | Endpoint                           | Roles Permitidos           | Parámetros / Payload JSON                                      | Respuesta Exitosa (200 / 201)                                               |
| :--------------- | :----: | :--------------------------------- | :------------------------- | :------------------------------------------------------------- | :-------------------------------------------------------------------------- |
| **Auth**         | `POST` | `/api/v1/auth/login`               | Público                    | `OAuth2PasswordRequestForm` (`username`, `password`)           | `{"access_token": "...", "token_type": "bearer", "user": {...}}`            |
| **Auth**         | `GET`  | `/api/v1/auth/me`                  | Todos                      | Header `Authorization: Bearer <JWT>`                           | Perfil del usuario autenticado y su rol.                                    |
| **Usuarios**     | `GET`  | `/api/v1/usuarios/`                | `administrador`            | `skip=0&limit=50`                                              | Lista paginada de usuarios registrados.                                     |
| **Usuarios**     | `POST` | `/api/v1/usuarios/`                | `administrador`            | `UserCreate` (`email`, `nombre`, `rol`, `password`)            | `201 Created` con nuevo usuario creado.                                     |
| **Corrales**     | `GET`  | `/api/v1/corrales/`                | Todos                      | `activo=true`                                                  | Listado de corrales con ocupación actual vs capacidad máxima.               |
| **Animales**     | `GET`  | `/api/v1/animales/`                | Todos                      | Filtros: `corral_id`, `estado`, `sexo`                         | Colección de porcinos con peso y estado biológico.                          |
| **Animales**     | `POST` | `/api/v1/animales/`                | `operario`, `vet`, `admin` | `AnimalCreate` (`codigo_arete`, `codigo_qr`, `corral_id`, ...) | `201 Created`. Aplica bloqueo pesimista `FOR UPDATE` en corral.             |
| **Animales**     | `GET`  | `/api/v1/animales/{id}/genealogia` | Todos                      | Path: `id` (UUID del animal)                                   | Árbol genealógico recursivo: animal, padre y madre.                         |
| **Pesajes**      | `POST` | `/api/v1/pesajes/manual`           | `operario`, `vet`, `admin` | `PesajeManualCreate` (`id_cerdo`, `peso_kg`, `notas`)          | `201 Created`. Inserta en Hipertabla y actualiza `peso_actual_kg`.          |
| **Pesajes**      | `POST` | `/api/v1/pesajes/vision`           | `operario`, `vet`, `admin` | `multipart/form-data`: `file` (imagen) + `id_cerdo`            | Inferencia YOLOv8 en RAM: retorna `peso_estimado`, `area_cm2`, `confianza`. |
| **Pesajes**      | `GET`  | `/api/v1/pesajes/stream/live`      | Todos                      | Query: `channel=1` (óptico) o `2` (térmico)                    | Stream de video MJPEG continuo con HUD CCTV.                                |
| **Pesajes**      | `GET`  | `/api/v1/pesajes/stream/metrics`   | Todos                      | -                                                              | JSON en tiempo real con última confianza, área y peso del stream.           |
| **Pesajes**      | `POST` | `/api/v1/pesajes/capturar-en-vivo` | `operario`, `vet`, `admin` | `id_cerdo`                                                     | Congela fotograma de Dahua, procesa YOLO e inserta en BD.                   |
| **Inventario**   | `GET`  | `/api/v1/inventario/items`         | Todos                      | Filtros de stock bajo                                          | Catálogo de insumos con factor de conversión bulto/kg.                      |
| **Inventario**   | `POST` | `/api/v1/inventario/movimientos`   | `vet`, `admin`             | `MovimientoCreate` (`item_id`, `tipo`, `cantidad`)             | Actualiza Kardex y stock en transacción protegida con locks.                |
| **Alimentación** | `POST` | `/api/v1/alimentacion/raciones`    | `operario`, `vet`, `admin` | `RacionCreate` (`corral_id`, `item_id`, `cantidad_kg`)         | Convierte kg a bultos, descuenta inventario y registra salida.              |
| **Sanidad**      | `POST` | `/api/v1/sanidad/tratamientos`     | `veterinario`, `admin`     | `TratamientoCreate` (`animal_id`, `medicamento_id`, ...)       | Graba tratamiento y calcula `fecha_fin_retiro` (Regla ICA).                 |
| **Sanidad**      | `GET`  | `/api/v1/sanidad/alertas-retiro`   | Todos                      | -                                                              | Listado de cerdos en periodo de carencia (retiro activo).                   |
| **Reproducción** | `POST` | `/api/v1/reproduccion/servicios`   | `operario`, `vet`, `admin` | `ServicioCreate` (`cerda_id`, `fecha_servicio`)                | Graba monta; BD calcula automáticamente fecha parto (+114 días).            |
| **Reproducción** | `POST` | `/api/v1/reproduccion/partos`      | `operario`, `vet`, `admin` | `PartoCreate` (`servicio_id`, `nacidos_vivos`, ...)            | Cambia estado de la cerda a `'lactante'`.                                   |
| **Reproducción** | `POST` | `/api/v1/reproduccion/destetes`    | `operario`, `vet`, `admin` | `DesteteCreate` (`parto_id`, `lechones_destetados`)            | Calcula `dias_lactancia` y regresa cerda a `'activo'`.                      |
| **Dashboard**    | `GET`  | `/api/v1/dashboard/kpis`           | Todos                      | -                                                              | Métricas consolidadas: cabezas, corrales, alertas de parto y retiro.        |
| **Dashboard**    | `GET`  | `/api/v1/dashboard/curvas-gmd`     | Todos                      | Query: `corral_id`                                             | Lectura de `vista_gmd_diaria_corral` generada con función `LAG()`.          |

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
    API->>API: Valida firma de token y extrae claims
    API->>API: RoleChecker verifica privilegios del rol
    alt Rol Autorizado (Veterinario o Administrador)
        API->>DB: INSERT en sanidad_tratamientos
        DB-->>API: Confirmacion de insercion
        API-->>Operario: 201 Created con fecha fin de retiro ICA
    else Rol No Autorizado (Operario)
        API-->>Operario: 403 Forbidden por privilegios insuficientes
    end
```

---

### 4.3 Catálogo Estándar de Códigos de Estado HTTP y Errores

|          Código          | Significado HTTP    | Cuándo se emite en PorciTech                                                           | Estructura de Respuesta                                                               |
| :----------------------: | :------------------ | :------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------ |
|       **`200 OK`**       | Petición exitosa    | Consultas `GET` y actualizaciones exitosas.                                            | Objeto JSON solicitado.                                                               |
|    **`201 Created`**     | Recurso creado      | Inserción confirmada de un pesaje, animal, parto o ración.                             | Objeto recién persistido con su `UUID`.                                               |
|  **`400 Bad Request`**   | Violación de regla  | Sobrecupo en corral, stock insuficiente en bodega o valor biológico absurdo (>500 kg). | `{"detail": "El corral ha alcanzado su capacidad máxima permitida."}`                 |
|  **`401 Unauthorized`**  | No autenticado      | Token JWT expirado, ausente o manipulado.                                              | `{"detail": "No se pudieron validar las credenciales"}`                               |
|   **`403 Forbidden`**    | Sin autorización    | Un operario intentando recetar fármacos o un usuario inactivo.                         | `{"detail": "Operación reservada para Médicos Veterinarios o Administradores"}`       |
|   **`404 Not Found`**    | Recurso inexistente | Arete QR no registrado o ID de animal no encontrado.                                   | `{"detail": "Porcino con arete visual no encontrado"}`                                |
|    **`409 Conflict`**    | Colisión de datos   | Intento de registrar un arete o código QR duplicado.                                   | `{"detail": "Ya existe un animal registrado con el código de arete suministrado"}`    |
| **`422 Unprocessable`**  | Fallo validación    | Payload JSON no cumple el esquema Pydantic v2.                                         | `{"detail": [{"loc": ["body", "peso_kg"], "msg": "Input should be greater than 0"}]}` |
| **`500 Internal Error`** | Falla no capturada  | Pérdida de enlace con hardware Dahua o falla crítica de red.                           | `{"detail": "Error interno del servidor procesando la solicitud"}`                    |

---

### 4.4 Especificación de Interfaces de Usuario (UI/UX)

#### A. Portal Web Administrativo (Next.js 16)

- **Pasaporte Sanitario QR Público ([`/trace/[id]`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-nextjs/src/app/trace/%5Bid%5D/page.jsx)):**
  Página estática/SSR pública sin barrera de autenticación. Al ser escaneada en el frigorífico:
  - Si `dias_retiro_restantes == 0`: Muestra sello verde oficial **"APTO PARA BENEFICIO Y CONSUMO HUMANO (ICA / INVIMA)"**.
  - Si `dias_retiro_restantes > 0`: Despliega bandera roja bloqueante **"PERIODO DE CARENCIA ACTIVO — NO APTO PARA SACRIFICIO"**, indicando fármaco, fecha de aplicación y días exactos faltantes para inocuidad cárnica.
- **Monitor CCTV con HUD en Vivo ([`WeightView.jsx`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-nextjs/src/features/weight/WeightView.jsx)):**
  Renderiza la transmisión MJPEG nativa generada por el backend con superposición de tarjeta HUD (área en $\text{cm}^2$, confianza de YOLO y peso proyectado en tiempo real). Botón de captura inmediata para congelar y guardar en TimescaleDB.

#### B. Aplicación Móvil en Campo (Flutter 3.12)

- **Ergonomía Glove-Friendly para Galpón:**
  - Teclado numérico gigante ([`GiantNumericKeypad`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech_mobile/lib/src/core/widgets/giant_numeric_keypad.dart)) con teclas de 64 píxeles de altura y confirmación háptica (`HapticFeedback.lightImpact()`) para operarios que utilizan guantes de bioseguridad húmedos.
  - Escáner QR animado con visor láser (`mobile_scanner`) para lectura instantánea de aretes sin tocar la pantalla.
  - Pre-procesamiento de fotos cenitales en el borde: redimensiona automáticamente las fotos de cámara a $1280 \times 1280$ píxeles al 85% de compresión JPEG, reduciendo el peso de subida de 8 MB a ~180 KB.

---

### 4.5 Diagrama de Secuencia: Flujo de Sincronización Móvil Offline-First

```mermaid
sequenceDiagram
    autonumber
    actor Operario as Operario en Galpon
    participant App as App Movil Flutter
    participant Sync as Motor Sync Outbox
    participant API as Backend FastAPI
    participant DB as TimescaleDB

    Operario->>App: Registra Pesaje Manual 28.5 kg Arete 4092
    App->>App: Evalua estado de red local
    Note over App,Sync: Modo Desconectado: Sin senal Wi-Fi en galpon
    App->>Sync: Encola peticion en LocalCacheService
    Sync->>Sync: Guarda payload con id_local UUID v4 en cola local
    App-->>Operario: Confirmacion de guardado en cola offline

    Note over Operario,API: Operario regresa a zona con Wi-Fi en granja
    App->>Sync: Detecta conexion activa a red LAN
    Sync->>API: POST /pesajes/manual enviando id_local UUID v4
    API->>DB: Insercion idempotente en tabla registro_pesos
    DB-->>API: Persistencia confirmada en Hipertabla
    API-->>Sync: 201 Created con sync_status synced
    Sync->>Sync: Elimina registro despachado de cola local
    Sync-->>App: Estado actualizado a sincronizado
```

---

<a name="capa-5-mantenimiento-gobernanza-y-registros-de-decisiones"></a>

# 🛡️ CAPA 5: Mantenimiento, Gobernanza y Registros de Decisiones — ISO 14764

### 5.1 Marco de Mantenimiento de Software (ISO/IEC/IEEE 14764)

El estándar internacional ISO/IEC/IEEE 14764 clasifica las actividades de evolución del software en cuatro tipologías. En PorciTech, estas se aplican de la siguiente manera:

```mermaid
flowchart TD
    subgraph MANTENIMIENTO ["Clasificacion de Mantenimiento ISO 14764"]
        M1["1. Mantenimiento Correctivo: Reanudacion automatica de stream RTSP ante cortes de camara"]
        M2["2. Mantenimiento Adaptativo: Actualizacion de tiempos de retiro segun resoluciones ICA"]
        M3["3. Mantenimiento Perfectivo: Reentrenamiento de YOLO con dataset local para subir precision"]
        M4["4. Mantenimiento Preventivo: Compresion automatica de Chunks en TimescaleDB y backups DRP"]
    end
```

---

### 5.2 Estrategia de Registro de Actividad (Logging) y Monitoreo de Salud

- **Estructura de Logs:** Formato estructurado JSON en consola estándar (`stdout`), compatible con colectores Docker:
  ```json
  {
    "timestamp": "2026-11-09T14:00:00Z",
    "level": "INFO",
    "service": "porcitech-api",
    "module": "vision.pipeline",
    "event": "yolo_inference_completed",
    "latency_ms": 84,
    "confidence": 0.962
  }
  ```
- **Endpoints de Monitoreo:**
  - `GET /health`: Comprueba la conectividad viva hacia PostgreSQL/TimescaleDB y el estado en memoria del modelo YOLO. Si la base de datos se cae, responde `503 Service Unavailable`.
  - `GET /api/v1/status`: Retorna la versión activa de la API y confirmación de los routers registrados.

---

### 5.3 Procedimientos de Respaldo (Backups) y Recuperación ante Desastres (DRP)

#### Política de Copias de Seguridad

1. **Frecuencia:** Copia lógica completa automatizada diariamente a las 23:00 horas mediante tarea `cron` del servidor host.
2. **Retención:** 30 días de respaldos rotativos diarios, 12 respaldos mensuales acumulados.

#### Comando de Respaldo Automatizado

```bash
# Generación de copia de seguridad con pg_dump comprimido
docker exec -t porcitech-db pg_dump -U postgres -d porcitech_db -Fc -f /var/lib/postgresql/data/backup_$(date +%Y%m%d_%H%M%S).dump
```

#### Procedimiento de Restauración (Disaster Recovery)

```bash
# En caso de falla catastrófica de hardware:
docker compose down -v
docker compose up -d db
docker exec -i porcitech-db pg_restore -U postgres -d porcitech_db -c /var/lib/postgresql/data/backup_archivo.dump
```

---

### 5.4 Registros de Decisiones de Arquitectura (Architecture Decision Records — ADRs)

#### ADR-001: Selección de PostgreSQL 16 + TimescaleDB sobre Motores NoSQL o MySQL Puro

- **Estado:** Aprobado
- **Contexto:** PorciTech requería transacciones ACID inmutables para el Kardex contable y las relaciones genealógicas 3FN, pero simultáneamente debía procesar millones de mediciones temporales de cámaras IA a 20 FPS sin ralentizar las consultas del Dashboard.
- **Decisión:** Adoptar PostgreSQL 16 con la extensión TimescaleDB.
- **Consecuencias Positivas:** Manejo nativo de series de tiempo mediante Hipertablas particionadas cada 7 días, índices BRIN de bajo consumo de memoria y vistas continuas (`cagg`) para GMD en tiempo real con sintaxis analítica SQL estándar (`LAG()`).
- **Consecuencias Negativas:** Mayor curva de aprendizaje para el equipo en la configuración de políticas de agregación continua y exigencia de clave primaria compuesta (`tiempo, id_registro, id_cerdo`).

#### ADR-002: Inferencia de YOLOv8 Embebida en Memoria RAM de FastAPI (`app.state.yolo_model`)

- **Estado:** Aprobado
- **Contexto:** En el diseño inicial, se evaluó un microservicio HTTP desacoplado en el puerto 8001 para procesar fotos. Sin embargo, para la cámara Dahua transmitiendo a 20 FPS, enviar tramas Full HD (6 MB) por red HTTP interna entre dos contenedores Docker generaba congestión de socket y latencias superiores a 800 ms.
- **Decisión:** Mantener el puerto 8001 exclusivamente como laboratorio I+D _stateless_ e integrar el modelo de inferencia en producción directamente en la memoria RAM del backend (`porcitech-api`), orquestado en `lifespan.py` y protegido con `asyncio.to_thread` y `yolo_lock`.
- **Consecuencias Positivas:** Latencia de inferencia reducida a menos de 90 ms por fotograma, streaming MJPEG fluido sin pérdida de paquetes y eliminación del cuello de botella de red entre contenedores.

#### ADR-003: Sincronización Móvil Offline-First con Patrón Outbox FIFO y Claves UUID v4

- **Estado:** Aprobado
- **Contexto:** Las naves de producción porcícola presentan zonas ciegas de radiofrecuencia. Si la aplicación dependiera de conexión síncrona continua, los operarios perderían registros de partos, pesajes y medicación.
- **Decisión:** Implementar persistencia local en Flutter mediante `LocalCacheService` con cola FIFO de peticiones protegidas con `UUID v4` e inserciones idempotentes en FastAPI.
- **Consecuencias Positivas:** Cero pérdida de información en campo. Sincronización transparente y en lote en cuanto el dispositivo detecta la señal Wi-Fi de la oficina de la granja.

#### ADR-004: Segmentación Dorsal con YOLOv8n-seg y Ecuación Alométrica Potencial

- **Estado:** Aprobado
- **Contexto:** La estimación tradicional basada en cajas rectangulares simples (_Bounding Box_) fallaba significativamente cuando los cerdos estaban orientados en diagonal dentro del corral, computando piso vacío como masa corporal con errores de pesaje superiores al 25%.
- **Decisión:** Entrenar un modelo de segmentación de instancias poligonal (`yolov8n-seg`) que mide exclusivamente el contorno dorsal en píxeles, convirtiéndolo a $\text{cm}^2$ mediante normalización dinámica de resolución y aplicando la ecuación potencial zootécnica:
  $$\text{Peso (kg)} = 0.0245 \times (\text{Área}_{\text{cm}^2})^{1.052}$$
- **Consecuencias Positivas:** Error porcentual absoluto medio (MAPE) reducido por debajo del 4.2% frente a la báscula de pesaje mecánico de control.

---

### 5.5 Matriz de Trazabilidad Normativa (Historias de Usuario vs Componentes)

| Historia de Usuario (Backlog)        | Componente Afectado  | Archivo Fuente Principal                                                                                                                                                                                                         | Tarea Scrum Asociada | Criterio de Verificación de Calidad                         |
| :----------------------------------- | :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------: | :---------------------------------------------------------- |
| **HU01: Autenticación JWT**          | Backend / BD / Móvil | [`security.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/core/security.py)                                                                                               |         T01          | Entrega de token bearer válido con expiración en 8 horas.   |
| **HU05: Registro de Animal y QR**    | Backend / Web / BD   | [`animales.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/api/v1/endpoints/animales.py)                                                                                   |         T04          | Validación de unicidad de arete y código QR.                |
| **HU10: Pasaporte Sanitario QR**     | Frontend Next.js     | [`page.jsx`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-nextjs/src/app/trace/%5Bid%5D/page.jsx)                                                                                        |         T08          | Acceso público sin login con semáforo de carencia ICA.      |
| **HU11: Vacunación en Galpón**       | App Móvil Flutter    | [`registro_de_vacunacion_porcitech.dart`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech_mobile/lib/src/features/health_record/presentation/screens/registro_de_vacunacion_porcitech.dart) |         T09          | Asignación obligatoria de lote y tiempo de retiro.          |
| **HU13: Kardex Automático**          | Backend FastAPI      | [`alimentacion.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/api/v1/endpoints/alimentacion.py)                                                                           |         T11          | Bloqueo `FOR UPDATE` y descuento de bultos por kg servidos. |
| **HU21: Pesaje Dorsal IA**           | Backend Visión / IA  | [`pipeline.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/vision/pipeline.py)                                                                                             |         T15          | Inferencia YOLOv8n-seg con error MAPE $< 5\%$.              |
| **HU31: Modo Offline Local**         | App Móvil Flutter    | [`local_cache_service.dart`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech_mobile/lib/src/core/storage/local_cache_service.dart)                                                          |         T18          | Persistencia local sin red en cola FIFO.                    |
| **HU32: Sincronización Idempotente** | Backend / Móvil      | [`pesajes.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/api/v1/endpoints/pesajes.py)                                                                                     |         T20          | Ingesta segura por UUID v4 evitando duplicados.             |
| **HU37: Curvas de Crecimiento GMD**  | Base de Datos / Web  | [`init.sql`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/ScriptsSQL/init.sql#L527)                                                                                                                |         T21          | Cálculo de GMD mediante función SQL `LAG()`.                |
| **HU40: Conector RTSP Dahua**        | Backend Visión       | [`dahua_stream.py`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/porcitech-backend/app/vision/dahua_stream.py)                                                                                     |         T23          | Stream H.264 continuo a 20 FPS con auto-pausa a 45s.        |

---

<a name="referencias-normativas-y-bibliográficas"></a>

# 📚 Referencias Normativas y Bibliográficas

1. **ISO/IEC/IEEE 14764:2022:** _Software Engineering — Software Life Cycle Processes — Maintenance_. International Organization for Standardization / IEEE Computer Society.
2. **ISO/IEC/IEEE 26531:2015:** _Systems and software engineering — Content management for product life-cycle, user and task-oriented information_.
3. **ISO/IEC/IEEE 26514:2022:** _Systems and software engineering — Requirements for designers and developers of user documentation_.
4. **Servicio Nacional de Aprendizaje (SENA):** _Diseño Curricular del Programa Tecnólogo en Análisis y Desarrollo de Software (ADSO)_, Código 228118, Red de Conocimiento en Informática, Diseño y Desarrollo de Software, Colombia.
5. **Instituto Colombiano Agropecuario (ICA):** _Resolución 20148 de 2016 — Por medio de la cual se establecen los requisitos y el procedimiento para la certificación de Granjas Porcícolas Bioseguras_.
6. **Asociación Porkcolombia — Fondo Nacional de la Porcicultura:** _Guía de Buenas Prácticas Porcícolas y Parámetros Zootécnicos Nacionales_, Bogotá D.C., Colombia.
7. **Ultralytics Inc.:** _YOLOv8: State-of-the-Art Computer Vision and Real-time Object Segmentation Models Documentation_, 2024.
8. **Timescale, Inc.:** _TimescaleDB: Time-series database architecture and Continuous Aggregates Documentation_, PostgreSQL Extension Guide, 2024.
