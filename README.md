# Expresiones regulares + Funciones de Extensión

## 1. ¿Qué es una expresión regular?
Una expresión regular (regular expression o regex) es una secuencia de carácteres que define un patrón de búsqueda, utilizada para encontrar, modificar, reemplazar, transformar u otros cadenas de texto según un patrón previamente definido; en resumen, sirve para manipular texto complejo de una manera muy sencilla.

Se utiliza haciendo uso del constructor de la clase `Regex` (clase que está disponible como parte de la biblioteca estándar de Kotlin desde su versión 1.0).

Un ejemplo básico de uso utilizando los métodos `matches` y `containsMatchIn`:
```kotlin
// * Creamos una variable inmutable llamada 'regex' que contiene 
//   el patrón de búsqueda (en este ejemplo, la palabra "Hola").
val regex = Regex("Hola")

// * Creamos una cadena de texto que usaremos como entrada para el ejemplo.
val input = "Hola 1DAWB"

// * Uso del método matches() para comprobar si TODA la cadena coincide
//   exactamente con el patrón. En este caso, dará "false" porque "Hola 1DAWB"
//   no coincide completamente con "Hola".
println(regex.matches(input)) // false

// * Uso del método containsMatchIn() para comprobar si el patrón 
//   está presente EN CUALQUIER PARTE de la cadena. En este caso, dará "true"
//   porque la palabra "Hola" si está dentro de "Hola 1DAWB".
println(regex.containsMatchIn(input)) // true
```


## 2. ¿Para qué se usan?
Las expresiones regulares tienen multitud de usos.

Algunos de los más comunes:

1. **Validar una cadena de texto** (por ejemplo, verificar si un correo electrónico, un DNI o un número de teléfono tienen un formato específico).
2. **Encontrar un patrón de texto en una cadena** (buscando palabras o secuencias específicas dentro de la misma).
3. **Encontrar y extraer números específicos** dentro de un texto.
4. **Coincidir con un rango de caracteres**, buscando por ejemplo letras de A-Z o números de 0-9.
5. **Reemplazar texto por otro** según el patrón definido.
6. **Separar una cadena en partes** usando un delimitador definido por un patrón establecido.

## 3. Explica las expresiones regulares con un ejemplo práctico.
```kotlin
fun buscarLetra(palabra: String, letra: Char): Boolean {
    // Creamos una expresión regular para buscar una letra en una palabra.
    val patronLetra = Regex(".*$letra.*")
    
    // True si se encuentra, False en el caso de no encontrarla.
    return patronLetra.matches(palabra)
}

fun main() {
    val palabra = "hola"
    val letra = 'o'

    println("La letra $letra " + if (buscarLetra(palabra, letra)) "se encuentra en la palabra." else "no se encuentra en la palabra.")
}
```

## 4. Localiza en la práctica del Ahorcado dónde se utiliza una expresión regular. Analiza y explica el código en detalle.

## 5. ¿Qué es una función de extensión?

## 6. Desarrolla y explica una función de extensión que se llame filtrar para la clase List<String>. Esta función debe utilizar una expresión regular para filtrar los elementos de la lista. El resultado será una lista con los elementos que coincidan con el patrón que se pasará a dicha función.
