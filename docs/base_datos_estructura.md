# 📘 Base de Datos – Estructura y Relaciones

## 🎯 Objetivo

Este documento describe la estructura de la base de datos utilizada en el sistema, incluyendo las tablas principales, sus relaciones y el propósito de cada una.

---

## 🧱 Tecnología

- **Sistema gestor:** PostgreSQL
- **Tipo de base de datos:** Relacional

---

## 🗄️ Tablas Principales

El sistema se basa en tres tablas clave:

- `usuarios`
- `roles`
- `usuarios_roles`

---

## 👤 Tabla: `usuarios`

Almacena la información principal de cada usuario del sistema.

### 📊 Campos principales

- `id`
- `nombre_usuario`
- `email`
- `password`
- `nombre`
- `apellido_1`
- `apellido_2`
- `dni_nie_pasaporte`
- `estado`

### 📌 Descripción

- Contiene los datos personales y de acceso
- Cada registro representa un usuario único

---

## 🛠️ Tabla: `roles`

Define los roles disponibles en el sistema.

### 📊 Campos principales

- `id`
- `nombre`

### 📌 Ejemplos de roles

- `admin`
- `profesor`
- `alumno`

---

## 🔗 Tabla: `usuarios_roles`

Tabla intermedia que relaciona usuarios con roles.

### 📊 Campos principales

- `usuario_id`
- `rol_id`

---

## 🔄 Relaciones

El sistema sigue una relación de tipo:

```text
usuarios → usuarios_roles → roles
```

### 📌 Interpretación

- Un usuario puede tener uno o varios roles
- Un rol puede pertenecer a varios usuarios
- Relación muchos a muchos

---

## 🧠 Modelo Conceptual

```text
[usuarios] ----< [usuarios_roles] >---- [roles]
```

---

## 🔄 Flujo de Datos

### Ejemplo: obtener usuarios con su rol

```text
Frontend solicita usuarios
      ↓
Backend consulta:
usuarios + usuarios_roles + roles
      ↓
Backend transforma datos
      ↓
Devuelve JSON limpio al frontend
```

---

## 🧾 Ejemplo de Resultado

El backend debe devolver datos simplificados:

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

## ⚠️ Importante

- ❌ No enviar relaciones complejas al frontend
- ❌ No exponer estructura interna de la base de datos
- ✅ El backend debe simplificar los datos
- ✅ El frontend solo consume JSON limpio

---

## 🧪 Estado Actual

Actualmente:

- La base de datos está creada
- Las tablas están definidas
- La relación entre usuarios y roles está implementada
- El frontend aún no está conectado directamente al backend

---

## 🔮 Mejoras Futuras

- Añadir tabla de asignaturas
- Relacionar profesores con asignaturas
- Relacionar alumnos con asignaturas
- Añadir sistema de mensajería
- Gestión de contenidos

---

## 🧠 Buenas Prácticas

- Usar claves primarias (`id`)
- Definir claves foráneas correctamente
- Evitar duplicidad de datos
- Mantener el modelo escalable
- Documentar cambios en la base de datos

---

## 📌 Nota final

La base de datos está diseñada para ser flexible, escalable y preparada para futuras funcionalidades, siendo una base sólida para el crecimiento de la plataforma educativa.
