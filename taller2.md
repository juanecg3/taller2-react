# Taller 2 Segundo corte: React

**Estudiante:** Juan Eduardo Caicedo Gómez  
**Asignatura:** Desarrollo Front-end
**Fecha:** 16 de octubre de 2026



## Punto 1 · ¿Qué es React?

React es una biblioteca de JavaScript que sirve para construir interfaces de usuario. La idea principal es que una pantalla se divide en piezas pequeñas llamadas componentes, y esas piezas se vuelven a actualizar cuando cambian los datos o cuando la persona hace algo en la página. Se usa sobre todo en páginas web interactivas, aunque con React Native las mismas ideas también se pueden llevar a aplicaciones nativas. [1]

React lo creó Jordan Walke, que era ingeniero de Facebook, hoy Meta. Se publicó como proyecto de código abierto el 29 de mayo de 2013, y esa fecha aparece en el historial oficial de versiones de React. Además, la página de reconocimientos de React identifica a Walke como su creador. [7–8]

Sobre si es una librería o un framework, React es una **biblioteca**. Una biblioteca da herramientas para resolver una parte concreta, que en este caso es la interfaz, y es el programa el que decide cuándo y cómo usarlas. Un framework, en cambio, normalmente trae una estructura más grande y unas reglas para organizar toda la aplicación. React solo se encarga de la parte de la interfaz, entonces para cosas como las rutas, la carga de datos o el renderizado en el servidor hay que agregar otras bibliotecas o usar un framework hecho sobre React, como Next.js. Hoy en día a veces se dice "framework de React" de forma informal, pero React por sí solo es una biblioteca para la interfaz. [1, 12]

Que React sea **declarativo** quiere decir que uno describe cómo debería verse la pantalla con los datos que hay en ese momento, y no cada paso para lograrlo. Por ejemplo, si la variable `abierto` vale `true`, se muestra un panel, y si vale `false`, no se muestra. React se encarga de calcular y aplicar los cambios necesarios. De esta manera quien programa expresa el resultado que quiere, en vez de ordenar una por una las instrucciones para modificar la página. [6]

## Punto 2 · ¿Qué problema resuelve React?

Cuando una interfaz se construye directamente con JavaScript y el DOM, el código tiene que buscar los elementos, cambiar textos o atributos, agregar y quitar nodos, y además mantener todo al día después de cada acción del usuario. Si hay muchas interacciones y muchos datos, esas instrucciones se van quedando regadas por todo el código y es fácil olvidarse de actualizar alguna zona, mostrar información vieja o terminar con estados visuales que se contradicen. Esa es la dificultad principal de hacerlo "a mano". [6]

La diferencia entre los dos enfoques es que en el **imperativo** se escriben los pasos concretos, por ejemplo "busca el botón, desactívalo, crea un mensaje y agrégalo al documento". En el **declarativo**, por el contrario, se expresa la condición y el aspecto esperado, por ejemplo "si el envío terminó, muestra el mensaje de éxito, y si todavía se está enviando, muestra el indicador de carga".

React mantiene la interfaz sincronizada porque relaciona lo que muestra cada componente con sus entradas, que son las props y el estado. Cuando el estado cambia a través de su función de actualización, React vuelve a calcular lo que debe mostrar el componente y actualiza el DOM para que quede igual. Es importante no modificar el estado directamente, sino pedir el cambio y dejar que React dibuje una interfaz coherente con el nuevo valor. [4, 6]

Los componentes reutilizables también ayudan bastante a resolver este problema, porque permiten dividir una pantalla en unidades con una responsabilidad clara, como `Boton`, `CampoTexto` o `TarjetaProducto`. Cada pieza recibe sus datos por medio de props y guarda el estado que le corresponde. Al reutilizar la misma pieza se repite menos código, y si hay que corregir o cambiar un comportamiento se hace en un solo lugar. [1, 3]

## Punto 3 · Principales componentes de React

### 3.1 Componentes

**Definición.** Un componente es una pieza de la interfaz que tiene nombre y que se puede combinar con otras piezas. En React moderno se crea normalmente como una función de JavaScript que devuelve JSX.

**Características principales.** El nombre del componente empieza con mayúscula, recibe información mediante props, puede tener su propio estado y puede contener otros componentes. También conviene que solo se encargue de describir la interfaz, sin modificar datos externos mientras se está renderizando. [1]

**Ejemplo.**

```jsx
function Saludo({ nombre }) {
  return <h2>Hola, {nombre}</h2>;
}

function App() {
  return <Saludo nombre="Lucía" />;
}
```

En este código `Saludo` es una función de componente. `App` la usa y le pasa el valor `Lucía`, entonces React muestra en pantalla "Hola, Lucía".

