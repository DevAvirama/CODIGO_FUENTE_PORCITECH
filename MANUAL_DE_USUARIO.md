# 📖 MANUAL DE USUARIO
## Plataforma Integral de Gestión Zootécnica, Visión Artificial y Trazabilidad (PorciTech 4.0)

---

### Ficha Metodológica de Documentación (ISO/IEC/IEEE 26514)
* **Programa de Formación:** Tecnólogo en Análisis y Desarrollo de Software (ADSO) — Código 228118
* **Ficha de Caracterización:** 3176243
* **Centro de Formación:** Centro de Teleinformática y Producción Industrial (CTPI) — Regional Cauca
* **Servicio Nacional de Aprendizaje (SENA)**
* **Unidad Productiva Beneficiaria:** Unidad Porcícola del Centro Agropecuario SENA — Granja La Rejoya
* **Alineación Normativa:** **ISO/IEC/IEEE 26514:2022** (*Systems and software engineering — Requirements for designers and developers of user documentation*)
* **Metodología de Gestión Documental:** Docs-as-Code (Markdown versionado en Git)

---

### Matriz de Control de Versiones del Manual (ISO 26514)

| Versión Manual | Versión App | Fecha | Naturaleza de la Actualización | Redactor Técnico | Aprobó |
| :---: | :---: | :---: | :--- | :--- | :--- |
| **v1.0.0** | v1.0.0 | 28/05/2025 | Publicación inicial: Módulos de Login, Catálogo de Cerdos y Aretes QR. | Santiago Avirama | Pablo A. Ortiz (PO) |
| **v2.0.0** | v2.0.0 | 20/07/2025 | Incorporación de la App Móvil: Teclado para guantes y cola Offline-First. | Mariana Guapacha | Pablo A. Ortiz (PO) |
| **v3.0.0** | v3.0.0 | 15/09/2025 | Guía de pesaje cenital por Visión Artificial y Monitor CCTV Dahua. | Juan David Ocampo| Pablo A. Ortiz (PO) |
| **v4.0.0** | v4.0.0 | 09/11/2026 | Consolidación PorciTech 4.0: Pasaporte QR ICA, Kardex y analítica GMD. | Santiago Avirama | Pablo A. Ortiz (PO) |

---

