## Diferencias fundamentales: ¿Cuál dirías que es la diferencia principal en cómo Flow Fields y Flocking logran el movimiento coordinado o dirigido de los agentes? (piensa en dónde reside la “inteligencia” o las reglas: ¿En el entorno o en las interacciones entre agentes?).

Los flow fields predeterminan unos vectores los cuales luego son utilziados como direcciones para hacer steering por diferentes vehiculos, el flocking logra moverse mediante reglas que hacen alterar los movimeintos dinamicamente. En uno el enetorno es el que dicta como se movera en el otro las reglas que siguen son las que dictan como se hace.

## Tipos de comportamiento emergente: basado en tu análisis y aplicación, ¿Qué tipo de comportamiento colectivo o patrón visual crees que es más fácil o natural lograr con Flow Fields? ¿Y con Flocking? Da ejemplos.

Con flowfields siento que es mas facil recrear movimientos caoticos pero definidos como lo seria el viento, los ripples del agua, la caida de una hoja de papel o en general fenomenos fisicos. Para el flocking siento que es mejor para cuando hablamos de mover una multitud de elementos organicos como lo serian bandas de pajaros, cabezas de ganado, renacuajos, etc.

## Ventajas y desventajas: en tu opinión, ¿Cuáles podrían ser las ventajas o desventajas de usar uno u otro algoritmo para ciertos tipos de efectos visuales o simulaciones?

Las ventajas del flowfields es que nos permite movernos en un espacio de manera organica y "random" con la cual podemos lograr simulaciones muy organicas pero que no tengan reaccion al enterno. El flocking por su parte es bueno para mover muchos objetos en un comportamiento pero tiende a ser un poco mas rigido en su dinamica ya que no es tan organico a la hora de moverse por el espacio. Cada algarotimo sirve para casos distintos que combinados pueden ser muy interesantes.

## El agente autónomo: ¿Cómo te ayudaron estos dos ejemplos (Flow Fields y Flocking) a entender mejor el concepto de “agente autónomo”? ¿Qué características definen a un agente en estos sistemas?

El agente autonomo me quedo descrito como una entidad o objeto el cual sigue una serie de reglas para moverse, si o si asi sea con flocking que son reglas mas directas o con flow fields en ambos casos este agente autonomo se mueve solo y actua solo peeeero actua bajo ese orden de reglas sea en moverse en cierto vector o en seguir a otros que se estan moviendo autonomamente.

## Emergencia: ¿En qué momento observaste “comportamiento emergente” (complejidad o patrones no programados explícitamente) al trabajar con estos algoritmos?

Al modificar las reglas sabes que va a suceder pero no lo que sucede en el durante, esto quiere decir que observe comportamientos erraticos cuando estaba digamos tirandole piedras a los pajaros (perdon) yo sabia que se iban a regar por todos lados pero no tenia ni idea de como se reagrupaban, e inclusive comence a notar que con cada piedra cambiaban el tamaño de flock, puede que comenzaran con un grupo super grande y luego ese se divideira en varios pequeños para leugo vovler a reunirse.
