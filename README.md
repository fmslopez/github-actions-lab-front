# github-actions-lab-front

He creado 2 workflows para el proyecto hangman-front, uno de ellos es para la integración continua y el otro para el depliegue.
En el fichero ci-front.yml

<img width="337" height="906" alt="captura de ci" src="https://github.com/user-attachments/assets/c9e185d5-3b55-49bf-9b47-d50a9d189a06" />

podemos observar que este workflow se activa cuando se realiza un push y un pull request, sobre la rama hangman-front, tal y como se puede observar en el parámetro paths y todo sobre la rama main.

En cuanto a los jobs, vamos a utilizar una máquina ubuntu, y vamos a tomar las actions de checkout para clonar el repositorio nuestro del proyecto, usremos la versión 18 y estableceremos el directorio de trabajo a hangman-front, realizamos un npm ci y un build.
Seguidamente realizamos un test sobre el proyecto. Inicialmente, tenemos un fallo en el test, tal y como se puede observar en las diferentes ejecuciones que se realiza en Actions. Se corrige ese error en el fichero start-game.spec.tsx cambiando los arguimentos en lugar de 1 por 2.
Finalmente, se incluye paso donde se indica que el test depende de que se realice el primer paso del build.
Por último, se muestra un Bye.

Ahora voy a comentar el fichero cd-front.yml

<img width="642" height="747" alt="captura de cd" src="https://github.com/user-attachments/assets/d56a72d6-354f-458d-baa0-c6e017fc07c5" />

En este caso, la ejecución del workflow se va a realizar de forma manual, es decir, dentro de Actions, nos vamos a nuestro workflow del cd y lo ejecutamos en nuestra rama main.
Se ejecutará en una máquina ubuntu, utilizo la actions de checkout v6 para clonar el repositorio, pero en este caso como vamos a subir la imagen a nuestro repositorio de Github, tenemos que indicarlo mediante la opción de registry:ghcr.io y luego incluir el usuario y el password, que se toman directamente desde github. Seguidamente, se hace el build, que en este caso es buildx (es mejor que el build) y por último se hace el push. Un dato a tener en cuenta es que en el parámetro del with, en la opción tags, tenemos que incluir delante de todo ghcr.io
(También tendremos que ir a settings, actions y cambiar la opción a read and write permissions)
