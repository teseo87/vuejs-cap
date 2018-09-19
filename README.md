# Repositorio vuejs-cap
Capacitación en Vue.js
Cooperativa de Software Libre Geneos

# Introducción pag01.html

En primer lugar la directiva html para incluir en nuestra página vue.js es:

<script src="https://unpkg.com/vue/dist/vue.js"></script>

Luego la forma de utilizarlo es la siguiente, dentro del html definimos un div por ejemplo app para delimitar el elemento del dom en el cual vue.js va a funcionar, en este caso el div app.

<div id="app">
</div>
<h1>Vue.js no va a tener acceso a este nivel</h1>


Definimos en javascript una instancia de vue como un objeto

Indicamos dentro de que elemento del dom vue.js va a funcionar mediante la directiva el, en este caso el div app

<script>
var app = new Vue({

  	el: '#app'
})
</script>

Para pasar los datos con los cuales va a poder trabajar vue usamos data que será un objeto. Por ejemplo si tenemos la varianle message, la definimos y la usamos en html mediante la sintaxis {{ message }}

<script>
var app = new Vue({

  	el: '#app',
  	data: {
    	message: 'Hello Vue!'
  	}
})
</script>

<div id="app">
	{{ message }}
</div>

<h1>Vue.js no va a tener acceso a este nivel</h1>

# Loops pag02.html

La directiva v-text nos permite realizar una asignación directa de contenidos

<span v-text="'Intro: ' + message"></span>

Todo lo que haya dentro del tag span será ignorado, los mensajes complementarios se pueden poner como se muestran en la cadena ya que es código javascript lo que se ejecuta.

Otra opción más limpia

<span>Intro: <span v-text="message"></span></span>

Si queremos hacer una vista condicional dependiendo de si la cadena message tiene contenido usamos la directiva v-show que se le asigna un valor true o false, en este caso usaremos message que en caso de ser vacío devuelve false y true si tiene al menos 1 letra.

<span v-show="message">Intro: <span v-text="message"></span></span>

Si queremos hacerlo con mayor cantidad de letras podemos usar otro condicional.

<span v-show="message.length > 2">Intro: <span v-text="message"></span></span>

Podemos usar tambien la directiva v-if que a diferencia de v-show (oculta el elemento) hace que desaparezca el elemento del DOM. La directiva v-if se puede usar en conjunto con v-else para el caso que no se cumpla la condición.

<span v-if="message">Intro: <span v-text="'Con v-if' + message"></span></span>
<span v-else>Ingrese información en el campo</span>

Para trabajar con loops vamos a definir una lista de tareas como parte de data y la directiva v-for para recorrer el arreglo: v-for="todo in todos" lo que hace es recorre cada posición de el arreglo todos y la asigna a la variable todo.

<div id="app">

  <ul class="list-group">
    <li class="list-group-item" v-for="todo in todos">{{ todo }}</li>
  </ul>

</div>


<script type="text/javascript">

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hola !!',
    todos : ['Tarea 1', 'Tarea 2']
  }
});

</script>

Para solucionar el problema de la renderización con las dobles llaves podemos hacer

<li class="list-group-item" v-for="todo in todos" v-text='todo'></li>

Tambien podemos hacer que cada tarea sea un objeto

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

Ahora deberemos modificar para mostrar accediendo al campo titulo del objeto.

<div id="app">

  <ul class="list-group">
    <li class="list-group-item" v-for="todo in todos">{{ todo.titulo }}</li>
  </ul>

</div>

Tambien podemos usar v-text

<div id="app">

  <ul class="list-group">
    <li class="list-group-item" v-for="todo in todos"><span v-text='todo.titulo'></span></li>
  </ul>

</div>

Podemos agregar más información al objeto tarea con el estado

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

Y reflejarlo accediendo a la nueva variable de estado

<ul class="list-group">
<li class="list-group-item" v-for="todo in todos">
  <span v-text='todo.titulo'></span>
  <small v-if='todo.completed'>Completa</small>
  <small v-else>Incompleta</small>
</li>
</ul>

