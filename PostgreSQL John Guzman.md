# Bases de datos Practica PostgreSQL John Guzman
Se creo una base de datos simple de un sistema universitario utilizando secuencias DML, DLL y PostgreSQL

# PostgreSQL
Utilizamos esta secuencia para generar automaticamente las ID de la tabla estudiantes:
```sql
CREATE SEQUENCE seq_estudiante
    START WITH 100
    INCREMENT BY 1
    MINVALUE 100;
```

# DDL
Utilizamos estas secuencias para la creacion de las tablas:
```sql
CREATE TABLE carrera (
    cod_carrera INT PRIMARY KEY,
    nombre VARCHAR(100),
    facultad VARCHAR(100)
);

CREATE TABLE materias (
    cod_materia INT PRIMARY KEY,
    nombre VARCHAR(100),
    facultad VARCHAR(100)
);

CREATE TABLE profesor (
    cedula BIGINT PRIMARY KEY,
    nombre VARCHAR(100),
    departamento VARCHAR(100)
);

CREATE TABLE estudiante (
    cod_estudiante INT PRIMARY KEY
        DEFAULT nextval('seq_estudiante'), --aqui se usa el valor generado por la secuencia PostgreSQL
    nombre_completo VARCHAR(150),
    email VARCHAR(100),
    fecha_nacimiento DATE,
    estado VARCHAR(50),
    cod_carrera INT,

    CONSTRAINT fk_estudiante_carrera
        FOREIGN KEY (cod_carrera)
        REFERENCES carrera(cod_carrera)
);

CREATE TABLE matricula (
    cod_estudiante INT,
    cod_materia INT,
    anio INT,
    semestre INT,
    nota_final FLOAT,

    CONSTRAINT pk_matricula
        PRIMARY KEY (
            cod_estudiante,
            cod_materia,
            anio,
            semestre
        ),

    CONSTRAINT fk_matricula_estudiante
        FOREIGN KEY (cod_estudiante)
        REFERENCES estudiante(cod_estudiante),

    CONSTRAINT fk_matricula_materia
        FOREIGN KEY (cod_materia)
        REFERENCES materias(cod_materia)
);
```
# DML
Utilizamos las secuencias para insertas los datos en las tablas:

```sql
INSERT INTO carrera VALUES
(1, 'Ingenieria de Sistemas', 'Ingenieria'),
(2, 'Ciencia Politica', 'Ciencias Humanas');

INSERT INTO materias VALUES
(10, 'Bases de Datos', 'Ingenieria'),
(20, 'Marxismo I', 'Ciencias Politicas'),
(21, 'Fundamentos del Estado', 'Ciencias Politicas');

INSERT INTO profesor VALUES
(1050607933, 'Mario Lopez', 'Ingenieria'),
(1050607010, 'David Wong', 'Ciencias Politicas');

INSERT INTO estudiante
(nombre_completo, email, fecha_nacimiento, estado, cod_carrera)
VALUES
('Juan Perez', 'juan@correo.com', '2004-05-12', 'Activo', 1);

INSERT INTO matricula VALUES
(100, 10, 2026, 1, 4.7);

INSERT INTO matricula VALUES
(100, 20, 2024, 2, 2.6);

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

```
# Visualizacion de las tablas
Aqui tenemos la secuencia y como se ve cada tabla en pgAdmin:

```sql
SELECT * FROM carrera;
```
<img width="458" height="162" alt="image" src="https://github.com/user-attachments/assets/c520fb6f-b105-48bc-9071-069aa69c9765" />

```sql
SELECT * FROM materias;
```
<img width="459" height="190" alt="image" src="https://github.com/user-attachments/assets/32f06d51-9aa0-48ce-9a38-2de9e0a6a250" />

```sql
SELECT * FROM profesor;
```
<img width="604" height="163" alt="image" src="https://github.com/user-attachments/assets/eafc756c-ce3a-47d5-9cab-140a9d141990" />


```sql
SELECT * FROM estudiante;
```
<img width="841" height="134" alt="image" src="https://github.com/user-attachments/assets/fa58d997-04b7-4bc1-aef9-01d41a51bc48" />

```sql
SELECT * FROM matriculadas;
```
<img width="571" height="165" alt="image" src="https://github.com/user-attachments/assets/39106c4e-ad82-444a-a24b-d81ff1248606" />

# Consulta
Aqui tenemos un ejemplo de una consulta, en la cual nos mostrara los codigos estudiantes y el codigo de la materia en la cual tengan mas de 3.0:
```sql
SELECT cod_estudiante, cod_materia
FROM matriculadas
WHERE nota_final >= 3.0;
```
Asi se ve el pgAdmin.

<img width="336" height="138" alt="image" src="https://github.com/user-attachments/assets/55b6d732-39b9-4613-9e21-afe6e9765a97" />

