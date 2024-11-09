```sql
-- Calcular el promedio de la longitud 
SELECT AVG(LENGTH(apellido)) FROM actor;

-- Seleccionar actores con longitud de 'nombre' mayor al promedio
SELECT * 
FROM actor 
WHERE LENGTH(nombre) > (SELECT AVG(LENGTH(nombre)) FROM actor);

-- Encontrar actores que han participado en películas de la categoría comedia
SELECT a.nombre, a.apellido
FROM actor AS a
JOIN pelicula_actor AS fa ON a.id_actor = fa.id_actor
JOIN pelicula_categoria AS fc ON fa.id_pelicula = fc.id_pelicula
JOIN categoria AS c ON fc.id_categoria = c.id_categoria
WHERE c.nombre = "Comedia";

-- Encontrar los nombres de las películas que nunca se han rantado
SELECT f.titulo
FROM pelicula AS f
LEFT JOIN inventario AS i ON f.id_pelicula = i.id_pelicula
LEFT JOIN renta AS r ON i.id_inventario = r.id_inventario
WHERE r.id_renta IS NULL;

-- Muestra los títulos de las películas y sus categorías
SELECT f.titulo, c.nombre AS categoria_nombre
FROM pelicula AS f
INNER JOIN pelicula_categoria AS fc ON f.id_pelicula = fc.id_pelicula
INNER JOIN categoria AS c ON fc.id_categoria = c.id_categoria;

-- Encontrar el título de la película y la cantidad de veces que han sido alquiladas
SELECT f.titulo, COUNT(r.id_renta) AS cantidad_rentas
FROM pelicula AS f
LEFT JOIN inventario AS i ON f.id_pelicula = i.id_pelicula
LEFT JOIN renta AS r ON i.id_inventario = r.id_inventario
GROUP BY f.titulo;

-- Mostrar los actores y los títulos de las películas en las que han participado
SELECT a.nombre, a.apellido, f.titulo
FROM actor AS a
JOIN pelicula_actor AS fa ON a.id_actor = fa.id_actor
JOIN pelicula AS f ON fa.id_pelicula = f.id_pelicula;

-- Seleccionar todas las ciudades donde hay empleados o clientes
SELECT DISTINCT ciudad
FROM ciudad
JOIN direccion ON ciudad.id_ciudad = direccion.id_ciudad
JOIN personal ON direccion.id_direccion = personal.id_direccion
UNION
SELECT ciudad
FROM ciudad
WHERE id_ciudad IN (
    SELECT id_ciudad 
    FROM direccion 
    WHERE id_direccion IN (
        SELECT
        id_direccion
        FROM cliente
    )
);

-- Se crea una vista que muestra los nombres de los actores con 'last_update' después del año 2020
CREATE VIEW prueba AS 
SELECT nombre, apellido
FROM actor 
WHERE YEAR(ultima_actualizacion) > 2020;

-- Insertar un nuevo actor llamado "Lucio Hernandez" con la fecha actual de 'last_update'
INSERT INTO actor (apellido1, apellido2, ultima_actualizacion) 
VALUES ("Lucio", "Hernandez", NOW());
