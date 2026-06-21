# Clase Square

## Descripción de la clase

El tipo de datos `Square`, que representa un cuadrado en un espacio bidimensional, estará definido por una clase concreta de igual nombre, **derivada de la clase** [**`Rectangle`**](clase-rectangle.md)**.**

### Atributos

Esta clase no define nuevos atributos.

### Métodos

Esta clase deberá **sobreescribir los métodos virtuales `print()` y `set_vertices()` heredados de la clase** [**`Rectangle`**](clase-rectangle.md)**.**&#x20;

{% hint style="info" %}
Por simplicidad, asumiremos que un cuadrado de vértices $$v_0, v_1, v_2, v_3$$ será válido solo si todas sus aristas $$\overline{v_0v_1}$$, $$\overline{v_1v_2}$$  $$\overline{v_2v_3}$$ y $$\overline{v_3v_0}$$ tienen la misma longitud.&#x20;

De nuevo, considera hacer uso del método estático [`Point2D::distance()`](clase-point2d.md).
{% endhint %}

Además, deberá implementar los siguientes métodos:

<table><thead><tr><th width="129">Visibilidad</th><th width="326">Perfil</th><th>Descripción</th></tr></thead><tbody><tr><td><code>private</code></td><td><code>static bool check(Point2D* vertices)</code></td><td>Comprueba, a partir de un array de 4 objetos <code>Point2D</code> proporcionado como parámetro, si esos vértices conforman un <strong>cuadrado</strong> válido. </td></tr><tr><td><code>public</code></td><td><code>Square()</code></td><td>Método constructor por defecto. Creará un cuadrado con el color que esté establecido por defecto, y los vértices v0=(-1,1); v1=(1,1), v2=(1,-1), y v3=(-1,-1).</td></tr><tr><td><code>public</code></td><td><code>Square(std::string color, Point2D* vertices)</code></td><td>Método constructor. Recibe como parámetro un array de <code>Point2D</code>, de tamaño 4, que contendrá los vértices v0, v1, v2 y v3 (en ese orden). Si esos vértices no conforman un <strong>cuadrado</strong> válido, lanzará una excepción <strong><code>std::invalid_argument</code></strong>.</td></tr><tr><td><code>public</code></td><td><code>void set_vertices(Point2D* vertices)</code></td><td>Modifica los vértices del cuadrado, a partir de un array de <code>Point2D</code> de tamaño 4, que contendrá los vértices v0, v1, v2 y v3 (en ese orden). Si esos vértices no conforman un <strong>cuadrado</strong> válido, lanzará una excepción <strong><code>std::invalid_argument</code></strong>.</td></tr><tr><td><code>public</code></td><td><code>ostream&#x26; operator&#x3C;&#x3C;(ostream &#x26;out, const Square &#x26;square)</code></td><td>Sobrecarga global del operador <code>&#x3C;&#x3C;</code>. <br><br>Recuerda incluir la cabecera <code>&#x3C;ostream></code> en el <code>.h</code>, así como declararlo <code>friend</code> en la clase.</td></tr></tbody></table>

{% hint style="success" %}
Intenta reaprovechar el método `print()` (heredado de `Rectangle`)  en  `operator<<()` (o viceversa), para evitar duplicidad de código.
{% endhint %}

***

## Actividad 16a: Declaración de la clase Square&#x20;

Desde nuestro directorio de trabajo, crea con vim el fichero de cabeceras `Square.h`. Recuerda que debe declarar las funciones que se sobreescriben. Comprueba que la sintaxis es correcta, y finalmente añade el fichero al repositorio git.

***

## Actividad 16b: Definición de la clase Square

Desde nuestro directorio de trabajo, crea con vim el fichero de código fuente `Square.cpp`, de acuerdo con la especificación del fichero de cabeceras `Square.h`. Añade al fichero `Makefile` la regla de compilación pertinente. Corrige los errores de compilación, en caso necesario, y añade los cambios de ambos ficheros al repositorio git.&#x20;

***

## Actividad 17: Depuración de la clase Square

Guarda en nuestro directorio de trabajo (`PRA_2627_P1`), el siguiente fichero de código fuente `testSquare.cpp`:

{% file src="../.gitbook/assets/testSquare.cpp" %}

A continuación, añade una regla `bin/testSquare` a tu `Makefile` para generar el binario ejecutable homónimo. Puedes usar la regla `bin/testRectangle` para inspirarte.&#x20;

{% hint style="warning" %}
Ten en cuenta que el enlazador necesitará el código objeto de los métodos heredados de `Rectangle`, por lo que también existirá una dependencia directa con el fichero de código objeto `Rectangle.o`.
{% endhint %}

Finalmente, ejecuta el binario para comprobar que tu implementación es correcta:

```bash
./bin/testSquare
```

Debería generar una salida como esta:

<details>

<summary>Salida esperada de la ejecución del binario "testSquare"</summary>

```
r1 = [Square: color = red; v0 = (-1,1); v1 = (1,1); v2 = (1,-1); v3 = (-1,-1)]
r1.area() => 4; r1.perimeter() => 8

r2 = [Square: color = green; v0 = (-2,2); v1 = (2,2); v2 = (2,-2); v3 = (-2,-2)]
r2.area() => 16; r2.perimeter() => 16

r2.set_vertices(...) => std::invalid_argument: Provided vertices do not build a valid square!
```

</details>

Si la semántica de tu salida es diferente, revisa tu código.&#x20;

Finalmente, añade `testSquare.cpp` y `Makefile` haz `git commit` y `git push`.
