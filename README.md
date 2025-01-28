# Expresiones regulares + Funciones de Extensión

## 1. ¿Qué es una expresión regular?
Una expresión regular (regular expression o regex) es una secuencia de carácteres que define un patrón de búsqueda, utilizada para encontrar, modificar, reemplazar, transformar u otros cadenas de texto según un patrón previamente definido; en resumen, sirve para manipular texto complejo de una manera muy sencilla.

Se utiliza haciendo uso del constructor de la clase `Regex` (clase que está disponible como parte de la biblioteca estándar de Kotlin desde su versión 1.0).

Algunos de los métodos que contiene la clase `Regex`:
1. `matches`: Comprueba si toda la cadena coincide exactamente con el patrón dado.
2. `containsMatchIn`: Comprueba si el patrón está presente en cualquier parte de la cadena.
3. `split`: Divide la cadena en una lista de subcadenas usando el patrón como delimitador.
4. `replace`: Reemplaza todas las ocurrencias en la cadena por el patrón.

Un ejemplo básico de uso utilizando los métodos `matches` y `containsMatchIn`:
```kotlin
// * Creamos una expresión regular con el contenido "Hola" como patrón.
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
7. **Comprobar si una contraseña cumple con ciertos requisitos.**

## 3. Explica las expresiones regulares con un ejemplo práctico.
```kotlin
fun buscarLetra(palabra: String, letra: Char): Boolean {
    // Creamos una expresión regular para buscar una letra en una palabra.
    // NOTA: Los símbolos .* indican que puede haber cualquier cantidad de caracteres antes de la parte que estamos buscando, incluidos 0 caracteres.
    // siendo . CUALQUIER CARACTER y * cero o más.
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
Una **función de extensión** es una manera de añadir nuevas funcionalidades a clases que ya existen sin tener que modificar su código. Sería como "extender" la funcionalidad de una clase con nuevas funciones.
Por ejemplo, podemos crear funcionalidades para la clase `String`:

Ejemplo de función de extensión que muestra un `String` tres veces por consola:
```kotlin
fun String.mostrarTresVeces(): String {
    return this.repeat(3)
}


fun main() {
    println("Prueba ".mostrarTresVeces())
}
```
Output:
```
Prueba Prueba Prueba
```

Ejemplo de función de extensión que permite a 'Nombre' (o otra palabra que se nos ocurra) saludar:
```kotlin
// * Añadimos la función saludar a la clase String, que retorna Hola junto al String al que apliquemos la función.
fun String.saludar(): String {
    return "¡$this te saluda!"
}


fun main() {
    println("Nombre".saludar())
}

```
Output:
```
¡Nombre te saluda!
```

Ejemplo utilizando `Regex`:
```kotlin
// * Función de extensión para reemplazar las vocales por un símbolo dado.
fun String.reemplazarVocales(simbolo: String): String {
    return this.replace(Regex("[aeiouAEIOU]"), simbolo)
}


fun main() {
    // Definimos un texto de prueba
    val texto = "Hola 1DAWB"

    // Llamamos a la función de extensión reemplazarVocales y le pasamos el símbolo "*".
    val resultado = texto.reemplazarVocales("*")

    println(resultado)
}
```
Output
```
H*l* 1D*WB
```

Un ejemplo algo más complejo:
```kotlin
fun String.comprobarTexto(): Boolean {
    // Patrón para validar que un texto tiene entre 1 y 5 caracteres y al menos uno de ellos es mayúscula.
    // SOLO permite letras A-Z.
    // https://regex101.com/
    val regex = Regex("^(?=(.*[A-Z]))[A-Za-z]{1,5}$")
    return this.matches(regex)
}


fun main() {
    val textoValido = "AAacx"
    println(textoValido.comprobarTexto())
    
    val textoInvalido = "1axcxd"
    println(textoInvalido.comprobarTexto())
}
```
Output
```
true
false
```

## 6. Desarrolla y explica una función de extensión que se llame filtrar para la clase List<String>. Esta función debe utilizar una expresión regular para filtrar los elementos de la lista. El resultado será una lista con los elementos que coincidan con el patrón que se pasará a dicha función.

### Fuentes

- **Documentación oficial de Kotlin**: [Kotlin Docs](https://kotlinlang.org/docs/home.html)
  
- **Pruebas interactivas de expresiones regulares**: [Regex101](https://regex101.com/)
  
- **Referencia de Regex en Kotlin**: [Kotlin Regex API](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.text/-regex/) 
