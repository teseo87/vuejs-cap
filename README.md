# Repositorio vuejs-cap

Capacitación en Vue.js
Cooperativa de Software Libre Geneos

# Introducción pag01.html

En primer lugar la directiva html para incluir en nuestra página vue.js es:

```
<script src="https://unpkg.com/vue/dist/vue.js"></script>
```

Luego la forma de utilizarlo es la siguiente, dentro del html definimos un div por ejemplo app para delimitar el elemento del dom en el cual vue.js va a funcionar, en este caso el div app.

```html
<div id="app">
</div>
<h1>Vue.js no va a tener acceso a este nivel</h1>
```

Definimos en javascript una instancia de vue como un objeto

Indicamos dentro de que elemento del dom vue.js va a funcionar mediante la directiva el, en este caso el div app

```javascript
<script>
var app = new Vue({

  	el: '#app'
})
</script>
```

Para pasar los datos con los cuales va a poder trabajar vue usamos data que será un objeto. Por ejemplo si tenemos la varianle message, la definimos y la usamos en html mediante la sintaxis {{ message }}

```javascript
<script>
var app = new Vue({

  	el: '#app',
  	data: {
    	message: 'Hello Vue!'
  	}
})
</script>
```

```html
<div id="app">
	{{ message }}
</div>

<h1>Vue.js no va a tener acceso a este nivel</h1>
```

# Loops pag02.html

La directiva v-text nos permite realizar una asignación directa de contenidos

```html
<span v-text="'Intro: ' + message"></span>
```

Todo lo que haya dentro del tag span será ignorado, los mensajes complementarios se pueden poner como se muestran en la cadena ya que es código javascript lo que se ejecuta.

Otra opción más limpia

```html
<span>Intro: <span v-text="message"></span></span>
```

Si queremos hacer una vista condicional dependiendo de si la cadena message tiene contenido usamos la directiva v-show que se le asigna un valor true o false, en este caso usaremos message que en caso de ser vacío devuelve false y true si tiene al menos 1 letra.

```html
<span v-show="message">Intro: <span v-text="message"></span></span>
```

Si queremos hacerlo con mayor cantidad de letras podemos usar otro condicional.

```html
<span v-show="message.length > 2">Intro: <span v-text="message"></span></span>
```

Podemos usar tambien la directiva v-if que a diferencia de v-show (oculta el elemento) hace que desaparezca el elemento del DOM. La directiva v-if se puede usar en conjunto con v-else para el caso que no se cumpla la condición.

```html
<span v-if="message">Intro: <span v-text="'Con v-if' + message"></span></span>
<span v-else>Ingrese información en el campo</span>
```

Para trabajar con loops vamos a definir una lista de tareas como parte de data y la directiva v-for para recorrer el arreglo: v-for="todo in todos" lo que hace es recorre cada posición de el arreglo todos y la asigna a la variable todo.

```html
<div id="app">

  <ul class="list-group">
    <li class="list-group-item" v-for="todo in todos">{{ todo }}</li>
  </ul>

</div>
```

```javascript
<script type="text/javascript">

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hola !!',
    todos : ['Tarea 1', 'Tarea 2']
  }
});

</script>
```

Para solucionar el problema de la renderización con las dobles llaves podemos hacer

```html
<li class="list-group-item" v-for="todo in todos" v-text='todo'></li>
```

Tambien podemos hacer que cada tarea sea un objeto

```javascript
<script type="text/javascript">

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hola !!',
    todos : [
    {'titulo' : 'Tarea1'},
    {'titulo' : 'Tarea2'},
    {'titulo' : 'Tarea3'}
    ]
  }
});

</script>
```

Ahora deberemos modificar para mostrar accediendo al campo titulo del objeto.

```html
<div id="app">

  <ul class="list-group">
    <li class="list-group-item" v-for="todo in todos">{{ todo.titulo }}</li>
  </ul>

</div>
```

Tambien podemos usar v-text

```html
<div id="app">

  <ul class="list-group">
    <li class="list-group-item" v-for="todo in todos"><span v-text='todo.titulo'></span></li>
  </ul>

</div>
```

Podemos agregar más información al objeto tarea con el estado

