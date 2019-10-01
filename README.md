# javaScript (básico)
## Variables:
JS es debilmente tipado. (weakly typed)

```javascript
const MAYORIA_EDAD = 18 // constante - Magic Number
```

### Strings
```javascript
var nombre = 'Carlos', apellido = 'Jaramillo'.toLowerCase();
var nombreConcatenado = `${nombre.toUpperCase()} ${apellido}`;

var nombreMayusculas = nombre.toUpperCase();
var apellidoMinusculas = apellido.toLowerCase();

var primeraLetraNombre = nombre.charAt(0);
var cantidadLetrasNombre = nombre.lenght; // attribute.

var nombreCompleto = nombre + '' + apellido;
var nombreCompletoST = `${nombre.toUpperCase()} ${apellido}` // StringTemplate or TemplateLiterals.

var str = nombre.substr(1,2); // (posicion inicial, cantidad de chars).
```

### Números
```javascript
var edad = 27;

edad = edad + 1;
edad += 1;

var precio = 200.3 * 3;
// No da exacto, porque la manera de guardar decimales de JS no es muy precisa.
// Porque destina una cantidad de bytes en la ram, para asignarle un decimal.
var precioFixed = 200.3 * 100 * 3 / 100; // Solo funciona con 1 decimal.
var priceFixed = Math.round(200.3 * 100 * 3) / 100; // es un poco más exacta.

var totalStr = priceFixed.toFixed(3); // Convertir a string y cantidad de decimales.
var totalNum = parseFloat(totalStr); // Convertir a número float.
```
    
## Funciones
Son pedazos de código reutilizables.
Se le pueden pasar parametros por referencia o valor y son opcionales.
    
```javascript
function nombreFuncion(parametrosRecibidos) {
    // cuerpo función.
    return // Valor retornado por la función
}
```
Se puede asignar a una variable, una función.
Si una función no tiene nombre, es anonima.

```javascript
var ó const  esMayorEdad = function (persona) {
    return persona.edad >= MAYORIA_EDAD
}

String.prototype.capitalize = function() {
    return this.charAt(0).toUpperCase() + this.slice(1).toLowerCase();
}
```
### Arrow Function 

se le quita la palabra function, y se agrega =>

Si solo recibe un parametro, podemos obviar los parentesis. (persona)
```javascript
const esMayorEdad = persona => { 
    return persona.edad >= MAYORIA_EDAD
}
```
Si una función solo retorna algo, podemos borrar el return y las { llaves }
```javascript
    const esMayorEdad = persona => persona.edad >= MAMAYORIA_EDAD
```
### Side Effect (daño colateral)
Cuando al ejecutar una función, ella modifica variables que no estan definidas dentro de ella.

```javascript
//Evitar Side Effect
function cumpleanos(persona) {
    // Retorna un objeto nuevo con la edad modificada 
    return {...persona, edad: persona.edad + 1}
    //(... Spread Operator) clona un objeto o array
}
```
   
### Alcance Funciones (Scopes) - Hoisting
- Las variables se envian por referencia a scopes descendientes predeterminadamente.

#### Hoisting
Declarar una variable, despues de usarla. - Las declaración de las variables declaradas con var, se (suben hasta el comienzo de la ejecución)

Todas las declaraciones (var, let, const, function, function*, class) son "hoisted"
Pero la diferencia entre las declaraciones

var **/** function **/** function* **(** undefined o generator **)**

y  let **/** const **/** class **(** temporal dead zone **)**

es la inicialización. Las segundas, solo se evaluan cuando son evaludas, mientras estan en una temporal dead zone

 
**Global Scope** (*var* o *let*) Estando fuera de una función/clase
```javascript    
a = 'xd'; // Global Scope (Default Scope)

var b; // Global Scope
b = 'xd'; 

var c = 'xd'; // Global Scope - Permite Hoisting 
let c = 'xd'; // Global Scope - No permite Hoisting
```
 **Local Scope** (*var* o *let*) Estando dentro de una función/clase
```javascript
function foo() {
    var d = 'lol'; // Local Scope
    var e = 'lol'; // Local Scope
}
```
- Se puede tener una variable global y una local con el mismo nombre y diferente valor
   
 **block scope** (*let* o *const*) *let* necesita estar dentro de un bloque *(if, while, for, loops, { }, etc)*
