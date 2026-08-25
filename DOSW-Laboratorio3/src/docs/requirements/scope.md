# Requerimientos del Sistema

## 1. Sistema

* **Nombre del sistema:** TechCup (TechCup Tournament)
* **Objetivo:** El sistema tiene como objetivo proveer una plataforma digital centralizada y segura para la administración y gestión integral de los torneos semestrales de fútbol de los programas de Ingeniería de Sistemas, Ingeniería de Inteligencia Artificial, Ingeniería en Ciberseguridad e Ingeniería Estadística en la Escuela Colombiana de Ingeniería Julio Garavito. Permite la creación y configuración de torneos, el registro y gestión de equipos participantes, el procesamiento y validación de pagos de inscripción vía PSE, y la generación y distribución de reportes de inscripciones e ingresos tanto para organizadores como para la Decanatura.

---

## 2. Problema a resolver

Actualmente, la Escuela Colombiana de Ingeniería Julio Garavito no dispone de un sistema centralizado y automatizado para la administración de sus torneos de fútbol, lo que genera dificultades en la organización, seguimiento y control financiero de los eventos deportivos.

Específicamente, el sistema busca solucionar las siguientes problemáticas:
* **Falta de centralización en la creación y parametrización de torneos:** Dificultad para definir de forma estandarizada las reglas básicas, fechas, tarifas, identificadores únicos semestrales y control de estados de los torneos.
* **Proceso manual y disperso en la inscripción de equipos:** Ausencia de un canal formal para que capitanes y estudiantes registren y actualicen la información de sus equipos en el torneo activo.
* **Falta de integración y validación ágil de pagos:** Inexistencia de un mecanismo digital para procesar el pago de inscripciones mediante PSE y validar oportunamente los comprobantes de pago de cada equipo.
* **Dificultad en la consolidación y consulta de información:** Complejidad para que estudiantes y organizadores visualicen los equipos inscritos y el avance de los torneos en tiempo real.
* **Generación y entrega manual de reportes:** Ineficiencia en la consolidación de ingresos recaudados y la necesidad de estructurar reportes de pagos en formato JSON para su entrega a la Decanatura.

---

## 3. Diagrama de Contexto

### 3.1 Diagrama

A continuación se presenta el Diagrama de Contexto (C4 Model - Nivel 1) del sistema TechCup Tournament:

![Diagrama de Contexto](../uml/Context%20Diagram%20C4.png)

### 3.2 Actores

| Actor / Rol | Descripción |
| :--- | :--- |
| **Estudiante (Student)** | Usuario final con cuenta en la plataforma que consulta información general sobre torneos, equipos y jugadores registrados. |
| **Organizador (Organizer)** | Usuario con privilegios de administración encargado de crear torneos, configurar sus reglas, cambiar sus estados, revisar y validar los pagos de inscripción de los equipos y generar reportes financieros y de participación. |
| **Capitán (Captain)** | Usuario del sistema que, además de consultar información, tiene la capacidad de crear y administrar su equipo, actualizar su alineación/datos y realizar el pago de inscripción para participar en el torneo activo. |
| **Decanatura (Dean)** | Interesado institucional que requiere y recibe la información consolidada, reportes de pagos e inscripciones de los torneos en formato JSON para efectos de supervisión y control académico/administrativo. |

### 3.3 Sistemas externos

| Sistema | Descripción |
| :--- | :--- |
| **PSE (Pagos Seguros en Línea)** | Plataforma externa de servicios financieros que procesa las transacciones de pago de las inscripciones de los equipos de forma segura y notifica el resultado de la transacción a TechCup. |
| **Outlook (Servicio de Correo Electrónico)** | Servicio de mensajería y correo en la nube utilizado para el envío automatizado de notificaciones, confirmaciones y reportes a los actores (Decanatura, Organizadores, Capitanes y Estudiantes). |

---

## 4. Alcance del sistema

### 4.1 Dentro del sistema

Funciones que el sistema **SÍ** realiza:
1. **Autenticación y control de acceso:** Gestión de credenciales (usuario y contraseña) diferenciando roles y permisos (Estudiante, Capitán, Organizador).
2. **Gestión integral de torneos:** Creación de torneos con ID único de 5 dígitos (basado en año y semestre, ej. `20262`), definición de fechas, tarifas y control del ciclo de vida a través de sus estados (*Pending, Active, In Progress, Closed, Cancelled*), asegurando que solo exista un torneo activo a la vez.
3. **Gestión y registro de equipos:** Creación y actualización de datos de equipos por parte de capitanes u organizadores, permitiendo la inscripción exclusiva en el torneo que se encuentre activo.
4. **Integración con PSE para pago de inscripciones:** Conexión con la pasarela de pagos PSE para procesar y recibir notificaciones del estado de pago de los equipos.
5. **Consulta y validación de pagos:** Módulo para que los organizadores verifiquen el estado de los pagos asociados a las inscripciones de los equipos.
6. **Generación de reportes:** Creación de reportes de equipos inscritos, reportes de ingresos por recaudos de inscripción y exportación de reportes en formato JSON dirigidos a la Decanatura.

### 4.2 Fuera del sistema

Funciones que el sistema **NO** realiza:
1. **Procesamiento financiero bancario propio:** El sistema no actúa como entidad bancaria ni almacena información de tarjetas de crédito o cuentas de ahorros; delega completamente el débito y procesamiento a la pasarela externa PSE.
2. **Eliminación definitiva (borrado) de torneos:** Conforme a las reglas de negocio, los torneos registrados no pueden ser eliminados de la base de datos (únicamente pueden transicionar a estados como *Cancelled* o *Closed*).
3. **Gestión concurrente de múltiples torneos activos:** El sistema restringe la ejecución a un único torneo activo a la vez; no permite la apertura simultánea de inscripciones para múltiples torneos paralelos.
4. **Arbitraje en vivo y transmisión multimedia de partidos:** El sistema no realiza seguimiento de jugadas en tiempo real ni streaming o transmisión de video de los encuentros deportivos.
5. **Servidor SMTP/correo propio:** El sistema no opera como servidor de correo independiente; delega la entrega y distribución de mensajes a la plataforma externa Outlook.
