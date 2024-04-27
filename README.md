Laboratorio | Consultas SQL 6
En esta actividad vamos a realizar un mantenimiento de la base de datos. En la base de datos actual solo tenemos información sobre películas del año 2006. Ahora también hemos recibido el catálogo de películas del año 2020. Para estos nuevos datos crearemos otra tabla e insertaremos de forma masiva todos los datos allí. A continuación se proporciona el código para crear una nueva tabla.

drop table if exists films_2020;
CREATE TABLE `films_2020` (
  `film_id` smallint(5) unsigned NOT NULL AUTO_INCREMENT,
  `title` varchar(255) NOT NULL,
  `description` text,
  `release_year` year(4) DEFAULT NULL,
  `language_id` tinyint(3) unsigned NOT NULL,
  `original_language_id` tinyint(3) unsigned DEFAULT NULL,
  `rental_duration` int(6),
  `rental_rate` decimal(4,2),
  `length` smallint(5) unsigned DEFAULT NULL,
  `replacement_cost` decimal(5,2) DEFAULT NULL,
  `rating` enum('G','PG','PG-13','R','NC-17') DEFAULT NULL,
  PRIMARY KEY (`film_id`),
  CONSTRAINT FOREIGN KEY (`original_language_id`) REFERENCES `language` (`language_id`) ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB AUTO_INCREMENT=1003 DEFAULT CHARSET=utf8;

Tenemos solo un elemento para cada película y todos se colocarán en la nueva tabla. Para 2020, la duración del alquiler será de 3 días, con un precio de oferta de 2.99€y un costo de reposición de 8.99€(todos estos son valores fijos para todas las películas de este año). El catálogo se encuentra en un archivo CSV llamado films_2020.csv que se puede encontrar en files_for_labla carpeta.

Instrucciones
Agregue las nuevas películas a la base de datos.
Actualizar información sobre rental_duration, rental_rate, y replacement_cost.
Pista
Es posible que tengas que usar los siguientes comandos para configurar la opción de importación masiva en ON:
show variables like 'local_infile';
set global local_infile = 1;
Si la importación masiva produce un error inesperado, también puede utilizar data_import_wizardpara insertar datos en la nueva tabla.