```javascript
if (true) {
    let i = 1; // Block Scope
}
console.log(i); // ReferenceError: i is not defined

const f = 'constante'; // No permite hoisting
```
- const crea una referencia inmutable, no variables inmutables
- las constantes no son reasignables, pero pueden ser mutables. 
    
 
 ## Objetos (JSON) - Destructuring
 Se declara con { claveKey: 'valorValue' } la clave puede ser un número o un string, el valor  puede ser una función, número, decimal, booleano, string..
 - Los Objetos que se pasen por parametro, se pasan por referencia (si los modificamos adentro de la función, se va ver afectado el objeto afuera también) - Side Effect
 
```javascript
var carlos = {
    nombre: 'Carlos',
    apellido: 'Jaramillo',
    edad: 22        
} 
    
function imprimirNombre(persona) {
    console.log(persona.nombre.toUpperCase());
}
imprimirNombre(carlos);

// Destructuring - solo se usa cuando siempre se envia
function imprimirNombre({ nombre }) { 
    console.log(nombre.toUpperCase());
}
imprimirNombre(carlos);
imprimirNombre({ nombre: 'Pepito' });

function imprimirNombre(persona) {
    // var nombre = persona.nombre;
    var { nombre } = persona; // Desestructurar Objetos
    console.log(nombre.toUpperCase());
}    
imprimirNombre(carlos);
``` 
## Comparaciones
Si comparara objetos fallaría porque compararía la posición en memoria.
#### Valores primitivos:
- 2 iguales (==) compara convirtiendo ambos valores a string  
- 3 iguales (===) compara tipo y valor

## Condicionales 
```javascript
if (condición) {
    código a ejecutar, si se cumple la función
} else {
    código a ejecutar, cuando no se cumple la función
}
```

## Ciclos (Estructuras repetitivas)
### For
```javascript
/* inicial; condición; incremento */
for (var i = 1; i <= 365; i++) {
    // código a repetir
}
```

### While
```javascript
// condición
while (persona.peso > META) {
    //  código a repetir, mientras se cumpla la condición
}
```
### Do While
```javascript
do {
    // Minimo se repite 1 vez, antes de verificar la condición
    // código a repetir, mientras se cumpla la condición
} while(persona.peso > Meta)
// condición
```

## Condicional múltiple: Switch
```javascript
switch(// variable a comparar){
    case 'case2':
        console.log('execute when case2');
        break;
    case 'caso1':
    case 'casoUno':
        console.log('execute when case1 or caseUno');
        break;
    default:
        break;
}
```

## Arrays o Arreglos
Estructura de datos, que nos permite agrupar dato, pueden ser números, strings, booleanos, objetos, etc. para realizar ciertas operaciónes sobre esa colección.

```javascript
// se declara con corchetes
var personas = [];

var numeros = [1, 2, 3, 4];
var vocales = ['a', 'e', 'i', 'o', 'u'];

// para acceder a una posición
vocales[1];

personas[0].altura;
personas[0]['altura'];
```

### Principales metodos de una array:
[Click aquí](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array)

### Filtrar elementos en un array (filter)
```javascript
const numeroPar = numero => numero % 2 === 0;

// la condición en filter debe ser una función
var numerosFiltrados = numeros.filter(numeroPar);
// retorna un nuevo array

// con función anonima
var numerosFiltrados = numeros.filter(function (numero) {
    return numero % 2 === 0;
});

```

### Transformar un array (map)
Itera sobre los elementos de un array, en el orden de inserción y retorna un array nuevo con los elementos modificados.
```javascript

const multiplicarPorDos = numero => numero * 2;
var numerosMultiplicados = numeros.map(multiplicarPorDos)

// también puede ser llamado con una función anonima
var numerosMultiplicados = numeros.map(function (numero) {
    return numero => numero * 2;
});

const pasarAlturaAcms = persona => {
    // personal.altura *= 100;
    // return persona;

    // retornar nuevo objeto, para no modificar la persona inicial
    return {
        ...persona,
        altura: persona.altura * 100
    }
}

// para retornar simplemente un objeto
const pasarAlturaAcms = persona => ({
    ...persona,
    altura: persona.altura * 100
})
```


