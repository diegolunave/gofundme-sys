# gofundme-sys

### Sistema de gestión de campañas de recaudación de fondos y donaciones

**gofundme-sys** es una aplicación web orientada a la creación, administración y seguimiento de campañas de recaudación de fondos. Su propósito es ofrecer un espacio digital donde las personas puedan crear campañas para diferentes causas, recibir donaciones y consultar el progreso de los fondos recaudados.

El proyecto está inspirado en plataformas de crowdfunding como GoFundMe y busca facilitar la conexión entre personas que necesitan apoyo económico y aquellas que desean contribuir a una causa.

---

## Objetivo del proyecto

Desarrollar un sistema web que permita gestionar campañas de recaudación de fondos de manera organizada, facilitando la publicación de campañas, el registro de donaciones y el seguimiento de los objetivos económicos establecidos.

## Usuarios del sistema

- **Creadores de campañas:** personas que desean publicar campañas para recaudar fondos y administrar sus objetivos.
- **Donantes:** usuarios que desean consultar campañas y realizar aportes económicos.
- **Administradores:** responsables de supervisar las campañas, los usuarios y el funcionamiento general de la plataforma.

## Funcionalidades principales

El sistema contempla las siguientes funcionalidades:

1. **Registro e inicio de sesión:** creación de cuentas y autenticación de usuarios.
2. **Creación de campañas:** publicación y administración de campañas de recaudación.
3. **Gestión de donaciones:** registro y consulta de los aportes realizados.
4. **Seguimiento de recaudaciones:** visualización del progreso económico de cada campaña.
5. **Panel de administración:** herramientas para supervisar usuarios, campañas y actividad del sistema.

*Nota: estas funcionalidades representan el alcance previsto del proyecto y su implementación se desarrollará progresivamente.*

## Tecnologías utilizadas

- **Node.js:** entorno de ejecución de JavaScript.
- **Express:** framework para el desarrollo del servidor y las rutas de la aplicación.
- **PostgreSQL:** sistema de gestión de bases de datos relacional.
- **Docker:** herramienta para gestionar los servicios y el entorno de desarrollo.
- **npm:** administrador de paquetes y dependencias.

## Requisitos previos

Antes de instalar el proyecto, es necesario contar con:

- Node.js y npm.
- Docker Desktop.
- Git.
- Una cuenta de GitHub.

## Instalación y configuración

### 1. Clonar el repositorio

```bash
git clone https://github.com/diegolunave/gofundme-sys.git
```

Entrar en la carpeta del proyecto:

```bash
cd gofundme-sys
```

### 2. Instalar las dependencias

```bash
npm install
```

### 3. Configurar las variables de entorno

En Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Después, revisar el archivo `.env` y completar las variables de configuración necesarias.

### 4. Iniciar la base de datos

Asegurarse de que Docker Desktop esté abierto y ejecutar:

```bash
docker compose up -d --wait
```

### 5. Crear las tablas y cargar los datos de prueba

Ejecutar las migraciones:

```bash
npm run migrate
```

Cargar los datos iniciales:

```bash
npm run seed
```

### 6. Ejecutar la aplicación

```bash
npm run dev
```

Una vez iniciado el servidor, abrir en el navegador:

http://localhost:5173

## Comprobación del proyecto

Para ejecutar las comprobaciones configuradas:

```bash
npm run check
```

Para ejecutar las pruebas de integración:

```bash
npm run test:integration
```

## Estructura general

```text
gofundme-sys/
│
├── src/                    # Código fuente de la aplicación
│
├── docs/
│   └── PRD.md              # Documento de requisitos del producto
│
├── AGENTS.md               # Descripción e instrucciones del proyecto
├── docker-compose.yml      # Configuración de Docker
├── package.json            # Dependencias y scripts
├── package-lock.json       # Versiones de dependencias
├── .env.example            # Plantilla de variables de entorno
└── README.md               # Documentación principal
```

## Alcance del proyecto

El desarrollo contempla inicialmente la implementación de los módulos de autenticación, usuarios, campañas, donaciones y administración.

La integración de servicios externos para procesar pagos reales se considera una decisión pendiente de definición y desarrollo.

## Estado del proyecto

**En desarrollo — Sprint 0**

Actualmente se está realizando la configuración inicial del entorno, la preparación de la base de datos, la documentación de requisitos y la organización del proyecto mediante GitHub.

---

## Autor

**Diego Luna**

Proyecto académico desarrollado para la asignatura **Lenguaje de Programación II**.