# CONSULTAS AVANZADAS (JOINS)

A continuacion se trabajan varios ejercicios de consultas en base a nuestro trabajo anterior:

# CONSULTA #1
Listar el nombre completo de cada estudiante y el nombre de su carrera.

```sql
SELECT e.nombre_completo,
       c.nombre AS carrera
FROM estudiante e
INNER JOIN carrera c
ON e.cod_carrera = c.cod_carrera;
```

VISUALIZACION:

<img width="548" height="316" alt="image" src="https://github.com/user-attachments/assets/cf3d5d61-6236-4dd8-9eed-1da5451487e4" />


# CONSULTA #2
Listar todas las materias con el nombre de la carrera a la que pertenecen. 

```sql
SELECT m.nombre AS materia,
       c.nombre AS carrera
FROM materias m
INNER JOIN carrera c
ON m.cod_carrera = c.cod_carrera;
```

VISUALIZACION:

<img width="546" height="323" alt="image" src="https://github.com/user-attachments/assets/cfb0f744-8550-49bd-acca-3546d9273e16" />

# CONSULTA #3
Mostrar el nombre del estudiante, la materia que cursó y la nota obtenida. 

```sql
SELECT e.nombre_completo,
       m.nombre AS materia,
       ma.nota_final
FROM matriculadas ma
INNER JOIN estudiante e
ON ma.cod_estudiante=e.cod_estudiante
INNER JOIN materias m
ON ma.cod_materia=m.cod_materia;
```

VISUALIZACION:

<img width="559" height="518" alt="image" src="https://github.com/user-attachments/assets/b819f341-c271-4ee0-800e-d6b4406b2a54" />

# CONSULTA #4
Mostrar el nombre del estudiante, la materia, el profesor que la dictó y la nota. 

```sql
SELECT e.nombre_completo,
       m.nombre AS materia,
       p.nombre AS profesor,
       ma.nota_final
FROM matriculadas ma
INNER JOIN estudiante e
ON ma.cod_estudiante=e.cod_estudiante
INNER JOIN materias m
ON ma.cod_materia=m.cod_materia
INNER JOIN profesor p
ON m.cedula_profesor=p.cedula;
```

VISUALIZACION:

<img width="638" height="490" alt="image" src="https://github.com/user-attachments/assets/b7fc07c2-986e-4858-a538-364d6d089fa0" />

# CONSULTA #5
no se we

```sql

```

VISUALIZACION:
-
