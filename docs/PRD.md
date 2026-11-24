# PRD — gofundme-sys

**Nombre del producto:** gofundme-sys  
**Tipo de producto:** Aplicación web de gestión de campañas de recaudación de fondos  
**Estado del documento:** Borrador inicial — Sprint 0  
**Versión:** 0.1  

## 1. Resumen del producto

gofundme-sys será una aplicación web que permitirá publicar y administrar campañas de recaudación de fondos, consultar iniciativas disponibles y registrar donaciones asociadas a cada campaña. También ofrecerá herramientas para que los creadores hagan seguimiento de sus campañas y para que los administradores supervisen usuarios y contenido.

El producto toma como referencia el funcionamiento general de las plataformas de crowdfunding, pero tendrá identidad, diseño e implementación propios. Su primera versión se centrará en los flujos esenciales y en demostrar el funcionamiento integrado de la aplicación y su base de datos.

## 2. Problema y oportunidad

Las personas que necesitan apoyo económico para una causa, proyecto o situación pueden tener dificultades para presentar su iniciativa, compartir información clara y llevar un control centralizado de los aportes recibidos. Del lado de los posibles donantes, puede resultar difícil encontrar la información de una campaña y entender cuánto ha recaudado.

El sistema busca reunir estas actividades en un solo espacio: publicación de campañas, consulta de información, registro de aportes y seguimiento de resultados. La plataforma también necesita herramientas administrativas para mantener organizada la información y atender posibles inconvenientes.

## 3. Objetivos del producto

- Permitir que una persona cree una cuenta y acceda de forma segura.
- Facilitar la creación y administración de campañas.
- Mostrar información comprensible sobre cada campaña y su progreso.
- Asociar los aportes registrados con la campaña correspondiente.
- Permitir que los creadores consulten el progreso de sus campañas.
- Proporcionar a los administradores herramientas básicas de supervisión.
- Mantener los datos consistentes entre la aplicación y PostgreSQL.

## 4. Usuarios objetivo y necesidades

### 4.1 Creador de campañas

Persona u organización que desea presentar una causa o iniciativa y solicitar apoyo.

**Necesidades:** registrarse, publicar una campaña, explicar su objetivo, establecer una meta, consultar el monto recaudado y revisar los aportes asociados.

### 4.2 Donante

Persona que desea conocer campañas y contribuir con una iniciativa.

**Necesidades:** explorar campañas, leer sus detalles, conocer su progreso y registrar un aporte mediante un flujo claro y confiable.

### 4.3 Administrador

Persona autorizada para supervisar el uso de la plataforma.

**Necesidades:** consultar usuarios y campañas, revisar contenido, cambiar estados cuando corresponda y dar seguimiento a la actividad.

## 5. Alcance

### 5.1 Alcance previsto para el MVP

- Registro, inicio y cierre de sesión.
- Gestión básica del perfil.
- Listado y consulta de campañas.
- Creación y edición de campañas por parte de su creador.
- Definición de una meta y visualización del progreso.
- Registro de donaciones o aportes vinculados a una campaña.
- Historial o resumen de aportes por campaña y para el creador.
- Panel administrativo básico para consultar y moderar campañas y usuarios.
- Persistencia de la información en PostgreSQL.

### 5.2 Fuera del alcance inicial

- Aplicación móvil nativa.
- Conversión de divisas y pagos internacionales.
- Suscripciones o donaciones recurrentes.
- Recomendaciones personalizadas mediante inteligencia artificial.
- Verificación automatizada de identidad o de organizaciones.
- Integración con múltiples proveedores de pago.
- Funciones avanzadas de impuestos, recibos fiscales o desembolsos bancarios.

**Nota sobre pagos:** el alcance inicial debe aclarar si las donaciones serán registros de prueba o transacciones reales. Hasta que se seleccione y configure un proveedor de pagos y se definan los controles necesarios, el desarrollo debe utilizar datos simulados o un entorno de pruebas. La aplicación no debe almacenar datos completos de tarjetas ni presentar un aporte como pago real confirmado sin una confirmación válida del flujo de pago.

