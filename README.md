# 🔐 Proyecto Laravel 12 - Sistema de Autenticación

**Elaborado por:** Manuel Guillén  
**Fecha:** 28/9/2025

---

## 📋 Introducción

Este proyecto implementa un sistema de autenticación completo utilizando **Laravel 12**, siguiendo la arquitectura **MVC (Model-View-Controller)**. El objetivo del laboratorio es demostrar la implementación de un sistema de login y registro de usuarios con las mejores prácticas de Laravel.

### 🏗️ Arquitectura MVC en Laravel

- **📊 Modelos (Models)**: Ubicados en `app/Models/`, representan la lógica de negocio y la estructura de datos. En este caso, el modelo `User` maneja la autenticación de usuarios.

- **🎨 Vistas (Views)**: Ubicadas en `resources/views/`, contienen la lógica de presentación. Incluye vistas para login, registro, dashboard y layouts base.

- **🎮 Controladores (Controllers)**: Ubicados en `app/Http/Controllers/`, manejan la lógica de la aplicación y actúan como intermediarios entre modelos y vistas.

- **🛣️ Rutas (Routes)**: Definidas en `routes/web.php`, establecen las URLs y conectan las peticiones HTTP con los controladores correspondientes.

---

## 🚀 Instalación y Configuración

### ⚙️ Prerrequisitos
- **PHP** 8.2 o superior
- **Composer**
- **Node.js** y **NPM**
- **Base de datos SQLite** (incluida por defecto)

### 1️⃣ Instalación de Dependencias

```bash
# Instalar dependencias de PHP
composer install

# Instalar dependencias de Node.js
npm install
```

### 2️⃣ Configuración del Archivo .env

```bash
# Copiar el archivo de configuración de ejemplo
cp .env.example .env

# Generar la clave de aplicación
php artisan key:generate
```

### 3️⃣ Configuración de Base de Datos

```bash
# Crear la base de datos SQLite (si no existe)
touch database/database.sqlite

# Ejecutar las migraciones
php artisan migrate
```

### 4️⃣ Compilar Assets Frontend

```bash
# Compilar assets para desarrollo
npm run dev

# O para producción
npm run build
```

### 5️⃣ Iniciar el Servidor

```bash
# Iniciar el servidor de desarrollo
php artisan serve
```

---

## 🔧 Secuencia de Comandos Utilizados

### 🔐 Instalación del Sistema de Autenticación

```bash
# 1. Instalar Laravel UI
composer require laravel/ui

# 2. Generar las vistas de autenticación con Bootstrap
php artisan ui bootstrap --auth

# 3. Instalar dependencias de Node.js
npm install

# 4. Compilar los assets
npm run dev

# 5. Ejecutar migraciones para crear las tablas de autenticación
php artisan migrate
```

### 📊 Comandos de Migración Utilizados

```bash
# Crear migración (ya incluida por defecto)
php artisan make:migration create_users_table

# Ejecutar migraciones
php artisan migrate

# Ver estado de migraciones
php artisan migrate:status

# Rollback de migraciones (si es necesario)
php artisan migrate:rollback
```

---

## 🗄️ Base de Datos

### 🎯 Entorno de Base de Datos
- **Tipo**: SQLite
- **Archivo**: `database/database.sqlite`
- **Configuración**: Definida en el archivo `.env`

### ⚙️ Configuración en .env
```env
DB_CONNECTION=sqlite
DB_DATABASE=database/database.sqlite
```

### 📋 Tablas Creadas

#### 1️⃣ **users**: Almacena información de usuarios
- `id` (Primary Key)
- `name`
- `email` (único)
- `email_verified_at`
- `password` (hasheada)
- `remember_token`
- `timestamps`

#### 2️⃣ **password_reset_tokens**: Tokens para recuperación de contraseñas
- `email` (Primary Key)
- `token`
- `created_at`

#### 3️⃣ **sessions**: Sesiones de usuario
- `id` (Primary Key)
- `user_id` (Foreign Key)
- `ip_address`
- `user_agent`
- `payload`
- `last_activity`

### 💾 Backup de Base de Datos

El archivo `database/database.sqlite` se incluye en el repositorio como respaldo de la base de datos con la estructura inicial.

---

