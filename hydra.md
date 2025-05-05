<h2>Ejercicio Hrydra</h2>

La siguiente herramienta que utilizamos es **Hydra**, y a continuación detallamos los pasos que seguimos para obtener la contraseña del usuario admin en Mutillidae.

Para ello, ejecutamos el comando `hydra`, ya que es la herramienta que empleamos para realizar el ataque de **fuerza bruta**. Utilizamos la opción `-l admin` para indicar que solo se probará el usuario **admin**, y `-P cewl.mutillidae.txt` para que **Hydra** cargue un diccionario personalizado con posibles contraseñas extraídas previamente del sitio web **Mutillidae**.

Especificamos la **dirección IP** del servidor objetivo (`10.0.2.10`) y el módulo `http-form-post`, que le indica a **Hydra** que el objetivo es un formulario web que recibe datos mediante **solicitudes POST**.

Luego, añadimos la ruta exacta del formulario de inicio de sesión: `/mutillidae/index.php?page=login.php`.

A continuación, definimos los datos que Hydra debe enviar en cada solicitud: `username=^USER^&password=^PASS^&login-php-submit-button=Login`.

Esta cadena la extraemos previamente desde BurpSuite (observar en el ejercicio anterior), interceptando un intento de login en la pestaña **Proxy**, aunque reemplazamos el usuario y la contraseña originales por los marcadores `^USER^` y `^PASS^`, que **Hydra** sustituye automáticamente con los valores del diccionario y el nombre de usuario especificado.

Agregamos también el texto de error "`Password incorrect`", que es la respuesta que la página web devuelve cuando el intento de autenticación falla. **Hydra** lo utiliza para distinguir entre combinaciones incorrectas y posibles accesos válidos.

Al ejecutar el comando completo, **Hydra** prueba todas las contraseñas del diccionario contra el usuario **admin**, y finalmente nos devuelve la contraseña válida: **adminpass**.