### 3.2 JSX

**Definición.** JSX es una sintaxis que deja escribir marcado parecido a HTML dentro del código de JavaScript. No es HTML pegado tal cual, sino que las herramientas del proyecto lo transforman en instrucciones que React sí puede interpretar.

**Características principales.** Las expresiones de JavaScript se escriben entre llaves. En general, un fragmento debe tener un solo elemento raíz, o también se puede usar la etiqueta vacía `<>...</>`. Las etiquetas que no tienen contenido se cierran, por ejemplo `<img />`. Los nombres de las propiedades siguen las convenciones de JavaScript, por eso se escribe `className` en lugar de `class`, y los atributos y manejadores van en camelCase, como `onClick`. [2]

**Ejemplo.**

```jsx
const nombre = 'Lucía';
const saludo = <p className="saludo">Hola, {nombre}</p>;
```

Aquí el valor de la variable se inserta dentro del párrafo, y `className` sirve para asignarle la clase de CSS.

### 3.3 Props

**Definición.** Las props, o propiedades, son los datos que un componente padre le entrega a un componente hijo. Funcionan parecido a los argumentos de una función y permiten configurar componentes que se pueden reutilizar.

**Características principales.** Pueden contener textos, números, objetos, listas o incluso funciones. El componente hijo las recibe y las usa para decidir qué va a representar. Algo importante es que el hijo debe tratarlas como datos de entrada y no modificarlas. [3]

**Ejemplo.**

```jsx
function Producto({ nombre, precio }) {
  return <p>{nombre}: ${precio}</p>;
}

<Producto nombre="Cuaderno" precio={12000} />
```

El componente muestra el nombre y el precio que le llegan. Las llaves en `precio={12000}` permiten pasar un número como valor de JavaScript.

### 3.4 Estado con `useState`

**Definición.** El estado es la información que un componente recuerda entre un renderizado y otro y que puede cambiar mientras se usa la aplicación, como la cantidad de artículos de un carrito o si un menú está abierto o cerrado. `useState` es el Hook que permite declarar ese valor dentro de un componente de función.

**Características principales.** Se importa desde `react` y devuelve el valor actual junto con una función para pedir que se actualice. Cuando se llama esa función, React vuelve a renderizar el componente con el valor nuevo, por eso no se cambia la variable directamente. Además, los Hooks se llaman en el nivel superior del componente y no dentro de condiciones o ciclos. [4]

**Ejemplo.**

```jsx
import { useState } from 'react';

function Contador() {
  const [cantidad, setCantidad] = useState(0);

  return (
    <button onClick={() => setCantidad(cantidad + 1)}>
      Clics: {cantidad}
    </button>
  );
}
```

La variable `cantidad` empieza en cero. Cada vez que se hace clic se pide guardar el valor siguiente, y React vuelve a renderizar el botón mostrando el contador ya actualizado.

### 3.5 Eventos

**Definición.** Los eventos son las respuestas a las acciones que hace el usuario, como dar un clic, escribir en un campo o enviar un formulario. React permite asociar funciones a los elementos con propiedades como `onClick` y `onChange`.

**Características principales.** El nombre del evento se escribe en camelCase y lo que se le pasa es una función, que se ejecuta cuando ocurre la acción. `onChange` se usa mucho en los campos de formulario. Un evento puede actualizar el estado y, por lo tanto, cambiar el contenido que se muestra. [5]

**Ejemplo.**

```jsx
import { useState } from 'react';

function CampoNombre() {
  const [nombre, setNombre] = useState('');

  return (
    <label>
      Nombre:
      <input
        value={nombre}
        onChange={(evento) => setNombre(evento.target.value)}
      />
      <p>Escribiste: {nombre}</p>
    </label>
  );
}
```

En este caso `onChange` lee el texto que hay en el campo y lo guarda en el estado. Cuando ese valor cambia, React actualiza el párrafo. Como el `value` está unido al estado, el campo siempre refleja lo que React tiene guardado.

## Punto 4 · Importancia de React en la industria

Muchas empresas escogen React porque permite organizar interfaces grandes como componentes que se pueden combinar y reutilizar. Su forma declarativa de trabajar y el manejo del estado ayudan a construir productos con pantallas dinámicas y muchas interacciones. También se puede integrar poco a poco en una aplicación que ya existe, según lo que necesite el equipo. Como muestra de que se usa a gran escala, Meta informó en 2025 que React y React Native impulsaban más de 50 millones de sitios y productos, incluyendo los de Microsoft, Shopify, Bloomberg, Discord, Coinbase y la NFL. [10]