## 6. Requisitos funcionales

| ID | Requisito | Criterio de aceptación inicial |
|---|---|---|
| RF-01 | Registro de usuarios | Una persona puede crear una cuenta con los campos requeridos y recibe un resultado claro si los datos no son válidos. |
| RF-02 | Inicio y cierre de sesión | Un usuario registrado puede iniciar sesión y cerrar su sesión. |
| RF-03 | Control de roles | El sistema distingue como mínimo entre creador/donante y administrador, y protege las operaciones según el rol. |
| RF-04 | Gestión del perfil | El usuario puede consultar y actualizar los datos de perfil permitidos. |
| RF-05 | Crear campaña | Un usuario autorizado puede crear una campaña con título, descripción, meta y los demás campos definidos por el sistema. |
| RF-06 | Editar campaña | El creador puede modificar sus propias campañas conforme a las reglas de estado; no puede modificar campañas de otras personas. |
| RF-07 | Consultar campañas | Los visitantes o usuarios pueden ver el listado de campañas publicadas y abrir su detalle. |
| RF-08 | Mostrar progreso | El detalle de una campaña muestra su meta y el total de aportes confirmados o registrados según el modo de operación. |
| RF-09 | Registrar donación | El sistema permite registrar un aporte asociado a una campaña mediante el flujo de prueba o de pago que se haya configurado. |
| RF-10 | Consultar aportes | El creador puede consultar el resumen de aportes de sus campañas, respetando la privacidad de los donantes. |
| RF-11 | Administrar campañas | El administrador puede revisar campañas y realizar las acciones de moderación autorizadas. |
| RF-12 | Administrar usuarios | El administrador puede consultar cuentas y aplicar las acciones de gestión definidas para el MVP. |

## 7. Requisitos no funcionales

- **Seguridad:** las contraseñas deben tratarse mediante mecanismos de hash seguros; las rutas y operaciones privadas deben verificar autenticación y autorización en el servidor.
- **Privacidad:** solo se mostrarán públicamente los datos necesarios para presentar una campaña. La información personal de los donantes debe limitarse según las reglas de privacidad del producto.
- **Integridad:** las donaciones deben estar asociadas a una campaña válida y sus estados deben distinguir claramente entre pendientes, confirmadas, fallidas o de prueba, según el flujo implementado.
- **Validación:** los datos deben validarse tanto en la interfaz como en el servidor.
- **Usabilidad:** la interfaz debe presentar formularios comprensibles, mensajes de error claros y navegación consistente.
- **Mantenibilidad:** el código debe organizarse por funcionalidades o según la arquitectura ya establecida en el repositorio.
- **Disponibilidad local:** durante el desarrollo, la aplicación y PostgreSQL deben poder iniciarse siguiendo las instrucciones del proyecto y Docker Compose.
- **Configuración:** las credenciales y claves deben gestionarse mediante variables de entorno, nunca mediante valores secretos escritos directamente en el código.

## 8. Flujos principales

### 8.1 Creación de una campaña

1. El usuario se registra o inicia sesión.
2. Selecciona la opción para crear una campaña.
3. Completa la información solicitada y establece una meta.
4. El sistema valida los datos.
5. La campaña se guarda con el estado inicial definido por el producto (por ejemplo, borrador o pendiente de revisión).
6. Cuando corresponda, la campaña se publica y aparece en el listado.

### 8.2 Consulta y aporte a una campaña

1. El visitante abre el listado de campañas.
2. Selecciona una campaña y consulta su descripción, meta y progreso.
3. Selecciona la opción para aportar.
4. El sistema solicita los datos permitidos para el flujo de aporte.
5. El aporte se registra como prueba o se procesa mediante el proveedor seleccionado.
6. El progreso se actualiza únicamente de acuerdo con el estado válido del aporte.

