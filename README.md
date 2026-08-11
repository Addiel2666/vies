# Proyecto Vue.js - Formulario de Contacto

Proyecto simple de Vue.js 3 con Vite que implementa un formulario de contacto con validación básica.

## Características

- **Framework**: Vue.js 3
- **Build Tool**: Vite
- **Componentes**: 
  - Componente Form reutilizable con campos para nombre, email y mensaje
  - Validación de campos requeridos
  - Mensaje de éxito después del envío
  - Estilos modernos y responsivos

## Instalación

```bash
npm install
```

## Desarrollo

Para iniciar el servidor de desarrollo:

```bash
npm run dev
```

El servidor estará disponible en [http://localhost:5173/](http://localhost:5173/)

## Build

Para compilar el proyecto para producción:

```bash
npm run build
```

Los archivos compilados se guardarán en la carpeta `dist/`.

## Preview

Para ver una vista previa del build de producción:

```bash
npm run preview
```

## Estructura del Proyecto

```
├── src/
│   ├── components/
│   │   ├── Form.vue          # Componente de formulario
│   │   └── HelloWorld.vue    # Componente original (opcional)
│   ├── App.vue               # Componente principal
│   ├── main.js               # Punto de entrada
│   └── style.css             # Estilos globales
├── public/
│   └── favicon.svg
├── index.html
├── package.json
└── vite.config.js
```

## Uso del Formulario

El componente `Form.vue` incluye:

- Campo de **Nombre** (texto requerido)
- Campo de **Email** (email requerido)
- Campo de **Mensaje** (textarea requerido)
- Botón **Enviar** con validación
- Mensaje de confirmación tras envío exitoso

El formulario se reinicia automáticamente 2 segundos después del envío.

## Tecnologías

- [Vue 3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- JavaScript
- CSS3

## Notas de Desarrollo

Este proyecto utiliza la sintaxis `<script setup>` de Vue 3 para componentes más concisos y legibles.

Para más información sobre Vue 3, consulta la [documentación oficial](https://vuejs.org/guide/introduction.html).

