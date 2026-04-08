# 📘 Panel del Profesor – Aula Virtual

## 🎯 Objetivo

El panel del profesor proporciona una vista principal desde la cual el usuario puede visualizar sus asignaturas, consultar información relevante y acceder a funcionalidades clave del sistema.

---

## 📍 Ubicación

```text
src/pages/ProfesorPage.jsx
```

---

## 🧩 Estructura del Componente

El componente está construido utilizando:

- `Layout` → estructura común (Navbar + contenido)
- `useAuth` → acceso al usuario autenticado

---

## 👋 Cabecera de Bienvenida

Se ha implementado una sección de bienvenida:

```html
<section className="welcome-box">
```

### 🎯 Funcionalidad

- Mostrar el nombre del profesor autenticado
- Introducir el panel de forma contextual
- Mejorar la experiencia de usuario

### 🎨 Estilo aplicado

- Fondo degradado
- Texto blanco
- Bordes redondeados
- Sombra ligera

---

## 📊 Resumen de Actividad

Se ha añadido una sección de resumen mediante tarjetas:

```html
<section className="dashboard-summary">
```

### 📌 Información mostrada

- Número de asignaturas activas
- Total de alumnos
- Mensajes pendientes

### 🎯 Objetivo

- Proporcionar una visión rápida del estado del profesor

---

## 📚 Visualización de Asignaturas

Las asignaturas se generan dinámicamente a partir de un array:

```javascript
const asignaturas = [ ... ];
```

### 🧾 Información por asignatura

Cada tarjeta incluye:

- Nombre de la asignatura
- Curso
- Número de alumnos
- Próximo tema
- Imagen representativa

---

## 🖼️ Uso de Imágenes

```javascript
import desarrolloWebImg from "../assets/desarrollo-web.jpg";
```

### 📍 Ubicación

```text
src/assets/
```

### 🎯 Objetivo

- Hacer la interfaz más visual
- Facilitar identificación rápida
- Mejorar UX

---

## 🧱 Diseño de Tarjetas (subject-card)

### 🖼️ 1. Imagen superior

```html
<img className="subject-image" />
```

**Características:**

- Anchura completa
- Altura fija
- `object-fit: fill`

---

### 📏 2. Separación visual

```css
margin-bottom: 10px;
border-bottom: 1px solid #eee;
```

**Objetivo:**

- Mejorar legibilidad
- Evitar saturación visual

---

### 📄 3. Contenido

Incluye:

- Título
- Información estructurada
- Botones de acción

---

## 🔘 Botones de Acción

```html
<button>Ver aula</button>
<button>Ver mensajes</button>
```

### 🎯 Función

- Acceso al aula virtual (futuro)
- Acceso a mensajería

⚠️ Actualmente son elementos visuales preparados para integración futura.

---

## 📱 Diseño Responsive

```css
.subjects-grid {
  grid-template-columns: repeat(auto-fit, minmax(290px, 1fr));
}
```

### ✅ Ventajas

- Adaptación automática
- Mejor visualización en móvil
- Distribución uniforme

---

## 🧠 Experiencia de Usuario (UX)

Se han aplicado mejoras como:

- Uso de tarjetas visuales
- Espaciado adecuado
- Separación clara de secciones
- Uso de imágenes
- Efecto hover en tarjetas

---

## 🎨 Criterios de Diseño

- Simplicidad
- Consistencia
- Escalabilidad
- Estética moderna

---

## 🧪 Estado Actual

Actualmente el panel permite:

- Visualizar información del profesor
- Consultar asignaturas
- Ver datos relevantes
- Navegar por la aplicación

---

## 🔮 Líneas Futuras

- Implementar funcionalidad de "Ver aula"
- Conectar con backend (datos reales)
- Integración con Mattermost
- Gestión de contenidos por asignatura

---

## 📌 Nota final

El panel del profesor proporciona una base sólida, visual y escalable, preparada para evolucionar hacia un sistema completo de gestión educativa.