### Reducir un array a un valor
```javascript
/*
var acum = 0
for (var i = 0; i < personas.length; i++) {
    acum = acum + personas[i].cantidadDeLibros
}
console.log(`En total todos tienen ${acum} libros`)
*/
// (una función, y el valor inicial del acumulador)

// acumulador y cada uno de los elementos elementos
const reducer = (acum, {cantidadDeLibros}) => acum + cantidadDeLibros;

var totalDeLibros = personas.reduce(reducer, 0)
```


## Prototipos (clases)
Javascript no soporta la herencia, porque no existen las clases. Existen los prototipos que son objetos que le vamos agregando metodos, que reciben funciones.

```javascript
function Persona(nombre, apellido, altura) {
    this.nombre = nombre;
    this.apellido = apellido;
    this.altura = altura;
    // return this; - está implicito.
}
// siempre en la parte superior, porque si se ejecutan antes de ser declaradas no existen.
// no pueden ser arrow functions, porque dentro de una arrow function this, this hace referencia a su padre.
Persona.prototype.saludar = function() {
    console.log(`Hola, Me llamo ${this.nombre}`);
}

var carlos = new Persona('Carlos', 'Jaramillo', 1.72)
```

### Herencia prototipal
Busca un metodo en si, si no lo encuentra lo busca en el prototipo padre, y así hacia arriba, hasta llegar al potrotipo base de todos los prototipos (obj) si no lo encuentra, aquí lanza el error.
```javascript
function Desarrollador(nombre, apellido) {
    this.nombre = nombre;
    this.apellido = apellido;
}

// Herencia antes de ECMA 2015
function heredaDe(prototipoHijo, prototipoPadre) {
    var fn = function () {}
    fn.prototype = prototipopadre.prototype;
    prototipoHijo.prototype = new fn;
    prototipoHijo.prototype.constructor = prototipoHijo;
}

Desarrollador.prototype.saludar = function () {
    console.log(`Hola, me llamo ${this.nombre} y soy dev.`)
}

```

### Clases (ECMA 2015)
```javascript
class Persona {
    constructor(nombre, apellido, altura) {
        this.nombre = nombre;
        this.apellido = apellido;
        this.altura = altura;
    }

    saludar(fn) {
        // var nombre = this.nombre;
        // var apellido = this.apellido;
        var {nombre, apellido} = this;
        console.log(`Hola, Me llamo ${nombre}`);
        if (fn) {
            fn(nombre, apellido, null)
        }
    }

    soyAlto() {
        return this.altura > 1.8;
    }
}

class Desarrollador extends Persona {
    constructor(nombre, apellido, altura) {
        // llamar constructor clase padre (necesario para usar this)
        super(nombre, apellido, altura);
        /*
        this.nombre = nombre;
        this.apellido = apellido;
        this.altura = altura;
        */
    }
    
    saludar(fn) {
        var {nombre, apellido} = this;
        console.log(`Hola, me llamo ${nombre} y soy dev!`);            
        if (fn) {
            fn(nombre, apellido, true)
        }
    }
}
```
## Enviar función como parametro
```javascript
function responderSaludo(nombre, apellido, esEstudiante){
  console.log(`buenas tardes ${nombre}${apellido}`)
  if(esEstudiante){
    console.log(`Ah, no sabie que eres estudiante.`)
  }
}

carlos.saludar(responderSaludo);
```

## Asincronismo
JavaScript sólo puede hacer una tarea a la vez (No es multi-tarea), sin embargo; es capaz de delegar la ejecución de ciertas funciones a otros procesos. Este modelo de concurrencia se llama **EventLoop**.

**Pila de ejecución** o **Call Stack**, se ponen las llamadas a funciones según el orden de ejecución del programa (se saca de la pila al terminar de ejecutar cada función)

**Callback**, una función que se ejecutará cuando regrese la respuesta del servidor.
Javascript sigue ejecutando el programa principal, y cuando llegue la respuesta la funcion a ejecutar va a parar a la **cola de tareas** (se encolan, segun orden de llegada) 
Aquí llegan: 
- las peticiones a servidores
- interacciones visuales
- navegación client-side
- eventos que se realizan cada cierto tiempo.

## Javascript ejecuta primero lo sincrono (pila de tareas), y posteriormente lo asincrono (cola de tareas).

