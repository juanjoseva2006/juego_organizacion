# Tide Escape

Tide Escape es un plataformero vertical en Jack. El personaje está sobre unas plataformas y el agua va subiendo desde abajo. Cada plataforma que pisas se rompe a los pocos segundos y reaparece más arriba, así que toca seguir saltando o la marea te alcanza.

## Integrantes

Sebastian Acosta Molina
Juan Jose 
Yan Frank Rios Lopez 



Video de YouTube: 

## El juego

La mayoría de juegos en Jack que vimos por ahí son Snake, Pong o clones directos de Doodle Jump. La diferencia con Tide Escape es que mezcla dos cosas al tiempo: las plataformas se rompen y el agua sube, así que no puedes quedarte quieto. En los últimos 30 frames antes de que una plataforma se vaya parpadea, para que sepas que ya casi se cae.

Se mueve con flecha izquierda y derecha, se salta con la flecha arriba, y cualquier tecla arranca la partida desde la pantalla de inicio.

## Cómo correrlo

Se ejecuta en Nand2TetrisCompilando la carpeta con el JackCompiler, abrir el VMEmulator, Load Program sobre la carpeta y Run. Mejor subir la velocidad del emulador al máximo con animaciones por defecto el juego se ve en cámara lenta y la marea pierde la presión.

Solo se usan clases del Jack OS estándar (`Screen`, `Output`, `Keyboard`, `Sys`, `Memory`, `Array`).

## Archivos

Son cuatro. [`Main.jack`](Tide_Escape/Main.jack) es la entrada del programa. [`Game.jack`](Tide_Escape/Game.jack) tiene el bucle principal y el estado del juego (jugador, plataformas, agua, puntaje). [`Player.jack`](Tide_Escape/Player.jack) es el personaje con su salto, gravedad y aterrizaje. [`Platform.jack`](Tide_Escape/Platform.jack) es la plataforma con su timer y el parpadeo.

## Retos que nos enfrentamos

Tuvimos tres problemas grandes durante el desarrollo.

Al inicio tuvimos un desbordamiento de memoria. En la primera versión, cada vez que una plataforma se rompía creábamos una nueva con `Platform.new` sin liberar la vieja. Después de unas decenas de saltos el VMEmulator tiraba ERR6 y el juego se moría. Lo arreglamos dejando un array fijo de siete plataformas desde el inicio, y cuando una se rompe la reusamos con un método `reset` que le cambia las coordenadas. Así no se pide memoria nueva durante la partida.

Otro fue la velocidad del jugador. Habíamos puesto un movimiento de 2 píxeles por pulsación y un salto suave, y al probarlo no alcanzabas a llegar de una plataforma a la siguiente antes de que el agua subiera. Subimos el desplazamiento a 8 píxeles y el impulso del salto a `velY = -12`, y ahí sí se puede planear la ruta.

El tercero fue parpadeo. Como redibujábamos en cada frame había flicker en el jugador y en las plataformas. Agregamos un método `erase` en las dos clases que pinta el rectángulo en blanco antes de moverlo, y solo redibujamos lo que cambia.

## Requisitos
Nand2Tetris Software Suite (versión 2.6 o superior). Se descarga de nand2tetris.org/software.
Java Runtime Environment (JRE) 8 o superior, porque las herramientas del suite (JackCompiler, VMEmulator) corren sobre Java.
Sistema operativo: Windows, macOS o Linux
No se necesitan librerías ni dependencias externas, solo el Jack OS estándar que viene con el suite.
