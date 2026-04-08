# 📘 Sistema de Autenticación – Frontend

## 🎯 Objetivo

Este documento describe cómo funciona el sistema de autenticación en el frontend, permitiendo gestionar el usuario logueado y su acceso a la aplicación.

---

## 📍 Ubicación

```text
src/context/AuthContext.jsx
```

---

## 🧠 Concepto Clave

La autenticación se gestiona mediante **Context API de React**, lo que permite:

- Compartir el usuario en toda la aplicación
- Evitar pasar props manualmente entre componentes
- Centralizar la lógica de login y logout

---

## 🧩 Funcionalidades principales

El `AuthContext` permite:

- ✅ Guardar el usuario autenticado
- ✅ Acceder al usuario desde cualquier componente
- ✅ Manejar el login
- ✅ Manejar el logout

---

## 👤 Usuario Autenticado

El contexto almacena información del usuario, por ejemplo:

```json
{
  "id": 1,
  "nombre_usuario": "gerard",
  "rol": "admin"
}
```

Este objeto estará disponible globalmente en toda la aplicación.

---

## 🔄 Flujo de Autenticación

```text
Login (formulario)
      ↓
AuthContext (guardar usuario)
      ↓
Acceso global en la app
      ↓
Uso en páginas y componentes
```

---

## 🧪 Uso del Contexto

Para acceder al usuario desde cualquier componente:

```javascript
import { useAuth } from "../context/AuthContext";

const { user } = useAuth();
```

### Ejemplo de uso

```jsx
<h1>Bienvenido, {user.nombre_usuario}</h1>
```

---

## 🔓 Logout

El sistema permite cerrar sesión:

```javascript
const { logout } = useAuth();

logout();
```

Esto elimina el usuario del contexto y devuelve al estado inicial.

---

## 🔐 Control de Acceso (Roles)

El sistema permite diferenciar usuarios según su rol:

- `admin`
- `profesor`
- `alumno` (futuro)

### Ejemplo

```javascript
if (user.rol === "admin") {
  // mostrar panel admin
}
```

---

## ⚠️ Estado Actual

Actualmente:

- La autenticación es simulada (mock)
- No hay conexión real con backend
- No hay persistencia (ej: localStorage) implementada

---

## 🔮 Mejoras Futuras

- Conectar login con backend real
- Implementar JWT (tokens)
- Guardar sesión en localStorage o cookies
- Proteger rutas (Private Routes)
- Control de permisos más avanzado

---

## 🧠 Buenas Prácticas

- Centralizar la autenticación en un único contexto
- No duplicar lógica en componentes
- Mantener el usuario accesible globalmente
- Separar autenticación de lógica de UI

---

## 📌 Nota final

El AuthContext es el núcleo de la gestión de usuarios en el frontend y será clave en la integración con el backend en fases posteriores.
