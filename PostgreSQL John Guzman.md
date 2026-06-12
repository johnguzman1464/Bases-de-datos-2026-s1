# Bases de datos Practica PostgreSQL John Guzman
Se creo una base de datos simple de un sistema universitario utilizando secuencias DML, DLL y PostgreSQL

# PostgreSQL
Utilizamos esta secuencia para generar automaticamente las ID de la tabla estudiantes:
```sql
CREATE SEQUENCE seq_estudiante
START 100
INCREMENT 1;
```

# DDL
Utilizamos estas secuencias para la creacion de las tablas:

# TABLA CARRERA
```sql
CREATE TABLE carrera (
    cod_carrera INT PRIMARY KEY,
    nombre VARCHAR(100),
    facultad VARCHAR(100)
);
```
# TABLA PROFESOR
```sql
CREATE TABLE profesor (
    cedula BIGINT PRIMARY KEY,
    nombre VARCHAR(100),
    departamento VARCHAR(100)
);
```

# TABLA MATERIAS
```sql
CREATE TABLE materias (
    cod_materia INT PRIMARY KEY,
    nombre VARCHAR(100),

    cod_carrera INT,
    cedula_profesor BIGINT,

    FOREIGN KEY (cod_carrera)
        REFERENCES carrera(cod_carrera),

    FOREIGN KEY (cedula_profesor)
        REFERENCES profesor(cedula)
);
```

# TABLA ESTUDIANTE
```sql

CREATE TABLE estudiante (
    cod_estudiante INT PRIMARY KEY
        DEFAULT nextval('seq_estudiante'),

    nombre_completo VARCHAR(150),
    email VARCHAR(100),
    fecha_nacimiento DATE,
    estado VARCHAR(50),

    cod_carrera INT,

    FOREIGN KEY (cod_carrera)
        REFERENCES carrera(cod_carrera)
);

```

# TABLA MATRICULA
```sql
CREATE TABLE matricula (
    cod_estudiante INT,
    cod_materia INT,
    anio INT,
    semestre INT,
    nota_final FLOAT,

    PRIMARY KEY
    (
        cod_estudiante,
        cod_materia,
        anio,
        semestre
    ),

    FOREIGN KEY (cod_estudiante)
        REFERENCES estudiante(cod_estudiante),

    FOREIGN KEY (cod_materia)
        REFERENCES materias(cod_materia)
);
```
# DML
Utilizamos las secuencias para insertas los datos en las tablas:

# DATOS CARRERA
```sql
INSERT INTO carrera VALUES
(1,'Ingenieria de Sistemas','Ingenieria'),
(2,'Ciencia Politica','Ciencias Humanas'),
(3,'Administracion de Empresas','Economia');
```
# DATOS PROFESORES
```sql
INSERT INTO profesor VALUES
(1050607933,'Mario Lopez','Ingenieria'),
(1050607010,'David Wong','Ciencias Politicas'),
(1050607999,'Carlos Ruiz','Administracion');

```
# DATOS MATERIAS 
```sql
INSERT INTO materias VALUES
(10,'Bases de Datos',1,1050607933),
(11,'Programacion Avanzada',1,1050607933),
(20,'Marxismo I',2,1050607010),
(21,'Fundamentos del Estado',2,1050607010),
(30,'Contabilidad',3,1050607999),
(31,'Economia Digital',1,1050607999),
(40,'Inteligencia Artificial',1,1050607933);
```
# DATOS ESTUDIANTES
```sql
INSERT INTO estudiante
(nombre_completo,email,fecha_nacimiento,estado,cod_carrera)
VALUES
('Juan Perez','juan@correo.com','2004-05-12','Activo',1),

('Ana Gomez','ana@correo.com','2003-07-11','Activo',1),

('Pedro Ruiz','pedro@correo.com','2002-09-20','Activo',1),

('Laura Torres','laura@correo.com','2004-01-10','Activo',1),

('Maria Diaz','maria@correo.com','2003-06-15','Activo',2),

('Camilo Vargas','camilo@correo.com','2004-02-22','Activo',2),

('Sofia Castro','sofia@correo.com','2003-10-10','Activo',3);
```
# DATOS MATRICULAS

```sql
INSERT INTO matricula VALUES
(100,10,2024,1,4.7),
(100,11,2024,2,4.9),
(100,31,2025,1,4.8),

(101,10,2024,1,3.8),
(101,11,2024,2,4.0),

(102,10,2024,1,2.5),
(102,11,2024,2,3.0),

(103,10,2024,1,4.5),
(103,31,2024,2,4.6),

(104,20,2024,1,2.6),
(104,21,2024,2,3.2),

(105,20,2024,1,4.3),
(105,21,2024,2,4.4),

(106,30,2024,1,4.9),
(106,30,2025,1,4.7);
```

# Modificaciones a las tablas
Utilizamos consultas DDL, para modificar las tablas de matricula y profesor.

```sql
ALTER TABLE profesor
ADD COLUMN email VARCHAR(100); --añade el campo email

ALTER TABLE matricula
RENAME TO matriculadas; --renombra la tabla
```

Ahora modificamos los datos de la tabla para insertas datos en la colummna de Email para la tabla profesores, usando DML

```sql
UPDATE profesor
SET email = 'maloepa@unal.edu.co'
WHERE cedula = 1050607933;

UPDATE profesor
SET email = 'dawoncito@unal.edu.co'
WHERE cedula = 1050607010;

UPDATE profesor
SET email= 'carlitosR@unal.edu.co'
WHERE cedula =1050607999;

```
# Visualizacion de las tablas
Aqui tenemos la secuencia y como se ve cada tabla en pgAdmin:

```sql
SELECT * FROM carrera;
```
<img width="555" height="218" alt="image" src="https://github.com/user-attachments/assets/b1d899e8-9317-4aa0-b262-f526bd02469b" />

```sql
SELECT * FROM materias;
```
<img width="550" height="313" alt="image" src="https://github.com/user-attachments/assets/f2b393b6-ddb2-4e18-84e5-a53c40d348c8" />

```sql
SELECT * FROM profesor;
```
<img width="602" height="223" alt="image" src="https://github.com/user-attachments/assets/4f25f67d-967e-449f-851d-22f2824f0b6b" />

```sql
SELECT * FROM estudiante;
```
<img width="844" height="286" alt="image" src="https://github.com/user-attachments/assets/d91f708d-c4f1-499b-ba45-c6d722cb1508" />

```sql
SELECT * FROM matriculadas;
```
<img width="565" height="494" alt="image" src="https://github.com/user-attachments/assets/1bf543ab-9d41-4219-889c-304fbe39bb4c" />

# Consulta
Aqui tenemos un ejemplo de una consulta, en la cual nos mostrara los codigos estudiantes y el codigo de la materia en la cual tengan mas de 3.0:
```sql
SELECT cod_estudiante, cod_materia
FROM matriculadas
WHERE nota_final >= 3.0;
```
Asi se ve el pgAdmin:

<img width="338" height="441" alt="image" src="https://github.com/user-attachments/assets/4a475375-c4e8-42eb-8ef8-10cb4fbe537c" />


Ahora continuamos con consultas mas avanzadas pertenecientes a los JOINS:

[Ir a Consultas Avanzadas (Joins)](CONSULTAS_JOINS.md)


