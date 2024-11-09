```sql
-- Tabla de adminitrador
CREATE TABLE administrador (
    id_administrador VARCHAR(255) PRIMARY KEY,
    nombre_usuario VARCHAR(255),
    password VARCHAR(255)
);

-- Tabla de tiendas
CREATE TABLE tienda (
    id_tienda VARCHAR(255) PRIMARY KEY,
    id_administrador VARCHAR(255),
    nombre VARCHAR(255),
    estado1 VARCHAR(255),
    FOREIGN KEY (id_administrador) REFERENCES administrador(id_administrador)
);

-- Tabla de usuarios
CREATE TABLE usuario (
    id_usuario VARCHAR(255) PRIMARY KEY,
    id_tienda VARCHAR(255),
    nombre_usuario VARCHAR(255),
    contraseña VARCHAR(255),
    estado2 INT,
    FOREIGN KEY (id_tienda) REFERENCES tienda(id_tienda)
);

-- Tabla de clientes
CREATE TABLE cliente (
    id_cliente VARCHAR(255) PRIMARY KEY,
    telefono VARCHAR(255),
    contraseña VARCHAR(255),
    estado3 INT
);

-- Tabla de puntos de tarjeta
CREATE TABLE tarjeta_puntos (
    id_tarjeta VARCHAR(255) PRIMARY KEY,
    id_cliente VARCHAR(255),
    id_tienda VARCHAR(255),
    puntos DECIMAL(12, 2),  
    ultima_actualizacion DATE,
    estado4 INT,
    FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente),
    FOREIGN KEY (id_tienda) REFERENCES tienda(id_tienda)
);

-- Tabla de transacciones
CREATE TABLE transaccion (
    id_transaccion VARCHAR(255) PRIMARY KEY,
    id_tarjeta VARCHAR(255),
    cantidad DECIMAL(12, 2),  
    puntos1 DECIMAL(12, 2),  
    fecha DATE,
    FOREIGN KEY (id_tarjeta) REFERENCES tarjeta_puntos(id_tarjeta)
);

-- Vista para mostrar el nombre y estado de cada tienda
CREATE VIEW nombre_vista AS 
SELECT nombre, estado1 FROM tienda;

-- Vista para mostrar información de administradores y sus tiendas
CREATE VIEW admin_tienda_info AS
SELECT a.nombre_usuario AS admin_nombre, 
       s.nombre AS tienda_nombre, 
       s.estado1 AS tienda_estado
FROM administrador AS a 
JOIN tienda AS s ON s.id_administrador = a.id_administrador;

-- Vista que muestra el ID del cliente, su teléfono, el nombre de la tienda y los puntos de su tarjeta
CREATE VIEW cliente_tarjeta_puntos_tienda_info AS
SELECT c.id_cliente AS id_del_cliente,
       c.telefono AS telefono_del_cliente,
       p.puntos AS puntos_de_tarjeta,
       s.name AS nombre_de_la_tienda
FROM cliente AS c
JOIN tarjeta_puntos AS p ON c.id_cliente = p.id_cliente
JOIN tienda AS s ON s.id_tienda = p.id_tienda;

-- Vista que muestra el nombre de las tiendas y la cantidad de clientes que tiene cada una
CREATE VIEW tienda_cliente_cantidad_info AS  
SELECT COUNT(c.id_cliente) AS cantidad_clientes,  
       s.nombre AS nombre_de_la_tienda
FROM tienda AS s
LEFT JOIN tarjeta_puntoss AS p ON s.id_tienda = p.id_tienda
LEFT JOIN cliente AS c ON c.id_cliente = p.id_cliente
GROUP BY s.nombre;

-- Vista que muestra el nombre de cada tienda y el monto total de ventas generadas en ellas
CREATE VIEW Monto_tienda AS
SELECT s.nombre AS nombre_tienda,
       SUM(t.cantidad) AS monto_ventas
FROM tienda AS s
JOIN tarjeta_puntos AS p ON s.id_tienda = p.id_tienda
JOIN transaction AS t ON p.id_tarjeta = t.id_tienda
GROUP BY s.nombre;
