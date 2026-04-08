# 📘 Integración Frontend ↔ Backend

## 🎯 Objetivo

Este documento define cómo debe realizarse la comunicación entre el frontend (React) y el backend (Node.js), estableciendo endpoints, formatos de datos y flujo de funcionamiento.

---

## 🧠 Concepto Clave

El frontend **NO accede directamente a la base de datos**.

### Flujo de comunicación

```text
Frontend (React)
      ↓
Services (adminService.js)
      ↓
Backend (API REST)
      ↓
Base de datos (PostgreSQL)
```

---

## 🔗 Punto de Conexión

El archivo encargado de comunicarse con el backend es:

```text
src/services/adminService.js
```

---

## 📡 Endpoints Necesarios

El backend debe implementar los siguientes endpoints:

---

## 📥 Obtener usuarios

```http
GET /api/admin/users
```

### 📌 Descripción

Devuelve todos los usuarios del sistema

---

## ➕ Crear usuario

```http
POST /api/admin/users
```

### 📌 Descripción

Crea un nuevo usuario

### 📥 Body esperado

```json
{
  "nombre_usuario": "gerard",
  "email": "test@test.com",
  "password": "123456",
  "nombre": "Gerard",
  "apellido_1": "Martinez",
  "apellido_2": "Lopez",
  "dni_nie_pasaporte": "12345678A",
  "rol": "admin"
}
```

---

## 🔄 Cambiar rol

```http
PUT /api/admin/users/:id/role
```

### 📌 Descripción

Actualiza el rol del usuario

### 📥 Body esperado

```json
{
  "rol": "profesor"
}
```

---

## 🔑 Cambiar contraseña

```http
PUT /api/admin/users/:id/password
```

### 📌 Descripción

Actualiza la contraseña del usuario

### 📥 Body esperado

```json
{
  "password": "nueva_password"
}
```

---

## 🧾 Formato de Respuesta

El backend debe devolver datos en formato JSON limpio:

```json
{
  "id": 1,
  "nombre_usuario": "gerard",
  "email": "test@test.com",
  "nombre": "Gerard",
  "apellido_1": "Martinez",
  "apellido_2": "Lopez",
  "dni_nie_pasaporte": "12345678A",
  "estado": "activo",
  "rol": "admin"
}
```

---

## 🔄 Flujo Completo de Ejemplo

### 🧪 Caso: Obtener usuarios

```text
AdminPage.jsx
      ↓
adminService.getUsers()
      ↓
GET /api/admin/users
      ↓
Backend procesa la petición
      ↓
Consulta a PostgreSQL
      ↓
Devuelve JSON
      ↓
React renderiza la tabla
```

---

## ⚠️ Reglas Importantes

- ❌ No enviar datos innecesarios al frontend
- ❌ No exponer estructura interna de la base de datos
- ✅ Devolver JSON limpio y simplificado
- ✅ Validar datos en el backend
- ✅ Manejar errores correctamente (status HTTP)

---

## 🧪 Estado Actual

Actualmente:

- El frontend usa datos simulados (mock)
- No hay conexión real con backend
- La estructura ya está preparada para integrarse

---

## 🔮 Próximos Pasos

### En el backend

- Crear rutas `/api/admin/...`
- Conectar con PostgreSQL
- Implementar controladores
- Validar datos
- Manejar errores

### En el frontend

- Sustituir datos mock por llamadas reales
- Usar `fetch` o `axios`
- Manejar respuestas y errores

---

## 🧠 Buenas Prácticas

- Mantener lógica en backend
- Usar servicios en frontend
- Separar responsabilidades
- Documentar endpoints
- Usar nombres consistentes

---

## 📌 Nota final

Este documento permite que frontend y backend trabajen de forma independiente pero coordinada, asegurando una integración clara, escalable y mantenible.