## ÍNDICE DEL MANUAL DE USUARIO
1. [Introducción y Requisitos del Sistema](#1-introducción-y-requisitos-del-sistema)
2. [Módulo I: Operación Móvil de Campo (App Flutter para Operarios)](#2-módulo-i-operación-móvil-de-campo)
3. [Módulo II: Portal Web Administrativo (Next.js para Administradores y Veterinarios)](#3-módulo-ii-portal-web-administrativo)
4. [Módulo III: Pasaporte Sanitario y Trazabilidad Pública (`/trace/[id]`)](#4-módulo-iii-pasaporte-sanitario)
5. [Módulo IV: Preguntas Frecuentes y Solución de Problemas (FAQ)](#5-módulo-iv-faq)

---

<a name="1-introducción-y-requisitos-del-sistema"></a>
# 1. Introducción y Requisitos del Sistema

### 1.1 ¿Qué es PorciTech 4.0?
**PorciTech 4.0** es un ecosistema tecnológico diseñado para tecnificar la producción porcícola en Colombia. Elimina el estrés del pesaje mecánico mediante **Visión Artificial con Inteligencia Artificial (YOLOv8)**, asegura la inocuidad alimentaria controlando los **tiempos de retiro de medicamentos exigidos por el ICA**, optimiza el 75% del costo de producción (el alimento concentrado) a través de un **Kardex automatizado** y permite a los operarios trabajar en los galpones **sin conexión a internet** gracias a su arquitectura **Offline-First**.

---

### 1.2 Requisitos para Usuarios Finales

| Entorno de Uso | Dispositivo Recomendado | Conectividad | Requisitos de Software |
| :--- | :--- | :--- | :--- |
| **App Móvil de Campo** | Teléfono o tablet Android (versión 8.0 o superior) o iPhone (iOS 13+). | **Funciona 100% Desconectado** en los corrales. Requiere Wi-Fi solo para sincronizar. | Cámara trasera de al menos 12 MP para escaneo de QR y fotos cenitales. |
| **Portal Web Administrativo** | Computador de escritorio o portátil. | Red local de la granja (LAN) o internet. | Navegador moderno (Google Chrome, Microsoft Edge, Mozilla Firefox o Brave). |
| **Pasaporte Sanitario QR** | Cualquier smartphone con lector de QR o cámara nativa. | Conexión a red móvil (3G/4G) o Wi-Fi. | Cualquier navegador web (no requiere instalar ninguna app ni iniciar sesión). |

---

### 1.3 Credenciales de Acceso Demostrativas (Roles del Sistema)

Para iniciar sesión en las pruebas de campo o demostraciones oficiales, utilice una de las siguientes cuentas pre-configuradas según el perfil que desee evaluar:

| Rol | Correo Electrónico | Contraseña | Permisos Principales |
| :--- | :--- | :---: | :--- |
| **Administrador** | `admin@sigep.com` | `admin123` | Control total, gestión de usuarios, auditoría, Kardex y configuración. |
| **Médico Veterinario** | `vet@sigep.com` | `vet123` | Prescripción sanitaria, semáforo de carencia ICA y control reproductivo. |
| **Operario de Galpón** | `operario@sigep.com` | `operario123` | Pesajes diarios, escaneo de aretes QR, raciones de comida y partos. |

---

<a name="2-módulo-i-operación-móvil-de-campo"></a>
# 📱 2. Módulo I: Operación Móvil de Campo (App Flutter)

Este módulo está especialmente adaptado a las condiciones de humedad, polvo y manipulación con **guantes de bioseguridad** en los galpones.

---

### 2.1 Inicio de Sesión y Reconocimiento de Conectividad

#### Procedimiento para Iniciar Sesión:
1. Abra la aplicación **PorciTech Móvil** en su dispositivo.
2. Ingrese su **Correo Electrónico** y **Contraseña**.
3. Presione el botón verde **Ingresar al Sistema**.
4. La aplicación guardará su sesión de forma segura y cifrada en el dispositivo para que no tenga que volver a digitar sus datos cada vez que ingrese al galpón.

![Pantalla de Inicio de Sesión Móvil](docs/assets/screenshots/movil_01_login.png)

```text
+-------------------------------------------------------+
|  🐷 PORCITECH 4.0 - GESTIÓN DE CAMPO                  |
+-------------------------------------------------------+
|  [1] Correo:     [ operario@sigep.com               ] |
|  [2] Contraseña: [ •••••••••••                      ] |
|                                                       |
|        +-------------------------------------+        |
|        | [3] BOTÓN: INGRESAR AL SISTEMA      |        |
|        +-------------------------------------+        |
+-------------------------------------------------------+
```
* **[1] Campo Correo:** Digite su usuario asignado.
* **[2] Campo Contraseña:** Digite su clave de acceso.
* **[3] Botón 'Ingresar al Sistema':** Valida credenciales y almacena el token seguro.

---

### 2.2 Dashboard de Campo y Estado de Conexión

Al ingresar, visualizará la pantalla principal de mando:

![Dashboard Móvil de Campo](docs/assets/screenshots/movil_02_dashboard.png)

```text
+-------------------------------------------------------+
|  PORCITECH CAMPO               [1] CHIP: [ ONLINE 🟢 ]|
+-------------------------------------------------------+
|  [2] TARJETA: Corrales Activos: 6  | Total Cerdos: 48 |
+-------------------------------------------------------+
|  ACCIONES RÁPIDAS EN GALPÓN:                          |
|  +------------------------+  +----------------------+ |
|  | [3] 📷 ESCANEAR QR     |  | [4] ⚖️ PESAR CON IA  | |
|  +------------------------+  +----------------------+ |
|  | [5] 💉 REGISTRAR VACUNA|  | [6] 🐷 NUEVO PARTO   | |
|  +------------------------+  +----------------------+ |
|                                                       |
|  [7] BOTÓN INFERIOR: [ IR A COLA DE SINCRONIZACIÓN ]  |
+-------------------------------------------------------+
```
* **[1] Chip de Conectividad:** 
  * `ONLINE 🟢`: El dispositivo tiene enlace con el servidor de la granja.
  * `OFFLINE 🔴`: Sin señal. Los datos que registre se guardarán automáticamente en la memoria del teléfono.
* **[2] Resumen del Galpón:** Total de animales y lotes a su cargo.
* **[3-6] Botones Táctiles Gigantes:** Accesos directos ergonómicos diseñados para pulsarse con guantes de caucho.
* **[7] Barra de Sincronización:** Muestra cuántas tareas están pendientes de subida.

---

### 2.3 Escaneo de Arete QR y Consulta Rápida en Corral

#### Procedimiento:
1. En el Dashboard de Campo, presione **Escanear QR**.
2. Se activará la cámara con una mira láser verde animada.
3. Apunte el visor al código QR impreso en el arete plástico del porcino a una distancia de entre 20 cm y 40 cm.
4. Al detectarlo, el teléfono vibrará y desplegará automáticamente la ficha rápida del cerdo desde la parte inferior:

![Ficha Rápida tras Escanear QR](docs/assets/screenshots/movil_03_escaneo_qr.png)

```text
+-------------------------------------------------------+
|              VISOR LÁSER ACTIVO [|||||]               |
+-------------------------------------------------------+
|  ================= FICHA DEL PORCINO ================ |
|  Arete: #4092-CEBA            Corral: LOTE-15 (Ceba)  |
|  Raza:  Pietrain x Landrace   Peso Actual: 58.5 kg    |
|                                                       |
|  [!] ESTADO SANITARIO:                                |
|  [ 🟢 APTO - SIN RESTRICCIÓN DE MEDICAMENTOS ]        |
|                                                       |
|  ACCIONES RÁPIDAS:                                    |
|  [ PESAR ESTE CERDO ]   [ APLICAR TRATAMIENTO ]       |
+-------------------------------------------------------+
```

> [!CAUTION]
> **ALERTA DE RETIRO SANITARIO (Semáforo Rojo):**
> Si el porcino escaneado tiene un tratamiento antibiótico activo, aparecerá una franja roja parpadeante:
> `🔴 EN PERIODO DE CARENCIA: Faltan 14 días (Tilmicosina) - PROHIBIDO DESTINAR A SACRIFICIO`.

---

### 2.4 Estimación de Peso por Visión Artificial (Cámara Cenital)

Reemplaza la báscula mecánica tradicional. Permite estimar el peso en milisegundos mediante una fotografía cenital (tomada desde arriba del corral).

#### Reglas para una Captura Exitosa:
1. Ubíquese por encima del cerdo (a una altura aproximada de 2.0 a 2.4 metros del suelo).
2. Asegúrese de que el lomo del animal esté visible y que no quede cortado por los barrotes del corral.
3. Presione el botón **Capturar Foto Cenital**.

![Captura Cenital de Visión Artificial](docs/assets/screenshots/movil_04_captura_ia.png)

```text
+-------------------------------------------------------+
|  GUÍA DE ENCUADRE CENITAL (LOMO COMPLETO)             |
|                                                       |
|          +-------------------------------+            |
|          |     [ SILUETA DORSAL DEL      |            |
|          |         PORCINO AQUÍ ]        |            |
|          +-------------------------------+            |
|                                                       |
|  [1] Lente: Gran Angular 1x      [2] Calidad: 1280px  |
|                                                       |
|       +-------------------------------------+         |
|       | [3] BOTÓN: ESTIMAR PESO CON IA      |         |
|       +-------------------------------------+         |
+-------------------------------------------------------+
```
* **[1] Encuadre Cenital:** La app ajusta automáticamente la perspectiva.
* **[2] Preprocesamiento en el Celular:** La foto se redimensiona automáticamente a 1280px para que suba en milisegundos sin consumir memoria ni saturar la red.
* **[3] Botón de Inferencia:** Envía la foto al modelo YOLOv8n-seg y muestra el resultado en pantalla:

```text
+-------------------------------------------------------+
|  RESULTADO DE ESTIMACIÓN MORFOMÉTRICA                 |
|  Peso Calculado: 62.4 kg                              |
|  Área Dorsal:    1,905.0 cm²                          |
|  Confianza IA:   98.0%                                |
|                                                       |
|  [ CONFIRMAR Y GUARDAR EN FICHA ]   [ REPETIR FOTO ]  |
+-------------------------------------------------------+
```

---

### 2.5 Registro de Pesaje Manual (Teclado Gigante para Guantes)

Si se utiliza una báscula mecánica o báscula digital de plataforma de respaldo, el operario cuenta con un teclado numérico táctil de **64 píxeles de altura**:

![Teclado Gigante para Guantes](docs/assets/screenshots/movil_05_teclado_guantes.png)

```text
+-------------------------------------------------------+
|  REGISTRO DE PESAJE MANUAL - ARETE #4092              |
|                                                       |
|  PESO EN BÁSCULA: [   58.50  ] KG                     |
|                                                       |
|  +-------+-------+-------+                            |
|  |   1   |   2   |   3   |  <- Teclas de 64px de alto |
|  +-------+-------+-------+     con vibración háptica  |
|  |   4   |   5   |   6   |                            |
|  +-------+-------+-------+                            |
|  |   7   |   8   |   9   |                            |
|  +-------+-------+-------+                            |
|  |   .   |   0   |  BORR |                            |
|  +-------+-------+-------+                            |
|                                                       |
|        +-------------------------------------+        |
|        | BOTÓN: GUARDAR PESAJE               |        |
|        +-------------------------------------+        |
+-------------------------------------------------------+
```
* Cada toque emite una vibración ligera (`HapticFeedback`) para que el operario sepa que la tecla fue presionada sin necesidad de quitarse los guantes.

---

### 2.6 Registro de Parto y Conteo de Camadas (Cerdas Reproductoras)

Exclusivo para la sala de maternidad cuando una hembra da a luz:

#### Procedimiento:
1. Escanee el arete de la madre o búsquela en el módulo de maternidad.
2. Utilice los botones incrementales `+` y `-` para totalizar la camada:

![Registro de Parto Móvil](docs/assets/screenshots/movil_06_parto.png)

```text
+-------------------------------------------------------+
|  REGISTRO DE PARTO - CERDA #H-104 (SALA MATERNIDAD)   |
+-------------------------------------------------------+
|  Nacidos Vivos:   [ - ]  [ 13 ]  [ + ]  (Meta: >= 12) |
|  Nacidos Muertos: [ - ]  [  1 ]  [ + ]                |
|  Momias:          [ - ]  [  0 ]  [ + ]                |
+-------------------------------------------------------+
|  Peso Total Camada (kg): [  19.50 ]                   |
|  Promedio por Lechón:     1.50 kg  (Desarrollo Óptimo)|
+-------------------------------------------------------+
|           +-------------------------------+           |
|           | BOTÓN: FINALIZAR Y GUARDAR    |           |
|           +-------------------------------+           |
+-------------------------------------------------------+
```

> [!NOTE]
> Al confirmar el parto, el sistema **cambia automáticamente el estado de la cerda a 'Lactante'** y actualiza el corral al pabellón de maternidad.

---

### 2.7 Modo Desconectado y Cola de Sincronización (Offline-First)

Cuando trabaje en galpones rurales profundos donde se pierde la señal Wi-Fi:

1. La app seguirá funcionando con total normalidad.
2. Al guardar un pesaje, parto o tratamiento sin señal, verá el mensaje:  
   `📦 Guardado localmente en Cola Offline`.
3. Al finalizar la jornada y volver al área administrativa con Wi-Fi, abra **Ajustes > Cola de Sincronización**:

![Gestor de Sincronización Offline](docs/assets/screenshots/movil_07_sync.png)

```text
+-------------------------------------------------------+
|  COLA DE SINCRONIZACIÓN LOCAL      [ ENLACE ACTIVO 🟢]|
+-------------------------------------------------------+
|  Registros pendientes por subir al servidor:          |
|                                                       |
|  [x] Pesaje Manual Cerdo #4092 (58.5 kg) - 10:14 AM   |
|  [x] Tratamiento Oxitetraciclina L.A.    - 10:28 AM   |
|  [x] Parto Cerda #H-104 (13 Vivos)       - 11:05 AM   |
|                                                       |
|        +-------------------------------------+        |
|        | BOTÓN: SINCRONIZAR TODO AHORA       |        |
|        +-------------------------------------+        |
+-------------------------------------------------------+
```
4. Presione **Sincronizar Todo Ahora**. La app enviará cada registro de forma segura sin duplicar identificadores gracias a sus claves universales UUID v4.

---

<a name="3-módulo-ii-portal-web-administrativo"></a>
# 💻 3. Módulo II: Portal Web Administrativo (Next.js 16)

Acceso desde cualquier navegador web en su computador apuntando a:  
👉 `http://localhost:3000` (o la IP local del servidor: `http://192.168.x.x:3000`).

---

### 3.1 Resumen Ejecutivo (Dashboard Central)

El panel gerencial ofrece una vista panorámica de la granja en tiempo real:

![Dashboard Web Administrativo](docs/assets/screenshots/web_01_dashboard.png)

```text
+-----------------------------------------------------------------------------------+
| PORCITECH 4.0 | [🔍 Búsqueda Rápida Arete/QR]                [ Admin: Julian B. ] |
+-----------------------------------------------------------------------------------+
|  [1] TARJETAS KPI:                                                                |
|  +----------------+  +----------------+  +----------------+  +-----------------+  |
|  | TOTAL CABEZAS  |  | CORRALES OCUP. |  | PARTOS PRÓXIMOS|  | RETIROS ACTIVOS |  |
|  |     48         |  |   6 / 10       |  |  2 (<= 7 días) |  |   2 Animales    |  |
|  +----------------+  +----------------+  +----------------+  +-----------------+  |
+-----------------------------------------------------------------------------------+
|  [2] GRÁFICA ANALÍTICA GMD (TIMESCALEDB):           | [3] ALERTAS CRÍTICAS:       |
|  Ganancia Media Diaria vs Meta Porkcolombia         | 🔴 Cerda #18: Retiro activo |
|  850 g/día [========================]               | 🟡 Cerda #04: Parto en 4 d  |
|  (Calculado automáticamente con función SQL LAG)    | 🟡 Alimento Ceba: Stock < 5 |
+-----------------------------------------------------------------------------------+
```
* **[1] KPIs en Tiempo Real:** Población total, porcentaje de ocupación de galpones y alertas sanitarias.
* **[2] Curvas de Crecimiento GMD:** Calculadas directamente desde TimescaleDB comparando el peso actual de cada corral contra su pesaje anterior.
* **[3] Panel de Alertas:** Notificaciones urgentes de partos próximos y tiempos de retiro.

---

### 3.2 Hoja de Vida Porcina e Impresión de Etiquetas QR

En el menú lateral **Población > Listado de Animales**:

1. Seleccione cualquier porcino para ver su expediente completo:
   * Filiación genética (Padre y Madre).
   * Historial de pesajes con gráfica de crecimiento.
   * Tratamientos médicos recibidos.
2. Presione el botón **Generar Etiqueta QR Imprimible**:
   * Descargará una plantilla en PDF lista para imprimir en hojas adhesivas resistentes al agua para pegar en el arete visual del animal.

---

### 3.3 Pesaje en Vivo con Cámara Industrial Dahua (Monitor CCTV)

En el menú lateral **Pesaje e IA > Monitor en Vivo**:

![Monitor CCTV en Vivo](docs/assets/screenshots/web_02_cctv.png)

```text
+-----------------------------------------------------------------------------------+
|  MONITOR CENITAL EN VIVO - CÁMARA INDUSTRIAL DAHUA TPC-BF                         |
+----------------------------------------------------+------------------------------+
|  [1] TRANSMISIÓN MJPEG (0-LAG / 20 FPS):           | [2] MÉTRICAS EN VIVO:        |
|                                                    | Confianza YOLO:  97.4%       |
|          +-------------------------------+         | Área Estimada:   1,777 cm²   |
|          |    [ VIDEO DEL CORRAL EN VIVO |         | Peso Proyectado: 58.0 kg     |
|          |    CON CAJA Y MÁSCARA VERDE]  |         +------------------------------+
|          +-------------------------------+         | [3] SELECCIONAR CERDO:       |
|                                                    | Arete: [ #4092-CEBA        ] |
|  CANAL: [ Canal 1: Óptico ] [ Canal 2: Térmico ]   |                              |
|                                                    | +--------------------------+ |
|                                                    | | [4] CAPTURAR Y GUARDAR   | |
|                                                    | +--------------------------+ |
+----------------------------------------------------+------------------------------+
```
* **[1] Video en Vivo:** Transmisión continua sin retraso (0-lag) gestionada por hilos demonio en el servidor.
* **[2] Métricas en Tiempo Real:** Muestra el peso proyectado mientras el cerdo camina por el corral.
* **[3] Selector de Arete:** Permite asignar la lectura al cerdo correspondiente.
* **[4] Botón 'Capturar y Guardar':** Congela el fotograma exacto y almacena el peso en la Hipertabla de TimescaleDB.

---

### 3.4 Control de Bodega y Kardex Contable (Conversión Automática)

En el menú lateral **Inventario > Bodega y Kardex**:

* **¿Cómo maneja PorciTech los bultos y los kilogramos?**
  * La bodega compra en **Bultos de 40 kg** (`factor_conversion_kg = 40.0`).
  * El operario sirve raciones en **Kilogramos** en el corral (ej. 20 kg).
  * El sistema divide `20 / 40 = 0.50 bultos` y descuenta automáticamente medio bulto del stock general, registrando la salida en el Kardex contable inmutable sin descuadre contable.

---

### 3.5 Flujo Reproductivo (Ley de los 114 Días)

En el menú lateral **Reproducción**:

1. **Registrar Servicio de Monta:**
   * Ingrese la fecha del servicio y seleccione la cerda y el macho.
   * **Automatización:** El motor de base de datos calculará y fijará la fecha probable de parto sumando exactamente **114 días** (3 meses, 3 semanas y 3 días).
2. **Alertas de Gestación:**
   * Cuando falten 7 días o menos para los 114 días, la cerda aparecerá resaltada en amarillo en el Dashboard con la indicación: *"Trasladar a Sala de Maternidad"*.

---

<a name="4-módulo-iii-pasaporte-sanitario"></a>
# 🛡️ 4. Módulo III: Pasaporte Sanitario y Trazabilidad Pública (`/trace/[id]`)

Diseñado para cumplir con las exigencias de inocuidad alimentaria del **ICA e INVIMA** en plantas de beneficio (frigoríficos) o puntos de venta.

---

### 4.1 ¿Cómo Funciona la Consulta Pública?
Cualquier persona (inspector sanitario, comprador o consumidor final) puede escanear el código QR del arete del porcino con la cámara de su teléfono celular común.

* **No requiere iniciar sesión.**
* **No requiere descargar ninguna aplicación.**
* El sistema abre la página oficial de verificación: `http://servidor:3000/trace/<codigo_qr>`.

---

### 4.2 Los Dos Posibles Resultados Oficiales

#### Caso A: Animal Apto (Certificado Verde)
Si el cerdo nunca ha recibido fármacos de retiro o si ya se cumplieron todos los días de carencia reglamentarios:

```text
+-------------------------------------------------------+
|  🐷 PORCITECH - CERTIFICADO OFICIAL DE INOCUIDAD ICA  |
+-------------------------------------------------------+
|  ESTADO DE TRAZABILIDAD SANITARIA:                    |
|                                                       |
|  ===================================================  |
|  🟢 APTO PARA COMERCIALIZACIÓN Y CONSUMO HUMANO       |
|  ===================================================  |
|                                                       |
|  Arete Identificador:  #4092-CEBA                     |
|  Granja de Origen:     Centro Agropecuario La Rejoya  |
|  Registro Sanitario:   ICA-BPP-2026-CAUCA             |
|  Tratamientos Activos: Ninguno (0 días de retiro)     |
|                                                       |
|  [✓] Carnes libres de trazas y residuos antibióticos  |
+-------------------------------------------------------+
```

---

#### Caso B: Animal Bloqueado por Periodo de Carencia (Alerta Roja)
Si el animal recibió un antibiótico recientemente y aún tiene días de retiro vigentes:

```text
+-------------------------------------------------------+
|  🐷 PORCITECH - CERTIFICADO OFICIAL DE INOCUIDAD ICA  |
+-------------------------------------------------------+
|  ESTADO DE TRAZABILIDAD SANITARIA:                    |
|                                                       |
|  ===================================================  |
|  🔴 PERIODO DE CARENCIA ACTIVO — NO APTO PARA SACRIFICIO|
|  ===================================================  |
|                                                       |
|  Arete Identificador:  #18-CUARENTENA                 |
|  Medicamento Aplicado: Tilmicosina 300 mg             |
|  Lote Biológico ICA:   LOTE-ICA-TILM-902              |
|  Fecha de Aplicación:  01/11/2026                     |
|  Tiempo de Retiro:     14 Días Obligatorios           |
|  Días Faltantes:       6 DÍAS RESTANTES               |
|  Apto para Beneficio:  15/11/2026                     |
|                                                       |
|  [!] INFRACCIÓN: El sacrificio de este animal genera  |
|      decomiso inmediato y sanción según Res. ICA      |
+-------------------------------------------------------+
```

---

<a name="5-módulo-iv-faq"></a>
# ❓ 5. Módulo IV: Preguntas Frecuentes y Solución de Problemas (FAQ)

### P1: "¿Qué debo hacer si la app móvil muestra el chip en color ROJO (Offline)?"
* **Respuesta:** No se preocupe. Puede seguir trabajando, registrando pesajes manuales, vacunas y partos. Todos sus registros se guardarán de forma segura en la memoria del teléfono. Al finalizar sus tareas en el galpón y acercarse a la oficina con Wi-Fi, entre a **Ajustes > Cola de Sincronización** y presione **Sincronizar Todo Ahora**.

---

### P2: "¿Por qué el sistema no me deja ingresar un cerdo a un corral?"
* **Respuesta:** Cada corral tiene configurada una **Capacidad Máxima**. Si el corral está lleno, el sistema bloquea el ingreso con el mensaje: *"El corral ha alcanzado su capacidad máxima permitida"*. Traslade primero otro porcino a otra fase o seleccione un corral con cupos libres.

---

### P3: "¿Por qué la foto cenital de la cámara IA arrojó un porcentaje de confianza bajo?"
* **Respuesta:** Esto ocurre cuando:
  1. El cerdo estaba acostado o tapado por otro animal.
  2. La foto se tomó demasiado cerca cortando la cabeza o la cola.
  3. Había poca iluminación en el galpón.  
  *Solución:* Asegúrese de que el lomo del animal esté despejado, mantenga una altura de ~2.20 metros y repita la captura con el botón **Repetir Foto**.

---

### P4: "¿Quién puede recetar medicamentos y asignar días de retiro?"
* **Respuesta:** Por normativa sanitaria del ICA y seguridad del sistema, solo los usuarios con rol de **Médico Veterinario** o **Administrador** pueden registrar tratamientos con tiempos de carencia. Los operarios solo pueden consultar el estado sanitario.

---

<a name="6-matriz-de-control-de-versiones"></a>
# 📋 6. Matriz de Aprobación Documental (SENA ADSO)

Este manual de usuario forma parte integral del repositorio de software de PorciTech 4.0 bajo la modalidad **Docs-as-Code**:

* **Ubicación en Repositorio:** [`MANUAL_DE_USUARIO.md`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/MANUAL_DE_USUARIO.md)
* **Directorio de Activos:** [`docs/assets/screenshots/`](file:///home/santiago/Documentos/ADSO_SENA_3176243/CODIGO_FUENTE_PORCITECH/docs/assets/screenshots)
* **Alineación:** Estándar ISO/IEC/IEEE 26514:2022 y Competencias SENA 220501095, 220501097 y 220501098.