```javascript
console.log('a');
// Envía la función a la cola de tareas, mientras sigue ejecutando el programa principal
setTimeout(() => console.log('b'), 0);
console.log('c');
// Cuando termina la ejecución del programa inicial, comienza a ejecutar las tareas de la cola de tareas
```

## Callbacks
Un callback es una función que se pasa a otra función como un argumento. Esta función se invoca, después, dentro de la función externa para completar alguna acción.

```javascript
const URL = 'https://swapi.co/api';
const PEOPLE_URL = '/people/:id';

const LUKE_URL = `${URL}${PEOPLE_URL.replace(':id',1)}`;

fetch(LUKE_URL)
.then((response)=>response.json())
.then((persona)=>{
    console.log(`Hola, yo soy ${persona.name}`)
})
.catch( error=> console.error('Error: ', error))

```


## Multiples request
Las respuestas en js no nos llegan en el mismo orden, por el asincronismo. A no ser que usemos callbacks

```javascript
const URL = 'https://swapi.co/api';
const PEOPLE_URL = '/people/:id';

const getPersona = (personaId, callback) => {
    const LUKE_URL = `${URL}${PEOPLE_URL.replace(':id',personaId)}`;
    fetch(LUKE_URL)
    .then((response)=>response.json())
    .then((persona)=>{
        console.log(`Hola, yo soy ${persona.name}`)
        if (callback) {
            callback();
        }
    })
    .catch( error=> console.error('Error: ', error))  // manejo de error en callback
};

/*
// No llegan en el mismo orden 

getPersona(1);
getPersona(2);
getPersona(3);
*/

// Callback Hell
getPersona(1, function () {
    getPersona(2, function () {
        getPersona(3);
    });
});

```

## Promesas
Anteriormente usabamos bluebird cuando no todos los browsers tenian soporte, ahora se pueden usar polyfills para browsers que no tengan esta clase creada aun.

Son valores que aun no conocemos, la promesa de que ahí habrá un valor cuando una acción asincrona/sincrona suceda y se resuelva. Son un obj de JS

```javascript
new Promise(function(resolve, reject){

}).then(valor => {
    // aquí se puede retornar otra promesa, para ir encadenandolas en acciones sucesivas asincronas
}).catch(err => {

});
```
#### Estados:
- Pending (Cuando se crea, inicializa)
- Fullfilled (resolve) (Cuando se resuelve, exitosamente)
```javascript
 .then(val => ..) // recibe una función
```
- Rejected (Error)
```javascript
.catch(err => ..)  // recibe una función
```

```javascript
const URL = 'https://swapi.co/api';
const PEOPLE_URL = '/people/:id';

const HEADERS = new Headers();
var miInit = { method: 'GET',
  headers: HEADERS,
   mode: 'cors',
  cache: 'default'
};

const getPersona = (personaId) => {
    const LUKE_URL = `${URL}${PEOPLE_URL.replace(':id',personaId)}`;
    // function(resolve, reject)
    return fetch(LUKE_URL, miInit)
        .then(response => response.json())
        .catch(error => console.log(`Error al obtener el personaje ${id}`)) 
};
```
### Promesas encadenadas
A diferencia de los callbacks que son anidados, las promesas son encadenadas.

```javascript
getPersona(1)
    .then(persona => {
        console.log(`Hola, yo soy ${persona.name}`)
        return getPersona(2)
    })
    .then(persona => {
        console.log(`Hola, yo soy ${persona.name}`)
        return getPersona(3)
    })
    .then(persona => {
        console.log(`Hola, yo soy ${persona.name}`)
    })
    .catch(`Error`);
```

### Multiples promesas en paralelo

```javascript
var ids = [1, 2, 3, 4, 5, 6,7];
var promesas = ids.map(id => getPersona(id));

Promise
    .all(promesas)
    .then(personajes => console.log(personajes))
    .catch(`Error`);
```


## Async-await
Se marca la función al inicio como **async**, se pone la parte asincrona en un try-catch y se le marca como await
```javascript
async function obtenerPersonajes() {
    var ids = [1, 2, 3, 4, 5, 6,7];
    var promesas = ids.map(id => getPersona(id));
    try {
        var personajes = await Promise.all(promesas);
        console.log(personajes)
    } catch (id) {
        console.log(`error in ${id}`);
    }
}

obtenerPersonajes();
```