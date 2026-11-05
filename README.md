# Practica inicial de React: Testimonios con componentes y estado

Ingenieria de Software · Unidad 3 · Periodo AGO–DIC 2026
TecNM en Celaya

## Integrantes

- Uriel Flores Zarate
- Jose Manuel Ramos Iglesias

## Entorno de desarrollo

- Node.js: v24.11.1
- npm: 11.6.2
- Vite: 8.3.5
- React: 19.3.1

## Scripts disponibles

- `npm install`: Instala las dependencias del proyecto.
- `npm run dev`: Inicia el servidor de desarrollo local.
- `npm run build`: Genera la compilacion de produccion en dist/.
- `npm run preview`: Previsualiza localmente la compilacion.
- `npm run lint`: Ejecuta el analisis estatico con oxlint.

## Registro de avance

### Seccion 1 a 4: Entorno e inicializacion con Vite

- Driver: Uriel Flores Zarate
- Navigator: Jose Manuel Ramos Iglesias
- Acciones:
  - Verificacion de versiones de Node.js (v24.11.1) y npm (11.6.2).
  - Creacion del proyecto con plantilla React de Vite.
  - Instalacion de dependencias y verificacion de compilacion inicial con `npm run build`.

### Seccion 5: Estructura y recorrido de la aplicacion

- Driver: Uriel Flores Zarate
- Navigator: Jose Manuel Ramos Iglesias
- Acciones:
  - Se estructuro el arbol de directorios segun el esquema de la practica (Figura 1), separando los componentes en `src/components/` y centralizando los estilos globales en `src/styles.css`.
  - Se configuro `public/fotos/` con 8 retratos en formato cuadrado (200x200 px con enfoque facial) para disponer de recursos locales sin depender de conectividad externa ni proveedores remotos.
  - Se prepararon los cascarones iniciales para `Testimonial.jsx`, `Controls.jsx` y el modulo `data.js`.
  - Se unifico el punto de entrada en `src/main.jsx`, encargandose de montar `App` dentro del nodo contenedor `#root` e importar `styles.css` una sola vez.

![Estructura de la aplicacion](docs/evidencias/Seccion_5.png)

## Preguntas de la practica

### Seccion 3: Comprobacion previa (JavaScript)

- **Diferencia entre un objeto y un arreglo de objetos**: Un objeto describe una sola entidad mediante propiedades clave-valor (por ejemplo, `{ id, nombre, cargo }`). Un arreglo de objetos es una coleccion ordenada que permite almacenar, iterar y acceder a multiples entidades.
- **Exportacion e importacion de data.js**: `export default testimonios` exporta el arreglo como el valor principal por defecto del modulo. Quien lo importa (`import testimonios from './data.js'`) recibe directamente la referencia sin necesidad de desestructuracion `{}`.
- **Uso de llaves en JSX (`{nombre}`)**: Las llaves indican a React que debe evaluar el contenido como una expresion dinamica de JavaScript, insertando su valor resultante en el arbol en lugar de tratarlo como texto literal.
- **Prediccion al pasar otro nombre al componente**: Al recibir nuevas props, React reejecuta la funcion del componente y concilia las diferencias en el DOM, actualizando unicamente el nodo de texto correspondiente.
