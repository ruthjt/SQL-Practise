# SQL-Practise
USE 001test;


#Creación de tablas
CREATE TABLE vuelos (
idv INTEGER,
nombre_mision VARCHAR (15),
fecha_inicio DATE,
origen VARCHAR (15),
destino VARCHAR (15)
);

DROP TABLE vuelos;
DROP TABLE astronautas;
DROP TABLE estrella;

CREATE TABLE astronautas (
ida INTEGER,
nombre_astronauta VARCHAR (15),
pais_nacimiento VARCHAR (15),
idv INTEGER
);

CREATE TABLE estrella (
ide INTEGER,
nombre_estrella VARCHAR (15),
diametro DOUBLE
);

CREATE TABLE pasajeros (
idv INTEGER,
ida INTEGER,
ide INTEGER
);

#Creación de pk
ALTER TABLE vuelos ADD PRIMARY KEY (idv);
ALTER TABLE astronautas ADD PRIMARY KEY (ida);
ALTER TABLE estrella ADD PRIMARY KEY (ide);
ALTER TABLE pasajeros ADD PRIMARY KEY(idv);

#Creación de fk
ALTER TABLE vuelos ADD FOREIGN KEY (ida) REFERENCES astronautas (ida);
ALTER TABLE vuelos ADD FOREIGN KEY (ide) REFERENCES estrella (ide);
ALTER TABLE astronautas ADD FOREIGN KEY (idv) REFERENCES vuelos (idv);
ALTER TABLE pasajeros ADD FOREIGN KEY (ida) REFERENCES astronautas(ida);


SELECT * FROM vuelos
INSERT INTO astronautas (ida, nombre_astronauta, pais_nacimiento)
VALUES (1, 'Neil Amstrong', 'Estados Unidos'),
		(2, 'Edwin Aldrin', 'Estados Unidos'),
		(3, 'Michael Collins', 'Estados Unidos' );
		
INSERT INTO vuelos (idv, nombre_mision, fecha_inicio, origen, destino)
VALUES (1, 'Apolo 11', '1969-07-16', 1, 2);

INSERT INTO estrella (ide, nombre_estrella, diametro)
VALUES (1, 'Tierra', 12742),
	(2, 'Marte', 6779),
	(3, 'Jupiter', 139822),
	(4, 'Luna', 3474),
	(5, 'Io', 3642),
	(6, 'Ganimedes', 5268);
	
INSERT INTO pasajeros (idv, ida, ide)
VALUES (1, 1, 1),
		(1, 2, 2),
		(1, 3, 3);
		
SELECT * FROM vuelos;

SELECT
  e1.nombre_estrella AS "Lugar de Origen",
  e2.nombre_estrella AS "Lugar de Destino",
  v.fecha_inicio AS "Fecha de Inicio",
  a.nombre_astronauta AS "Nombre del Astronauta"
FROM
  vuelos v
INNER JOIN
  estrella e1 ON v.origen = e1.ide
INNER JOIN
  estrella e2 ON v.destino = e2.ide
INNER JOIN
  pasajeros p ON v.idv = p.idv
INNER JOIN
  astronautas a ON p.ida = a.ida;
