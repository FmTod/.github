# Javascript

## **NO USAR JQUERY**

## Estilo de código

[Prettier](https://prettier.io) determina nuestro estilo de código. Si bien la salida de Prettier no siempre es la más bonita, es consistente y elimina toda discusión (sin sentido) sobre el estilo de código.

Intentamos seguir los valores predeterminados de Prettier, pero tenemos algunas anulaciones para mantener nuestro estilo de código JavaScript consistente con PHP.

Las primeras dos reglas están configuradas realmente con `.editorconfig`. Usamos 4 espacios como sangría.

```txt
indent_size = 4
```

Dado que usamos 4 espacios en lugar de los 2 predeterminados, la longitud de línea predeterminada de 80 caracteres puede ser un poco corta (especialmente al escribir plantillas en JSX).

```json
{
    "printWidth": 120
}
```

Finalmente, preferimos comillas simples sobre comillas dobles para consistencia con PHP.

```json
{
    "singleQuote": true
}
```

## Asignación de variables

Preferir `const` sobre `let`. Solo usar `let` para indicar que una variable será reasignada. Nunca usar `var`.

```js
// Bueno
const person = { name: 'Sebastian' };
person.name = 'Seb';

// Malo, la variable nunca fue reasignada
let person = { name: 'Sebastian' };
person.name = 'Seb';
```

## Nombres de variables

Los nombres de variables generalmente no deben ser abreviados.

```js
// Bueno
function saveUser(user) {
    localStorage.set('user', user);
}

// Malo, es difícil razonar sobre abreviaturas en bloques a medida que crecen.
function saveUser(u) {
    localStorage.set('user', u);
}
```

En funciones de flecha de una sola línea, se permiten abreviaturas para reducir el ruido si el contexto es lo suficientemente claro. Por ejemplo, si estás llamando a `map` o `forEach` en una colección de elementos, está claro que el parámetro es un elemento de un cierto tipo, lo cual se puede deducir del nombre sustantivo de la colección.

```js
// Bueno
function saveUserSessions(userSessions) {
    userSessions.forEach(s => saveUserSession(s));
}

// Aceptable, pero bastante ruidoso.
function saveUserSessions(userSessions) {
    userSessions.forEach(userSession => saveUserSession(userSession));
}
```

## Comparaciones

Siempre usar un triple igual para comparaciones de variables. Si no estás seguro del tipo, cámbialo primero.

```js
// Bueno
const one = 1;
const another = "1";

if (one === parseInt(another)) {
    // ...
}

// Malo
const one = 1;
const another = "1";

if (one == another) {
    // ...
}
```

## Palabra clave de función vs. funciones de flecha

Las declaraciones de funciones deben usar la palabra clave de función.

```js
// Bueno
function scrollTo(offset) {
    // ...
}

// Usar una función de flecha no proporciona beneficios aquí, mientras que la
// palabra clave `function` hace que sea inmediatamente claro que esto es una función.
const scrollTo = (offset) => {
    // ...
};
```

Las funciones breves y de una sola línea también pueden usar la sintaxis de flecha. No hay una regla estricta aquí.

```js
// Bueno
function sum(a, b) {
    return a + b;
}

// Es un método corto y simple, por lo que aplastarlo en una sola línea está bien.
const sum = (a, b) => a + b;
```

```js
// Bueno
export function query(selector) {
    return document.querySelector(selector);
}

// Este es un poco más largo, tener todo en una línea se siente un poco pesado.
// No es fácilmente escaneable a diferencia del ejemplo anterior.
export const query = (selector) => document.querySelector(selector);
```

Las funciones de orden superior pueden usar funciones de flecha si mejora la legibilidad.

```js
function sum(a, b) {
    return a + b;
}

// Bueno
const adder = (a) => (b) => sum(a, b);

// Aceptable, pero innecesariamente ruidoso.
function adder(a) {
    return function (b) {
        return sum(a, b);
    };
}
```

Las funciones anónimas deben usar funciones de flecha.

```js
['a', 'b'].map((a) => a.toUpperCase());
```

A menos que necesiten acceder a `this`.

```js
$('a').on('click', function () {
    window.location = $(this).attr('href');
});
```

Intenta mantener tus funciones puras y limitar el uso de la palabra clave `this`.

Los métodos de objeto deben usar la sintaxis de método abreviado.

```js
// Bueno
export default {
    methods: {
        handleClick(event) {
            event.preventDefault();
        },
    },
};

// Malo, la palabra clave `function` no sirve para nada.
export default {
    methods: {
        handleClick: function (event) {
            event.preventDefault();
        },
    },
};
```

## Desestructuración de objetos y matrices

La desestructuración es preferible sobre asignar variables a las claves correspondientes.

```js
// Bueno
const [hours, minutes] = '12:00'.split(':');

// Malo, innecesariamente verbose y requiere una asignación adicional en este caso.
const time = '12:00'.split(':');
const hours = time[0];
const minutes = time[1];
```

La desestructuración es muy valiosa para pasar objetos tipo configuración.

```js
function uploader({
    element,
    url,
    multiple = false,
    beforeUpload = noop,
    afterUpload = noop,
}) {
    // ...
}
```
