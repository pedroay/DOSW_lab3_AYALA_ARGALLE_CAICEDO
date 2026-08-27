# 📄 Requerimientos del Sistema

## 1. Lista general de requerimientos

El sistema de TECHCUP tiene los siguientes requerimientos (descripción a alto nivel):

### 1.1 Requerimientos funcionales

El sistema de TECHCUP debe tener la capacidad de:

1.Los organizadores deben poder crear,actualizar y cambiar el estado de un torneo.
2.Los capitanades deben poder registrar un equipo.
3.Consultar los equipos de un toreno.
4.Los captianes deben poder pagar incripción torneo.
5.mandar reporte en formato json a la decanatura.
6.ingreso mediante nombre de usuario y contraseña tanto para los organizadores de TechCup como para los estudiantes.
7.Los organizadores del torneo deben poder consultar y verificar el pago asociado a la inscripción de cualquier equipo.
8.Los organizadores del torneo deben poder generar un informe que contenga la lista de todos los equipos registrados en un torneo.
9.Los organizadores del torneo deben poder generar un informe con los ingresos totales obtenidos a partir de las cuotas de inscripción.
10.Capacidad para eliminar un torneo en su totalidad, incluyendo todos los equipos que se hayan registrado en él.

### 1.2 Requerimientos no funcionales

El sistema de TECHCUP debe tener:

1.Los colores de la Universidad
2.El logo debe ser el siguiente
![Logo torneo](../images/TechCup_Logo.png)
3.El tipo fuente de la letra debe ser la que usa
4.El boton para acceder a la aplicación del torneo debe ser el logo
5.Debe tener un modo oscuro

## 2. Diagramas de caso de uso

### 2.1 Requerimiento Funcional 1

| Campo | Descripción |
|------|-------------|
| **ID** | RF-01 |
| **Nombre del requerimiento** | Gestión del Torneo |
| **Descripción** | El sistema debe permitir a los organizadores crear, actualizar, leer y cambiar el estado de un torneo, así como gestionar los equipos inscritos en él. Cada torneo posee un ID único de 5 dígitos basado en el año y semestre (ej. `20262`) y puede transicionar entre los estados *Pending, Active, In Progress, Closed, Cancelled*. Solo puede existir un torneo activo a la vez. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, TechCup debe tener previamente un organizador autenticado con credenciales válidas (nombre de usuario y contraseña) y con los permisos de administración correspondientes. |
| **Actor** | Organizador (Organizer) |
| **Flujo principal** | 1. El organizador inicia sesión en el sistema con sus credenciales.<br>2. El organizador selecciona la opción de gestionar torneos.<br>3. El sistema muestra las opciones de crear, actualizar, consultar o cambiar el estado de un torneo.<br>4. El organizador elige la acción deseada (crear, actualizar, leer o cambiar estado).<br>5. El sistema solicita los datos necesarios según la acción (fechas, tarifas, estado, etc.).<br>6. El organizador ingresa o confirma la información requerida.<br>7. El sistema valida los datos (por ejemplo, que no exista otro torneo activo si se desea activar uno nuevo).<br>8. El sistema ejecuta la acción y actualiza el estado del torneo en la base de datos.<br>9. El sistema muestra una confirmación de la operación realizada. |
| **Diagrama de caso de uso** | ![Diagrama de caso de uso - Gestión del Torneo](../uml/CaseOfUse_GestionTorneo.png) |
| **Poscondiciones** | Se espera como resultado que el torneo haya sido creado, actualizado o que su estado haya cambiado exitosamente en el sistema, reflejando la información actualizada para todos los usuarios. |


### 2.2 Requerimiento Funcional 2

| Campo | Descripción |
|------|-------------|
| **ID** | RF-02 |
| **Nombre del requerimiento** | Registrar Equipo |
| **Descripción** | El sistema debe permitir a los capitanes registrar un equipo en el torneo que se encuentre activo, ingresando la información del equipo y de sus integrantes para poder participar en el torneo junto a sus compañeros. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, TechCup debe tener previamente un capitán autenticado con credenciales válidas (nombre de usuario y contraseña) y debe existir un torneo en estado *Active* en el cual inscribir al equipo. |
| **Actor** | Capitán (Captain) |
| **Flujo principal** | 1. El capitán inicia sesión en el sistema con sus credenciales.<br>2. El capitán selecciona la opción de registrar equipo.<br>3. El sistema verifica que exista un torneo en estado *Active*.<br>4. El sistema muestra el formulario de registro de equipo.<br>5. El capitán ingresa los datos del equipo (nombre, integrantes/compañeros).<br>6. El sistema valida la información ingresada.<br>7. El sistema registra el equipo y lo asocia al torneo activo.<br>8. El sistema muestra una confirmación del registro exitoso del equipo. |
| **Diagrama de caso de uso** | ![Diagrama de caso de uso - Registrar Equipo](../uml/CaseOfUse_RegistrarEquipo.png) |
| **Poscondiciones** | Se espera como resultado que el equipo quede registrado e inscrito exitosamente en el torneo activo, siendo visible para los organizadores y demás usuarios del sistema. |

### 2.3 Requerimiento Funcional 3

| Campo | Descripción |
|------|-------------|
| **ID** | RF-03 |
| **Nombre del requerimiento** | Pagar Inscripción del Torneo |
| **Descripción** | El sistema debe permitir a los capitanes realizar el pago de la inscripción de su equipo en el torneo a través de la pasarela de pagos PSE, para quedar registrados formalmente y poder participar en el torneo. |
| **Precondiciones** | Para que el sistema cumpla con este requerimiento, TechCup debe tener previamente un capitán autenticado con credenciales válidas, un equipo registrado en el torneo activo y la integración con el sistema externo PSE disponible para procesar la transacción. |
| **Actor** | Capitán (Captain) |
| **Flujo principal** | 1. El capitán inicia sesión en el sistema con sus credenciales.<br>2. El capitán selecciona la opción de pagar la inscripción del torneo.<br>3. El sistema muestra los detalles del pago (tarifa de inscripción, equipo asociado, torneo).<br>4. El capitán confirma el pago.<br>5. El sistema redirige al capitán a la pasarela de pagos PSE.<br>6. El capitán completa la transacción en PSE.<br>7. PSE notifica al sistema el resultado de la transacción (aprobada/rechazada).<br>8. El sistema actualiza el estado de pago del equipo.<br>9. El sistema muestra una confirmación del pago realizado al capitán. |
| **Diagrama de caso de uso** | ![Diagrama de caso de uso - Pagar Inscripción](../uml/CaseOfUse_PagarTorneo.png) |
| **Poscondiciones** | Se espera como resultado que el pago de la inscripción quede registrado exitosamente en el sistema, el equipo quede formalmente inscrito en el torneo y el comprobante de pago esté disponible para consulta y validación por parte de los organizadores. |

## 3. Preguntas