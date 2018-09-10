# TwoDatabaseExample
Ejemplo de conexión a dos bases de datos en laravel con gestores diferentes (MySQL y PostgreSQL).

## Getting Started

Estas instrucciones te permitirán obtener una copia del proyecto en funcionamiento en su máquina local para fines de desarrollo y prueba.

### Prerequisites
Tener nociones basicas de laravel y con entornos de trabajo dedicados a este.

## Steps
* Descargar e instalar laragon (Version WAMP) https://laragon.org/download/index.html
* Descargar binarios de postgreSQL https://www.enterprisedb.com/download-postgresql-binaries
* Colocar los binarios de postgres en Laragon 
``` 
  1 Dirigete a la direccion local de tu equipo en la carpeta de laragon: C:\laragon
  2 Copia los binarios de postgres que descargaste y pegalos en la siguiente ubicación
		C:\laragon\bin\postgresql
		Nota: si no existe la carpeta postgresql, crearla
  3 Descomprimir los binarios de la siguiente forma:
		3.1 Crear una carpeta con el nombre de los binarios de postgres
			Ejem: postgresql-9.6.10-1-windows-x64-binaries
		3.2 Abrir los binarios con un gestor de archivos comprimidos (winrar, 7zip)
		3.3 Entrar en la carpeta pgsql de los binarios comprimidos
		3.4 Extraer todas las carpetas y archivos dentro de la carpeta que creamos anteriormente (postgresql-9.6.10-1-windows-x64-binaries)
```
* Configurar el arhivo php.ini
```
  1- Iniciar laragon en modo administrador
  2- Dirigirse al icono que aparece en la barra de tareas de laragon y dar click derecho
  3- Dirigirse a la pestaña de PHP, y despues dar un clic en php.ini	
  4- Laragon incluye por defecto un editor de texto (Notepad++), presionar ctrl+f y buscar pdo y dar click en "find next"
  5- Descomentar las siguientes lineas de codigo quitando el punto y coma del inicio:
		    * extension=php_pdo_pgsql.dll
		    * extension=php_pgsql.dll
  6- Guardar el archivo
	      * Nota: Si pide abrir el editor como administrar, dar click en permitir y volver a guardar el archivo
```
* Configurar proyectos laravel en laragon para inicializar con dos gestores de bases de datos
```
  1- Iniciar laragon en modo administrador (Puedes dejar seteada esta configuracion en las propiedades del acceso directo)
  2- Dar click en "preferences" (Icono de engrane)
  3- Revisar que este palomeada la opcion de Auto virtual hosts
	  3.1- Cambiar el nombre de hostname {name}.dev por {name}.test
  4- Dirigirse a la pestaña de "Services & Ports"
	  4.1- Tener palomeadas las siguientes opciones:
			  * Apache (Verificar que este en el puerto 80)
			  * MySQL (Verificar que este en el puerto 3306)
			              ----En advanced----
			  * PostgreSQL (Verificar que este en el puerto 5432)
			  * Nginx (Verificar que este en el puerto 8080)
  5- Reinicar laragon
```
* Inicializar laragon y dar click en "Start All"
* Crear las bases de datos MySQL desde laragon > Database
```
Nombre: basedatos1 y en collation: utf8mb4_unicode_ci
```
* Crear base de datos PostgreSQL desde laragon > postgresql > pgAdmin4
```
  1- Crear un nuevo grupo de servers con el nombre que tu desees
  2- Crear la base de datos en el nuevo servidor de grupos, click derecho y create database con los siguientes datos:
		  * Nombre: basedatos2
		  * owner: postgres
		  * encoding: UTF8
		  * Tablespace: pg_default
		  * collation: Spanish_Mexico.1252 (Si no existe dejar en blanco)
		  * Character Type: Spanish_Mexico.1252 (Si no existe dejar en blanco)
  3 Dar click en guardar.
```
* Descargar el proyecto y guardarlo en la siguiente ruta: ``` c:\laragon\www\ ```
* Renombra el archivo  ``` .env.example  ``` a  ``` .env  ``` (contiene los parametros utilizados para la conexion a la base de datos).
* Ejecuta el siguiente comando ```composer install``` 
* Ejecuta el siguiente comando ``` php artisan key:generate ```
* Ejecuta el siguiente comando ``` php artisan migrate:refresh --seed --database="pgsql" ```
* Ejecuta el siguiente comando ``` php artisan migrate:refresh --seed --database="mysql" ```
* Ejecuta el siguiente comando ``` php artisan serve ```
```
Nota: Puedes remplazar facilmente estos parametros por las credenciales de tus bases de datos alojadas en servidores.
```
## Running
Una vez configurado el proyecto puedes probar estas rutas de ejemplo para observar su comportamiento
```
Ruta de ejemplo: 
* http://mysqlpostgreexample.test/api/user/POSTGRES  
* http://mysqlpostgreexample.test/api/user/MYSQL
* http://mysqlpostgreexample.test/api/user/SQLITE
```

## Built With
* [Laravel](https://laravel.com/docs/5.7) - Framework utilizado
* [Laragon](https://laragon.org/download/index.html) - Entorno de desarrollo para laravel