### 8.3 Supervisión administrativa

1. El administrador inicia sesión con una cuenta autorizada.
2. Accede al panel administrativo.
3. Consulta campañas y usuarios.
4. Revisa los elementos que requieren atención.
5. Ejecuta únicamente las acciones permitidas y el sistema registra el cambio correspondiente.

## 9. Datos principales del sistema

Las siguientes entidades son una propuesta conceptual que debe ajustarse al esquema real de la base de datos y a las migraciones del proyecto:

- **User:** identificador, nombre, correo electrónico, hash de contraseña, rol, estado y fechas de creación/actualización.
- **Campaign:** identificador, creador, título, descripción, meta, categoría, estado y fechas relevantes.
- **Donation:** identificador, campaña, donante (si se encuentra identificado), monto, estado, referencia externa si aplica y fecha.
- **AuditLog (opcional para el MVP):** identificador del actor, acción, entidad afectada y fecha, para registrar operaciones administrativas importantes.

No se deben guardar números completos de tarjetas ni códigos de seguridad en estas entidades.

## 10. Organización propuesta de funcionalidades dentro de src/

La siguiente tabla es una **propuesta de organización**. Antes de implementarla, se debe revisar el contenido real de `src/` y respetar el framework y los patrones existentes. Si el proyecto ya tiene otra estructura, se actualizará esta tabla para reflejarla.

| Funcionalidad | Responsabilidad | Carpeta propuesta |
|---|---|---|
| Autenticación | Registro, inicio/cierre de sesión y control de acceso | `src/auth/` |
| Usuarios y perfiles | Datos del perfil y operaciones propias del usuario | `src/users/` |
| Campañas | Creación, edición, listado, detalle y estados | `src/campaigns/` |
| Donaciones | Registro, estado e historial de aportes | `src/donations/` |
| Panel administrativo | Supervisión de usuarios y campañas | `src/admin/` |
| Elementos compartidos | Validaciones, utilidades y componentes reutilizables | `src/shared/` |

La ubicación de páginas, componentes visuales, rutas HTTP, servicios y repositorios dependerá de la arquitectura real del proyecto. No se deben crear todas estas carpetas automáticamente si el framework utiliza otra convención.

## 11. Indicadores iniciales de éxito

- Un usuario puede completar el registro y acceder a su cuenta.
- Un creador puede crear una campaña y consultarla posteriormente.
- Una campaña publicada aparece en el listado y muestra su información.
- Un aporte de prueba puede asociarse correctamente a una campaña.
- El progreso de la campaña coincide con los aportes válidos según las reglas definidas.
- Un administrador puede acceder a las herramientas de supervisión sin conceder esos permisos a usuarios normales.
- Las comprobaciones y pruebas disponibles del proyecto se ejecutan sin errores conocidos.

## 12. Suposiciones y decisiones pendientes

Antes de cerrar el PRD y desarrollar funcionalidades relacionadas, el equipo debe confirmar:

1. Si las campañas se publican inmediatamente o requieren aprobación administrativa.
2. Si los aportes del MVP serán simulados o se integrará un proveedor de pagos en modo de pruebas.
3. Si los donantes podrán aportar sin crear una cuenta.
4. Qué datos de los donantes serán visibles para el creador y para el público.
5. Qué categorías, estados y campos serán obligatorios para una campaña.
6. Qué framework y estructura concreta utiliza actualmente el repositorio.
7. Qué acciones administrativas estarán disponibles en la primera versión.

Estas decisiones deben documentarse antes de considerarlas requisitos definitivos.

## 13. Prioridad sugerida para el MVP

1. Configuración del proyecto y conexión con PostgreSQL.
2. Registro, inicio de sesión y roles.
3. Creación y consulta de campañas.
4. Registro de aportes de prueba y actualización del progreso.
5. Panel del creador.
6. Panel administrativo básico.
7. Pruebas, validaciones y documentación.
