## Preguntas

✅ 1. ¿Cómo se gestiona la creación y la desaparición de las partículas y cómo se gestiona la memoria?

✅ 2. ¿Cómo se aplica el marco de movimiento motion 101 en los sistemas de partículas que analizaste en la actividad anterior?

✅ 3. ¿Cómo se aplican fuerzas externas a los sistemas de partículas que trabajaste en la unidad? ¿Qué fuerzas se aplicaron y cómo están modeladas?

✅ 4. ¿Cómo se aplicaste los conceptos de herencia y polimorfismo en los sistemas de partículas que trabajaste en la unidad?

### Respuestas

1. La creacion y la desaparicion de las particulas se gestiona agregando un numero de particulas a un array en el cual dinamicamente esta usando las particulas prendiendolas y apagandolas como fue enseñado en la unidad.
2. El marco de movimiento se utiliza para mover tanto las particulas que son lanzables por la catapulta como las particulas del viento
3. Las fuerzas externas utilziadas son la fuerza del viento y la fuerza de repulsion. Se modelan con los parametros de los motion 101. Se aplican la fuerza del viento en cada projectil lanzado, la repulsion la estrella la tiene para repulsar el viento y todas son afectadas por la gravedad
4. El concepto de herencia se aplica con los lanzables, se creo una clase lanzable y de ella heredaron las diferentes clases para cada projectil. El polimorfismo llega en como cada uno maneja las fuerzas, en general el polimorfismo mas marcado es en el cual el projectil de la estrella ahora tambien tiene repulsion de las particulas al igual que otras variaciones de diferentes fuerzas.
