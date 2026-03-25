# 📘 Panel de Administración – Frontend & Backend (TFG)

## 🎯 Objetivo

Este documento describe la implementación del panel de administración del sistema, incluyendo:

- Estructura del frontend
- Componentes principales
- Servicios (API simulada)
- Integración con backend
- Requisitos para el desarrollo backend

---

# 🧱 Estructura del Frontend

```text
src/
├── pages/
│   └── AdminPage.jsx
├── components/
│   ├── AdminUserForm.jsx
│   └── AdminUserTable.jsx
├── services/
│   └── adminService.js
```

---

# 🔑 Archivo clave

```text
src/services/adminService.js
```

---

# 🧩 Servicios (adminService.js)

```javascript
let usuarios = [
  {
    id: 1,
    nombre_usuario: "gerard.admin",
    email: "admin@test.com",
    nombre: "Gerard",
    apellido_1: "Martínez",
    apellido_2: "López",
    dni_nie_pasaporte: "12345678A",
    estado: "activo",
    rol: "admin",
  },
];

export const getUsers = async () => {
  return [...usuarios];
};

export const createUser = async (nuevoUsuario) => {
  const usuario = {
    id: usuarios.length + 1,
    ...nuevoUsuario,
    estado: "activo",
  };

  usuarios.push(usuario);
  return usuario;
};

export const updateUser = async (id, datos) => {
  usuarios = usuarios.map((u) =>
    u.id === id ? { ...u, ...datos } : u
  );
};

export const changeUserPassword = async (id, password) => {
  console.log("Cambio de contraseña para usuario", id);
};
```

---

# 📡 API necesaria (Backend)

## Endpoints

```http
GET /api/admin/users
POST /api/admin/users
PUT /api/admin/users/:id/role
PUT /api/admin/users/:id/password
```

---

# 🧾 Formato esperado

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

