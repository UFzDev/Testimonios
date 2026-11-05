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

#### Preguntas de comprobacion previa

- **Diferencia entre un objeto y un arreglo de objetos**: Un objeto describe una sola entidad mediante propiedades clave-valor (por ejemplo, `{ id, nombre, cargo }`). Un arreglo de objetos es una coleccion ordenada que permite almacenar, iterar y acceder a multiples entidades.
- **Exportacion e importacion de data.js**: `export default testimonios` exporta el arreglo como el valor principal por defecto del modulo. Quien lo importa (`import testimonios from './data.js'`) recibe directamente la referencia sin necesidad de desestructuracion `{}`.
- **Uso de llaves en JSX (`{nombre}`)**: Las llaves indican a React que debe evaluar el contenido como una expresion dinamica de JavaScript, insertando su valor resultante en el arbol en lugar de tratarlo como texto literal.
- **Prediccion al pasar otro nombre al componente**: Al recibir nuevas props, React reejecuta la funcion del componente y concilia las diferencias en el DOM, actualizando unicamente el nodo de texto correspondiente.

### Seccion 5: Estructura y recorrido de la aplicacion

- Driver: Uriel Flores Zarate
- Navigator: Jose Manuel Ramos Iglesias
- Acciones:
  - Se estructuro el arbol de directorios segun el esquema de la guia (Figura 1), separando los componentes en `src/components/` y centralizando los estilos globales en `src/styles.css`.
  - Se configuro `public/fotos/` con 8 retratos en formato cuadrado (200x200 px con enfoque facial) para disponer de recursos locales sin depender de conectividad externa ni proveedores remotos.
  - Se prepararon los cascarones iniciales para `Testimonial.jsx`, `Controls.jsx` y el modulo `data.js`.
  - Se unifico el punto de entrada en `src/main.jsx`, encargandose de montar `App` dentro del nodo contenedor `#root` e importar `styles.css` una sola vez.

![Estructura de la aplicacion](docs/evidencias/Seccion_5.png)

### Seccion 6: Datos y componente de presentacion

- Driver: Uriel Flores Zarate
- Navigator: Jose Manuel Ramos Iglesias
- Acciones:
  - Se definio el modulo `src/data.js` como un modulo nativo de JavaScript (`export default`) que contiene un arreglo con 8 objetos estructurados, vinculando cada registro a su respectiva imagen local en `/fotos/`:

```javascript
const testimonios = [
  {
    id: 1,
    nombre: "Ana Pérez",
    cargo: "Dirección",
    texto: "La herramienta facilita organizar nuestras tareas.",
    foto: "/fotos/ana.jpg",
  },
  // ... 7 registros adicionales con id unico del 2 al 8
];

export default testimonios;
```

- Se construyo el componente de presentacion `src/components/Testimonial.jsx`, el cual recibe el testimonio individual a traves de la prop `item`. Aplica desestructuracion limpia y genera marcado semantico accesible con texto alternativo contextual:

```jsx
export default function Testimonial({ item }) {
  if (!item) return null;

  const { nombre, cargo, texto, foto } = item;

  return (
    <article className="testimonial-card">
      <img
        className="testimonial-photo"
        src={foto}
        alt={`Retrato ilustrativo de ${nombre}`}
        width="90"
        height="90"
      />
      <h2>{nombre}</h2>
      <p className="testimonial-role">{cargo}</p>
      <blockquote>{texto}</blockquote>
    </article>
  );
}
```

### Seccion 7: Montaje y primera tarjeta estatica

- Driver: Uriel Flores Zarate
- Navigator: Jose Manuel Ramos Iglesias
- Acciones:
  - Se implemento la primera version de `src/App.jsx` montando de forma estatica el primer elemento del arreglo (`testimonios[0]`):

```jsx
import testimonios from "./data.js";
import Testimonial from "./components/Testimonial.jsx";

export default function App() {
  return (
    <main className="app">
      <h1>Experiencias de nuestros usuarios</h1>
      <Testimonial item={testimonios[0]} />
    </main>
  );
}
```

- Se comprobo el funcionamiento del renderizado estatico y el flujo unidireccional de datos pasando inicialmente `testimonios[0]` (Ana Perez) y posteriormente intercambiando el indice por `testimonios[1]` (Luis Garcia) para verificar la reactividad ante el cambio de props.

![Testimonio en posicion 0](docs/evidencias/Seccion_7.1.png)
![Testimonio en posicion 1](docs/evidencias/Seccion_7.2.png)

#### Detente y explica

- **¿Que archivo contiene la tarjeta y cual el objeto mostrado?**:
  `src/components/Testimonial.jsx` contiene la estructura visual y de marcado de la tarjeta, mientras que `src/data.js` almacena los objetos de datos estructurados que son leidos por `src/App.jsx`.
- **¿Que recibe `item` y por que el hijo no necesita importar `data.js`?**:
  `item` recibe como propiedad (_prop_) un unico objeto testimonio individual entregado por el componente padre (`App`). El componente hijo no necesita importar `data.js` porque su unica responsabilidad es presentar los datos que le son inyectados desde el exterior, desacoplandose del origen de la fuente de datos.
- **¿Que diferencia hay entre `main.jsx` y `App.jsx`?**:
  `src/main.jsx` es el punto de entrada de la aplicacion que conecta React con el DOM del navegador mediante `createRoot` sobre el elemento `#root`. `src/App.jsx` es el componente raiz de la jerarquia de React que define la logica, la estructura general y la coordinacion de los componentes visuales.
- **¿Que tendrias que copiar si no existiera el componente `Testimonial`?**:
  Habria que duplicar manualmente en cada lugar todo el bloque de marcado JSX (`<article>`, `<img>`, `<h2>`, `<p>`, `<blockquote>`) y las operaciones de acceso a las propiedades del objeto, dificultando el mantenimiento y aumentando la redundancia del codigo.
