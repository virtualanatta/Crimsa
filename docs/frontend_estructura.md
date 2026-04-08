# 📘 Estructura del Frontend – Plataforma Web Educativa

## 🎯 Objetivo

Este documento describe la estructura del frontend del proyecto, facilitando la comprensión del código y la colaboración entre desarrolladores.

---

## 📍 Ubicación del Proyecto

```bash
/mnt/TFG_CRIMSA/01_PROYECTO/CODIGO/frontend/src
```

---

## 🧱 Estructura de Carpetas

```text
src/
├── pages/         → Vistas principales de la aplicación
├── components/    → Componentes reutilizables
├── services/      → Conexión con el backend (API)
├── context/       → Gestión del estado global (autenticación)
├── assets/        → Imágenes y recursos estáticos
```

---

## 📂 Descripción de Carpetas

## 📄 pages/

Contiene las páginas principales que representan vistas completas de la aplicación.

### Ejemplos

```text
src/pages/AdminPage.jsx
src/pages/ProfesorPage.jsx
```

### Responsabilidades

- Renderizar vistas completas
- Coordinar componentes
- Gestionar lógica de alto nivel

---

## 🧩 components/

Contiene componentes reutilizables que pueden ser usados en distintas partes de la aplicación.

### Ejemplos

```text
src/components/AdminUserForm.jsx
src/components/AdminUserTable.jsx
```

### Responsabilidades

- Mostrar UI específica
- Recibir props
- No contener lógica compleja de negocio

---

## 🔗 services/

Encargado de la comunicación con el backend.

### Ejemplo

```text
src/services/adminService.js
```

### Responsabilidades

- Realizar llamadas HTTP (GET, POST, PUT...)
- Centralizar acceso a la API
- Evitar lógica de backend en componentes

### ⚠️ Estado actual

- Se utilizan datos simulados (mock)

### 🔮 Futuro

- Conexión real con backend (Node.js)

---

## 🔐 context/

Gestión del estado global de la aplicación.

### Ejemplo

```text
src/context/AuthContext.jsx
```

### Responsabilidades

- Guardar usuario autenticado
- Proporcionar acceso global al usuario
- Manejar login y logout

---

## 🖼️ assets/

Contiene recursos estáticos como imágenes.

### Ejemplo

```text
src/assets/desarrollo-web.jpg
```

### Uso

- Mejora visual de la interfaz
- Identificación de asignaturas

---

## 🔄 Flujo Interno del Frontend

```text
Page (pages/)
   ↓
Components (components/)
   ↓
Services (services/)
   ↓
Backend (API)
```

---

## 🧠 Buenas Prácticas Aplicadas

- Separación de responsabilidades
- Componentes reutilizables
- Centralización de llamadas a API
- Uso de Context para estado global
- Código organizado y escalable

---

## ⚠️ Importante

- ❌ El frontend NO accede directamente a la base de datos
- ✅ Siempre se comunica a través del backend
- ✅ Los datos deben venir en formato JSON limpio

---

## 🚀 Cómo ejecutar el frontend

```bash
npm run dev
```

### Acceso

```text
http://100.107.56.81:8080
```

---

## 📌 Nota final

Esta estructura permite escalar el proyecto fácilmente, mantener el código limpio y facilitar la colaboración entre frontend y backend.