React tiene un ecosistema muy amplio a su alrededor. React Developer Tools ayuda a inspeccionar los componentes, Vite y otros empaquetadores preparan el código para el navegador, bibliotecas como React Router se encargan de la navegación, y frameworks como Next.js agregan reglas para las rutas y el renderizado en el servidor. Todo esto hace que no haya que armar desde cero cada parte común de una aplicación. [13–15]

Por otro lado, React nació en Meta y hoy su desarrollo lo hace un equipo dedicado junto con aportes de personas y empresas de distintos lugares. En octubre de 2025 Meta anunció la React Foundation como el nuevo hogar institucional de React y React Native, y también una transición hacia una gobernanza técnica independiente liderada por mantenedores y colaboradores. Meta dijo que iba a seguir financiando el proyecto y asignando ingenieros. Esto muestra que el mantenimiento depende tanto del equipo de Meta como de una comunidad abierta más grande. [8, 10]

Para alguien que se está formando como desarrollador front-end, React es relevante porque se usa en productos reales y saberlo permite construir interfaces por componentes, entender el flujo de los datos y trabajar con un ecosistema que usan muchas empresas. Según la información de la Linux Foundation que recoge IT Brief, React lo utilizan más de 20 millones de desarrolladores en el mundo, lo que da una idea de qué tan extendida está esta habilidad. [16] Aprenderlo también ayuda a reforzar JavaScript, los eventos, el estado y el diseño de interfaces, pero no reemplaza los fundamentos como HTML, CSS, la accesibilidad o la plataforma web. [10]

## Punto 5 · Empresas que utilizan React

### Meta (Facebook.com)

Meta usa React en Facebook.com. En su artículo de ingeniería sobre la reconstrucción del sitio, la empresa explica que Facebook.com es una aplicación del lado del cliente hecha con React y Relay. Es un caso relevante porque React se creó en Meta para resolver necesidades de interfaz a gran escala, y usarlo en su propio producto dio experiencia y mejoras que después se compartieron con la comunidad. [9]

### Netflix (interfaz de TV)

Netflix Engineering publicó un artículo sobre cómo construyó una interfaz de usuario para televisores con React. El equipo cuenta que escogió React por su flujo de datos en una sola dirección y por su enfoque declarativo, porque eso facilitaba razonar sobre la aplicación. Es un caso relevante ya que muestra React aplicado a una interfaz de streaming pensada para televisores, donde el rendimiento y la navegación con control remoto son muy importantes. [11]



## Fuentes consultadas

1. React, [Tu primer componente](https://react.dev/learn/your-first-component), definición y creación de componentes.
2. React, [Escribir marcado con JSX](https://react.dev/learn/writing-markup-with-jsx), qué es JSX y cómo se usa.
3. React, [Pasar props a un componente](https://react.dev/learn/passing-props-to-a-component), props y comunicación entre componentes.
4. React, [useState](https://react.dev/reference/react/useState), estado en componentes de función.
5. React, [Responder a eventos](https://react.dev/learn/responding-to-events), eventos y manejadores.
6. React, [Reaccionar a la entrada con estado](https://react.dev/learn/reacting-to-input-with-state), enfoque declarativo e imperativo.
7. React, [Versiones](https://react.dev/versions), React se hizo público el 29 de mayo de 2013.
8. React, [Agradecimientos](https://react.dev/community/acknowledgements), Jordan Walke y aportes de la comunidad.
9. Meta Engineering, [Reconstrucción del stack tecnológico de Facebook.com](https://engineering.fb.com/2020/05/08/web/facebook-redesign/), uso de React y Relay en Facebook.com.
10. Meta Engineering, [Presentamos la React Foundation](https://engineering.fb.com/2025/10/07/open-source/introducing-the-react-foundation-the-new-home-for-react-react-native/), transición institucional y mantenimiento del proyecto.
11. Netflix Technology Blog, [Creación de una interfaz de TV de alto rendimiento con React](https://medium.com/netflix-techblog/crafting-a-high-performance-tv-user-interface-using-react-3350e5a6ad3b), caso de uso de React en la interfaz para televisores.
12. MDN Web Docs, [Introducción a React](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Frameworks_libraries/React_getting_started), contexto de React como biblioteca de interfaz.
13. React, [Crear una aplicación React](https://react.dev/learn/creating-a-react-app), recomienda frameworks para aplicaciones completas.
14. React, [React Developer Tools](https://react.dev/learn/react-developer-tools), herramientas para inspeccionar y depurar componentes.
15. Vite, [Guía](https://vite.dev/guide/), herramienta de desarrollo y construcción para proyectos web.
16. IT Brief, [Linux Foundation to form React Foundation for open governance](https://itbrief.co.uk/story/linux-foundation-to-form-react-foundation-for-open-governance), cantidad de desarrolladores que usan React.
