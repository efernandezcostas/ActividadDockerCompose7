# Preparativos

**Crear la carpeta donde almacenar el docker-compose.yaml**   
<code>mkdir joomla</code>      
<code>cd joomla</code>

**Crear el archivo docker-compose.yaml**
<code>nano docker-compose.yml</code>

~~~
name: "Actividad7"

services:
  mysql:
    image: mysql
    restart: always
    environment:
      MYSQL_DATABASE: bdjoomla
      MYSQL_USER: enrique
      MYSQL_PASSWORD: admin
      MYSQL_ROOT_PASSWORD: admin
    volumes:
      - mysql_datos:/var/lib/mysql

  joomla:
    image: joomla
    restart: always
    ports:
      - 8080:80
    environment:
      JOOMLA_DB_HOST: mysql
      JOOMLA_DB_NAME: bdjoomla
      JOOMLA_DB_USER: enrique
      JOOMLA_DB_PASSWORD: admin
    volumes:
      - joomla_datos:/var/www/html
    depends_on:
      - mysql

  php:
    image: phpmyadmin
    restart: always
    ports:
      - 8081:80
    depends_on:
      - mysql
    environment:
      PMA_ARBITRARY: 1
      DB_HOST: mysql

volumes:
  mysql_datos:
  joomla_datos:
~~~

# Instalación
**Lanzar el docker compose**   
<code>docker compose up -d</code>

*Para eliminarlo y limpiar los volúmenes de datos:*    
<code>docker compose down -v</code>

**Comprobar que se crearon los contenedores y están en ejecución**   
<code>docker ps -a</code>

~~~
CONTAINER ID   IMAGE                          COMMAND                  CREATED         STATUS                     PORTS                                     NAMES
6bdbf490c05e   phpmyadmin                     "/docker-entrypoint.…"   5 seconds ago   Up 3 seconds               0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   actividad7-php-1
cba2817ce3db   joomla                         "/entrypoint.sh apac…"   5 seconds ago   Up 3 seconds               0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   actividad7-joomla-1
6567d497769f   mysql                          "docker-entrypoint.s…"   5 seconds ago   Up 4 seconds               3306/tcp, 33060/tcp                       actividad7-mysql-1
~~~

# Configuración
## Joomla
**Entrar a la página desde el navegador** *\<ip\>:\<puerto\>*   

![Screenshot_20241111_111153](https://github.com/user-attachments/assets/c31eb803-e2bf-427b-8ae1-aa9b209d17ae)

**Tras configurarlo:**    

![image](https://github.com/user-attachments/assets/05b334dc-c41a-4fa8-9cd6-10785f5a54e5)

**Página de administración:**    

![image](https://github.com/user-attachments/assets/11aea955-60e4-4346-bb32-86dc01a6ea42)

**Página principal:**   

![image](https://github.com/user-attachments/assets/4bc8bde8-83b1-4994-9b4f-3f72d788d8d6)

## PhpMyAdmin

**Entrar a la página desde el navegador**

![image](https://github.com/user-attachments/assets/16e2efd2-2ad3-4d1c-9636-fd0d810254cb)

**Tras poner los datos:**   

![image](https://github.com/user-attachments/assets/001c4820-ccd8-4d5c-bd8f-260d69b3d020)





