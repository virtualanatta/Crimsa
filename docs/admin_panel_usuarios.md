# 📘 Panel de Administración – Gestión de Usuarios

## 🎯 Objetivo

Este módulo permite a los administradores gestionar los usuarios del sistema, incluyendo creación, visualización y modificación de datos.

---

## 📍 Archivos principales

```text
src/pages/AdminPage.jsx
src/components/AdminUserForm.jsx
src/components/AdminUserTable.jsx
src/services/adminService.js
```

---

## 🧩 Estructura del Módulo

El panel de administración está dividido en:

```text
AdminPage (lógica principal)
   ↓
Form (crear usuario)
   ↓
Tabla (visualizar usuarios)
   ↓
Service (conexión backend)
```

---

## 🧠 Funcionamiento General

## 🔹 AdminPage.jsx

Es el componente principal que:

- Carga los usuarios
- Controla acciones del sistema
- Coordina formulario y tabla
- Usa `adminService` para obtener datos

---

## 🔹 AdminUserForm.jsx

Formulario para crear usuarios.

### 📥 Campos incluidos

- `nombre_usuario`
- `email`
- `password`
- `nombre`
- `apellido_1`
- `apellido_2`
- `dni_nie_pasaporte`
- `rol`

### 🧠 Función

- Recoger datos del usuario
- Enviar la información al sistema

---

## 🔹 AdminUserTable.jsx

Tabla que muestra los usuarios del sistema.

### 📊 Información mostrada

- Nombre completo
- Usuario
- Email
- DNI/NIE
- Rol
- Estado

### ⚙️ Acciones disponibles

- Cambiar rol
- Cambiar contraseña

---

## 🔹 adminService.js

Este archivo es el puente entre frontend y backend.

### 📌 Responsabilidades

- Obtener usuarios
- Crear usuarios
- Actualizar datos

### ⚠️ Estado actual

- Usa datos simulados (mock)

### 🔮 Futuro

- Conexión real con API REST

---

## 🔗 Integración con Backend

El backend debe proporcionar los siguientes endpoints:

### 📥 Obtener usuarios

```http
GET /api/admin/users
```

---

### ➕ Crear usuario

```http
POST /api/admin/users
```

---

### 🔄 Cambiar rol

```http
PUT /api/admin/users/:id/role
```

---

### 🔑 Cambiar contraseña

```http
PUT /api/admin/users/:id/password
```

---

## 🧾 Formato de datos esperado

El backend debe devolver un JSON con esta estructura:

```json
{
  "id": 1,
  "nombre_usuario": "gerard",
  "email": "test@test.com",
  "nombre": "Gerard",
  "apellido_1": "Martinez",
  "dni_nie_pasaporte": "12345678A",
  "estado": "activo",
  "rol": "admin"
}
```

---

## 🔄 Flujo del módulo

```text
Usuario (Admin)
      ↓
Formulario / Tabla
      ↓
AdminPage
      ↓
adminService
      ↓
Backend (API)
      ↓
Base de datos
```

---

## ⚠️ Importante

- ❌ El frontend NO gestiona la base de datos
- ✅ Toda la lógica debe estar en el backend
- ✅ El frontend solo consume datos en JSON

---

## 🧪 Estado actual del módulo

- ✅ Interfaz completamente funcional
- ✅ Formularios y tabla implementados
- ✅ Lógica estructurada correctamente
- 🔄 Falta conexión con backend real

---

## 🔮 Mejoras futuras

- Validaciones de formulario
- Confirmaciones (modales)
- Eliminación de usuarios
- Filtros y búsqueda
- Paginación
- Integración completa con backend

---

## 🧠 Buenas prácticas aplicadas

- Separación de lógica (service)
- Componentes reutilizables
- Estructura clara y escalable
- Preparado para integración backend

---

## 📌 Nota final

El panel de administración es el núcleo de gestión del sistema y está preparado para integrarse fácilmente con el backend, facilitando el desarrollo conjunto.