## 📸 Resultado del Laboratorio

![Dashboard de Usuario Autenticado](https://via.placeholder.com/800x400/4F46E5/FFFFFF?text=Dashboard+de+Usuario+Autenticado)

> *Imagen mostrando el dashboard principal después del login exitoso*

---

## ⚠️ Dificultades y Soluciones

### 🚨 Problema 1: Error de Migración
**Descripción**: Error al ejecutar `php artisan migrate` debido a configuración incorrecta de base de datos.

**✅ Solución**: 
- Verificar que el archivo `.env` tenga la configuración correcta para SQLite
- Asegurar que el archivo `database/database.sqlite` exista
- Ejecutar `php artisan config:clear` antes de las migraciones

### 🚨 Problema 2: Assets No Compilados
**Descripción**: Las vistas de autenticación no mostraban estilos correctamente.

**✅ Solución**:
- Ejecutar `npm install` para instalar dependencias
- Compilar assets con `npm run dev`
- Verificar que los archivos CSS/JS se generen en `public/css` y `public/js`

### 🚨 Problema 3: Configuración de Rutas de Autenticación
**Descripción**: Las rutas de autenticación no funcionaban correctamente.

**✅ Solución**:
- Verificar que `Auth::routes()` esté incluido en `routes/web.php`
- Asegurar que el middleware de autenticación esté configurado correctamente
- Verificar que las vistas estén en las ubicaciones correctas

---

## 📚 Referencias

1. **📖 Laravel Documentation - Authentication**  
   https://laravel.com/docs/authentication  
   *Documentación oficial de Laravel sobre implementación de autenticación*

2. **📦 Laravel UI Package**  
   https://github.com/laravel/ui  
   *Repositorio oficial del paquete Laravel UI para scaffolding de autenticación*

3. **🗄️ Laravel Database Migrations**  
   https://laravel.com/docs/migrations  
   *Guía oficial sobre migraciones de base de datos en Laravel*

4. **🎨 Bootstrap Documentation**  
   https://getbootstrap.com/docs/5.3/  
   *Documentación de Bootstrap para el diseño de las vistas de autenticación*

---

## 🏗️ Estructura del Proyecto

```
lab2/
├── app/
│   ├── Http/Controllers/
│   │   ├── Auth/          # Controladores de autenticación
│   │   └── HomeController.php
│   └── Models/
│       └── User.php       # Modelo de usuario
├── database/
│   ├── migrations/        # Archivos de migración
│   └── database.sqlite    # Base de datos SQLite
├── resources/
│   └── views/
│       ├── auth/          # Vistas de login/registro
│       ├── layouts/       # Layouts base
│       └── home.blade.php # Dashboard principal
├── routes/
│   └── web.php           # Rutas de la aplicación
└── public/               # Archivos públicos y assets
```

---

## 🎯 Objetivo del Laboratorio

El objetivo principal de este laboratorio es implementar un sistema de autenticación completo en Laravel, demostrando:

- ✅ Configuración inicial de un proyecto Laravel
- ✅ Implementación de autenticación de usuarios
- ✅ Uso de migraciones para estructura de base de datos
- ✅ Integración de frontend con Bootstrap
- ✅ Manejo de sesiones y middleware
- ✅ Buenas prácticas de desarrollo con Laravel

---

## 📝 Notas Adicionales

- 🔧 El proyecto utiliza **Laravel 12** con **PHP 8.2+**
- 🔐 La autenticación incluye registro, login, logout y recuperación de contraseña
- 🛡️ Se implementó middleware de autenticación para proteger rutas
- 📱 El diseño es responsive utilizando **Bootstrap 5**
- 💾 La base de datos SQLite facilita el desarrollo y testing

---

## 🏛️ Información del Estudiante

---

<div align="center">

### 📋 Información del Laboratorio

**Este laboratorio ha sido desarrollado por el estudiante de la Universidad Tecnológica de Panamá:**

| Campo | Información |
|-------|-------------|
| **👤 Nombre:** | [Manuel Guillén] |
| **📧 Correo:** | [manuel.guillen1@utp.ac.pa] |
| **📚 Curso:** | [Ing. Web] |
| **👩‍🏫 Instructor del Laboratorio:** | **Ing. Irina Fong** |

---



