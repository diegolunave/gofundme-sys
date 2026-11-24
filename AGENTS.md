# AGENTS.md — gofundme-sys

## 1. Descripción del producto

**gofundme-sys** es una aplicación web para gestionar campañas de recaudación de fondos. Permite que las personas creen y publiquen campañas, que otras personas consulten las iniciativas y registren sus donaciones, y que los administradores supervisen el funcionamiento general de la plataforma.

El proyecto está inspirado en la categoría de plataformas de crowdfunding y recaudación de fondos. Debe desarrollar una identidad, interfaz y código propios; no debe copiar marcas, textos, diseños ni recursos protegidos de otras plataformas.

## 2. Objetivo principal

Ofrecer un espacio digital organizado y fácil de usar donde los creadores puedan presentar una necesidad o iniciativa, definir una meta de recaudación y consultar el progreso de su campaña; donde los donantes puedan conocer las campañas y registrar sus aportes; y donde los administradores puedan supervisar usuarios, campañas y actividad.

## 3. Usuarios del sistema

- **Creador de campañas:** persona que se registra, publica una campaña, proporciona su descripción, establece una meta y consulta las donaciones recibidas.
- **Donante:** persona que consulta campañas y registra o realiza un aporte mediante el mecanismo que se defina para el proyecto.
- **Administrador:** usuario autorizado para revisar y gestionar cuentas, campañas y actividad de la plataforma.

El sistema debe aplicar permisos según el rol. Una persona no debe obtener permisos de administrador por el simple hecho de registrarse.

## 4. Funcionalidades principales

1. Registro, inicio de sesión y cierre de sesión.
2. Gestión básica del perfil de usuario.
3. Creación, edición y consulta de campañas.
4. Publicación de información de campaña: título, descripción, categoría, meta, imágenes (si están soportadas) y estado.
5. Consulta de campañas y de su progreso de recaudación.
6. Registro y consulta de donaciones asociadas a una campaña.
7. Panel del creador para consultar y administrar sus propias campañas.
8. Panel administrativo para supervisar usuarios, campañas y actividad.

## 5. Tecnologías y entorno

Según las instrucciones de configuración del curso, el proyecto utiliza o contempla:

- **Node.js y npm:** ejecución del proyecto y gestión de dependencias.
- **PostgreSQL:** persistencia de datos.
- **Docker Compose:** ejecución local de los servicios definidos por el repositorio.
- **Git y GitHub:** control de versiones, Pull Requests, Issues y Releases.

El framework de frontend, el framework de backend, el ORM y cualquier proveedor de pagos deben confirmarse revisando `package.json`, la configuración y el código existente. No se deben introducir tecnologías nuevas sin una necesidad justificada y sin respetar las decisiones ya tomadas en el repositorio.

## 6. Organización prevista del código

La estructura concreta debe seguir el código ya existente. Como propuesta inicial, las funcionalidades podrían organizarse así:

- `src/` — código fuente de la aplicación.
- `src/auth/` — registro, autenticación, sesiones y control de acceso.
- `src/users/` — perfiles y gestión de usuarios.
- `src/campaigns/` — creación, edición, consulta y estados de campañas.
- `src/donations/` — registro y consulta de aportes.
- `src/admin/` — herramientas y vistas administrativas.
- `src/shared/` — componentes, utilidades y lógica compartida.
- `docs/` — documentación del proyecto, incluido el PRD.

Estas rutas son una **propuesta**, no una afirmación de que las carpetas ya existan. Antes de crear o mover archivos, inspecciona la estructura real de `src/` y adapta la organización al framework del proyecto. Si el repositorio usa una estructura por capas o por funcionalidades diferente, conserva el patrón existente.

## 7. Convenciones de desarrollo

- Lee `README.md`, `package.json`, la configuración y la documentación de `docs/` antes de hacer cambios importantes.
- Mantén el estilo, el lenguaje y la arquitectura que ya utiliza el proyecto.
- Escribe nombres claros y consistentes para archivos, funciones, variables y componentes.
- Mantén separadas las responsabilidades de interfaz, lógica de negocio y acceso a datos, de acuerdo con la arquitectura existente.
- Valida los datos recibidos en el servidor; no confíes únicamente en las validaciones del navegador.
- Aplica autorización en el servidor para las operaciones protegidas y verifica la propiedad de cada campaña antes de permitir cambios.
- No incluyas contraseñas, tokens, claves API ni credenciales en el código, los commits o los documentos públicos.
- Usa variables de entorno para la configuración sensible. Mantén `.env` fuera del control de versiones y actualiza `.env.example` cuando cambien las variables requeridas, sin incluir secretos reales.
- No almacenes directamente números completos de tarjetas ni códigos de seguridad. Cualquier pago real deberá integrarse mediante un proveedor especializado y su entorno de pruebas, después de definir los requisitos correspondientes.
- No registres una donación como pago completado si el proveedor o el flujo de prueba no ha confirmado el resultado.
- Evita cambios destructivos en la base de datos. Las modificaciones del esquema deben realizarse mediante las migraciones del proyecto.
- No añadas dependencias sin justificar su necesidad.

## 8. Pruebas y calidad

Antes de considerar terminado un cambio:

1. Ejecuta las comprobaciones disponibles definidas en `package.json` (por ejemplo, `npm run check`).
2. Ejecuta las pruebas pertinentes (por ejemplo, `npm test` o `npm run test:integration`, si esos scripts existen).
3. Corrige los errores introducidos por el cambio.
4. Comprueba que la aplicación siga iniciando de acuerdo con las instrucciones del proyecto.

No afirmes que una prueba pasó si no se ejecutó o si devolvió errores. Si una prueba no puede ejecutarse, deja constancia del motivo.

## 9. Git y Pull Requests

- Trabaja en ramas descriptivas; evita desarrollar directamente sobre `main`.
- Usa commits pequeños y mensajes que expliquen el cambio.
- En los Pull Requests incluye el objetivo, un resumen de los cambios y las pruebas realizadas.
- No fusiones un Pull Request con comprobaciones obligatorias fallidas.
- No subas archivos generados, dependencias instaladas ni secretos, salvo que el repositorio los requiera expresamente.

## 10. Criterio general

Prioriza una implementación sencilla, segura, mantenible y coherente con el alcance del MVP. Cuando un requisito sea ambiguo, revisa primero la documentación y el código existente; si sigue sin estar definido, documenta la suposición en lugar de presentarla como una decisión confirmada.
