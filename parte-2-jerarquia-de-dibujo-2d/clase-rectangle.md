# Clase Rectangle

## Descripción de la clase

El tipo de datos Rectangle, que representa un rectángulo en un espacio bidimensional, estará definido por una clase concreta de igual nombre, derivada de la interfaz Shape.

### Atributos

<table><thead><tr><th width="129">Visibilidad</th><th width="220">Declaración</th><th>Descripción</th></tr></thead><tbody><tr><td><code>public</code></td><td><code>static int const N_VERTICES = 4</code></td><td>Constante con el número de vértices de un rectángulo (4).</td></tr><tr><td><code>protected</code></td><td><code>Point2D* vs</code></td><td>Puntero a un array de 4 elementos de tipo <code>Point2D</code> correspondientes a los vértices v0, v1, v2 y v3 de un rectángulo. </td></tr></tbody></table>

### Métodos

**Además de los métodos abstractos heredados de la interfaz** [**`Shape`**](clase-abstracta-shape.md), deberá implementar los siguientes métodos:

<table><thead><tr><th width="129">Visibilidad</th><th width="326">Perfil</th><th>Descripción</th></tr></thead><tbody><tr><td><code>public</code></td><td><code>Rectangle()</code></td><td>Método constructor por defecto. Creará un rectángulo con el color que esté establecido por defecto, y los vértices v0=(-1,0.5); v1=(1,0.5), v2=(1,-0.5), y v3=(-1,-0.5).</td></tr><tr><td><code>public</code></td><td><code>Rectangle(std::string color, Point2D* vertices)</code></td><td>Método constructor. Recibe como parámetro una cadena con el color de la figura, y un array de <code>Point2D</code>, de tamaño 4, que contendrá los vértices v0, v1, v2 y v3 (en ese orden). Si esos vértices no conforman un rectángulo, lanzará una excepción <strong><code>std::invalid_argument</code></strong>.</td></tr><tr><td><code>public</code></td><td><code>Rectangle(const Rectangle &#x26;r)</code></td><td><strong>Constructor de copia</strong>. Permitirá hacer una copia segura de rectángulos. </td></tr><tr><td><code>public</code></td><td><code>~Rectangle()</code></td><td>Método destructor. Se encargará de liberar la memoria dinámica reservada por el array <code>vs</code>.</td></tr><tr><td><code>public</code></td><td><code>Point2D get_vertex(int ind) const</code></td><td>Devuelve el <code>Point2D</code> del rectángulo que ocupa el índice <code>ind</code>. Lanza una excepción <strong><code>std::out_of_range</code></strong> si el índice no es válido (fuera del intervalo <code>[0, N_VERTICES-1]</code>).</td></tr><tr><td><code>public</code></td><td><code>Point2D operator[](int ind) const</code></td><td><strong>Sobrecarga del operador <code>[]</code>.</strong> Devuelve el elemento situado en la posición <code>ind</code>. Lanza una excepción <strong><code>std::out_of_range</code></strong> si la posición no es válida (fuera del intervalo <code>[0, N_VERTICES-1]</code>).</td></tr><tr><td><code>public</code></td><td><code>virtual void set_vertices(Point2D* vertices)</code></td><td><strong>Método virtual.</strong> Modifica los vértices del rectángulo, a partir de un array de <code>Point2D</code> de tamaño 4, que contendrá los vértices v0, v1, v2 y v3 (en ese orden). Si esos vértices no conforman un <strong>rectángulo</strong> válido, lanzará una excepción <strong><code>std::invalid_argument</code></strong>.</td></tr><tr><td><code>public</code></td><td><code>Rectangle&#x26; operator=(const Rectangle &#x26;r);</code></td><td>Sobrecarga del operador <code>=</code> (<strong>asignación de copia</strong>). Permitirá hacer una copia segura de rectángulos. </td></tr><tr><td><code>public</code></td><td><code>std::ostream&#x26; operator&#x3C;&#x3C;(ostream &#x26;out, const Rectangle &#x26;r)</code></td><td>Sobrecarga global del operador <code>&#x3C;&#x3C;</code>. <br><br>Recuerda incluir la cabecera <code>&#x3C;iostream></code> en el <code>.h</code>, así como declararlo <code>friend</code> en la clase.</td></tr><tr><td><code>private</code></td><td><code>static bool check(Point2D* vertices)</code></td><td>Comprueba, a partir de un array de 4 objetos <code>Point2D</code> proporcionado como parámetro, si esos vértices conforman un rectángulo válido. Ver nota más abajo. </td></tr></tbody></table>

{% hint style="info" %}
Por simplicidad, asumiremos que un rectángulo de vértices $$v_0, v_1, v_2, v_3$$ será válido solo si, por un lado, las aristas $$\overline{v_0v_1}$$ y $$\overline{v_2v_3}$$ tienen la misma longitud, y por otro lado, las aristas $$\overline{v_1v_2}$$ y $$\overline{v_3v_0}$$ tienen la misma longitud.&#x20;

Considera hacer uso del método estático [`Point2D::distance()`](clase-point2d.md).
{% endhint %}

{% hint style="success" %}
Aprovecha que sobreescribes el `operator<<` en la clase para simpificar la sobrescritura del método `print()`.
{% endhint %}

***

## Actividad 14a: Declaración de la clase Rectangle

Desde nuestro directorio de trabajo (`PRA_2425_P1`), crea con vim el fichero de cabeceras `Rectangle.h`. Dado que esta clase va a ser importada desde múltiples fuentes, **debemos envolver la definición de la clase dentro de una guarda de importación** _("include guard")_, usando las directivas del preprocesador `ifndef <VAR>` _(if-not-defined)_ y `define <VAR>`. Esto nos evitará los errores de compilación correspondientes a una importación múltiple. Aquí tienes una plantilla:

```cpp
#ifndef RECTANGLE_H
#define RECTANGLE_H

#include <iostream>
#include "Shape.h"
#include "Point2D.h"

class Rectangle : ??? {
    //...
};

#endif
```

Recuerda que debe declarar las funciones que se sobreescriben. Comprueba que la sintaxis es correcta, y finalmente añade el fichero al repositorio git.

{% hint style="danger" %}
Es muy importante que **declares virtuales los métodos `print()` y `set_vertices()`, para que sean polimórficos** (ten en cuenta que la clase derivada [`Square`](clase-square.md) los sobreescribirá).
{% endhint %}

***

## Actividad 14b: Definición de la clase Rectangle

Desde nuestro directorio de trabajo, crea con vim el fichero de código fuente `Rectangle.cpp`, de acuerdo con la especificación del fichero de cabeceras `Rectangle.h`. Añade al fichero `Makefile` la regla de compilación pertinente. Corrige los errores de compilación, en caso necesario, y añade los cambios de ambos ficheros al repositorio git.&#x20;

***

## Actividad 15: Depuración de la clase Rectangle

Guarda en nuestro directorio de trabajo (`PRA_2627_P1`), el siguiente fichero de código fuente `testRectangle.cpp`:

{% file src="../.gitbook/assets/testRectangle.cpp" %}

A continuación, añade una regla `bin/testRectangle` a tu `Makefile` para generar el binario ejecutable homónimo. Puedes usar la regla `testCircle` para inspirarte.

Finalmente, ejecuta el binario para comprobar que tu implementación es correcta:

```bash
./bin/testRectangle
```

Debería generar una salida como esta:

<details>

<summary>Salida esperada de la ejecución del binario "testRectangle"</summary>

```
r1 = [Rectangle: color = red; v0 = (-1,0.5); v1 = (1,0.5); v2 = (1,-0.5); v3 = (-1,-0.5)]
r1.area() => 2; r1.perimeter() => 6
r2 = [Rectangle: color = green; v0 = (-1,1); v1 = (1,1); v2 = (1,-1); v3 = (-1,-1)]
r2.area() => 4; r2.perimeter() => 8

r1.get_vertex(0) => (-1,0.5); r1[0] => (-1,0.5)
r1.get_vertex(3) => (-1,-0.5); r1[3] => (-1,-0.5)

r2.translate(10,10) =>
    r2 = [Rectangle: color = green; v0 = (9,11); v1 = (11,11); v2 = (11,9); v3 = (9,9)]

r2.set_vertices(...) => std::invalid_argument: Provided vertices do not build a valid rectangle!

Rectangle r3 = r1; Aleshores...
r1 = [Rectangle: color = red; v0 = (-1,0.5); v1 = (1,0.5); v2 = (1,-0.5); v3 = (-1,-0.5)]
r3 = [Rectangle: color = red; v0 = (-1,0.5); v1 = (1,0.5); v2 = (1,-0.5); v3 = (-1,-0.5)]
r3.translate(100, 100); Aleshores...
r1 = [Rectangle: color = red; v0 = (-1,0.5); v1 = (1,0.5); v2 = (1,-0.5); v3 = (-1,-0.5)]
r3 = [Rectangle: color = red; v0 = (99,100.5); v1 = (101,100.5); v2 = (101,99.5); v3 = (99,99.5)]
```

</details>

Si la salida es diferente, revisa tu código.&#x20;

Finalmente, añade `testRectangle.cpp` y `Makefile` haz `git commit` y `git push`.
