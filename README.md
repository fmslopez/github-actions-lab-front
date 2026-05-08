# github-actions-lab-front

He creado 2 workflows para el proyecto hangman-front, uno de ellos es para la integración continua y el otro para el depliegue.
En el fichero ci-front.yml

<img width="337" height="906" alt="captura de ci" src="https://github.com/user-attachments/assets/c9e185d5-3b55-49bf-9b47-d50a9d189a06" />

podemos observar que este workflow se activa cuando se realiza un push y un pull request, sobre la rama hangman-front, tal y como se puede observar en el parámetro paths y todo sobre la rama main.


<img width="792" height="292" alt="captura 1 ci" src="https://github.com/user-attachments/assets/cf322af8-66ff-41aa-85ec-337c70d9245b" />


En cuanto a los jobs, vamos a utilizar una máquina ubuntu, y vamos a tomar las actions de checkout para clonar el repositorio nuestro del proyecto, usremos la versión 18 y estableceremos el directorio de trabajo a hangman-front, realizamos un npm ci y un build.


<img width="417" height="336" alt="captura 2 ci" src="https://github.com/user-attachments/assets/cf92b6cc-933f-46fa-aff1-70820f19abfd" />


Seguidamente realizamos un test sobre el proyecto. 


<img width="437" height="427" alt="captura 3 ci" src="https://github.com/user-attachments/assets/01cf515c-cde4-46c2-9fcd-581d9c4cb856" />


En la siguiente captura se muestra un Bye.
Finalmente, se incluye paso donde se indica que el test depende de que se realice el primer paso del build.

<img width="322" height="272" alt="captura 4" src="https://github.com/user-attachments/assets/6a910d27-9e1e-42c6-b797-a3a41b682711" />


Inicialmente, tenemos un fallo en el test, tal y como se puede observar en las diferentes ejecuciones que se realiza en Actions.  


Se corrige ese error en el fichero start-game.spec.tsx cambiando los arguimentos en lugar de 1 por 2.


<img width="1102" height="470" alt="captura 5 ci" src="https://github.com/user-attachments/assets/1599fc6b-81d1-4f2c-b9fe-00d7e1f2596e" />


Ahora voy a comentar el fichero cd-front.yml

<img width="642" height="747" alt="captura de cd" src="https://github.com/user-attachments/assets/d56a72d6-354f-458d-baa0-c6e017fc07c5" />

En este caso, la ejecución del workflow se va a realizar de forma manual, es decir, dentro de Actions, nos vamos a nuestro workflow del cd y lo ejecutamos en nuestra rama main.

captura 8 cd

Se ejecutará en una máquina ubuntu, utilizo la actions de checkout v6 para clonar el repositorio, pero en este caso como vamos a subir la imagen a nuestro repositorio de Github, tenemos que indicarlo mediante la opción de registry:ghcr.io y luego incluir el usuario y el password, que se toman directamente desde github. 

captura 9 cd

Seguidamente, se hace el build, que en este caso es buildx (es mejor que el build) y por último se hace el push. 

captura 10 cd

Un dato a tener en cuenta es que en el parámetro del with, en la opción tags, tenemos que incluir delante de todo ghcr.io

captura 11

con esto evitamos el siguiente error.

captura 12

También tendremos que ir a settings, actions y cambiar la opción a read and write permissions, para evitar el error que se muestra a continuación.

captura 7

captura 13