```javascript
<script type="text/javascript">

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hola !!',
    
    todos : [
    {titulo : 'Tarea1', completed : true},
    {titulo : 'Tarea2', completed : false},
    {titulo : 'Tarea3', completed : true}
    ]

  }
});

</script>
```

Y reflejarlo accediendo a la nueva variable de estado

```html
<ul class="list-group">
<li class="list-group-item" v-for="todo in todos">
  <span v-text='todo.titulo'></span>
  <small v-if='todo.completed'>Completa</small>
  <small v-else>Incompleta</small>
</li>
</ul>
```
# Eventos pag03.html

La directiva v-on nos permite capturar eventos por ejemplo relacionados a un botón y ejecutar un código javascript.

```html
<span>Mensaje: <span v-text="message"></span> <button v-on:click="message = message.length">Msj Length</button></span>
```
Tambien puede usarse una versió abreviada utilizandop el @ en lugar del v-on

```html
<span>Mensaje: <span v-text="message"></span> <button @click="message = message.length">Msj Length</button></span>
```
Para agregar funciones y poder sacar ese código del html, podemos usar la directiva methods dentro del objeto de vue.js, que a la ves va a ser un objeto que permite definir los métodos necesarios.

```javascript
<script type="text/javascript">

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hola !!',
    
    // todos : ['Tarea 1', 'Tarea 2']

    // todos : [
    // {titulo : 'Tarea1'},
    // {titulo : 'Tarea2'},
    // {titulo : 'Tarea3'}
    // ]
    
    todos : [
    {titulo : 'Tarea1', completed : true},
    {titulo : 'Tarea2', completed : false},
    {titulo : 'Tarea3', completed : true}
    ]

  },
  methods : {
    contar: function () {
      this.message = this.message.length;
    }
  }
});

</script>
```

Luego la forma de invocarlo en el html será:

```html
<span>Mensaje: <span v-text="message"></span> <button @click="contar">Msj Length</button></span>
```
Podemos en base a esta manipulación de eventos, agregar botones para el cambio de estados de las tareas:

```html
<ul class="list-group">
    <li class="list-group-item" v-for="todo in todos">
      <!-- {{ todo }} -->
      <!-- {{ todo.titulo }} -->
      <span v-text='todo.titulo'></span>
      <small v-if='todo.completed'>Completa</small>
      <small v-else>Incompleta</small>
      <span style="float:right;">
      <button type="button" class="btn btn-warning" @click="todo.completed = false" v-if="todo.completed">Revertir</button>
      <button type="button" class="btn btn-success" @click="todo.completed = true" v-else>Completar</button>
      </span>
    </li>
  </ul>
```

# Propiedades calculadas pag04-2.html

Permiten optimizar el llanmado a funciones, de modo que se guarda el resultado de la función en memoria y no se ejecutan nuevamente, hasta tanto no exista un cambio en algun elemento.

Se definen en la sección computed del objeto vue:

```javascript
<script type="text/javascript">

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hola !!',
    
    // todos : ['Tarea 1', 'Tarea 2']

    // todos : [
    // {titulo : 'Tarea1'},
    // {titulo : 'Tarea2'},
    // {titulo : 'Tarea3'}
    // ]
    
    todos : [
    {titulo : 'Tarea1', completed : true},
    {titulo : 'Tarea2', completed : false},
    {titulo : 'Tarea3', completed : true}
    ]

  },

  methods : {
    contar: function () {
      this.message = this.message.length;
    },
    contarCompletas1: function () {
      return this.todos.filter(function(todo) {return todo.completed;}).length;
    },
    contarIncompletas1: function () {
      return this.todos.filter(function(todo) {return ! todo.completed;}).length;
    }
  },

  computed : {

    contarCompletas: function () {
      console.log("contarCompletas");
      return this.todos.filter(function(todo) {return todo.completed;}).length;
    },
    contarIncompletas: function () {
      console.log("contarIncompletas");
      return this.todos.filter(function(todo) {return ! todo.completed;}).length;
    }


  }

});

</script>
```
Luego se invoca como una propiedad y no una función

```html
<h3>Lista de Tareas</h3>
<h3>Tareas completas: <span v-text="contarCompletas"></span></h3>
<h3>Tareas incompletas: <span v-text="contarIncompletas"></span></h3>
<br>
```