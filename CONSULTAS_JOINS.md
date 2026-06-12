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
Listar todos los estudiantes aunque no tengan matrículas registradas.

```sql
SELECT e.nombre_completo,
       ma.cod_materia
FROM estudiante e
LEFT JOIN matriculadas ma
ON e.cod_estudiante=ma.cod_estudiante;
```

VISUALIZACION:

<img width="336" height="494" alt="image" src="https://github.com/user-attachments/assets/15d0fc46-24af-4d65-ac13-4d65793c7336" />

# CONSULTA #6
Mostrar las materias que no tienen ningún estudiante matriculado. 

```sql
SELECT m.nombre
FROM materias m
LEFT JOIN matriculadas ma
ON m.cod_materia=ma.cod_materia
WHERE ma.cod_materia IS NULL;
```

VISUALIZACION:

<img width="332" height="138" alt="image" src="https://github.com/user-attachments/assets/f107c8de-dce6-43f5-9920-33e48f4be2ae" />

# CONSULTA #7
Contar cuántos estudiantes hay en cada carrera.

```sql
SELECT c.nombre,
       COUNT(*) cantidad
FROM estudiante e
INNER JOIN carrera c
ON e.cod_carrera=c.cod_carrera
GROUP BY c.nombre;
```

VISUALIZACION:

<img width="330" height="187" alt="image" src="https://github.com/user-attachments/assets/c054580a-d818-49ef-97c8-b944fb9bd9dc" />

# CONSULTA #8
Calcular el promedio de notas por materia.

```sql
SELECT m.nombre,
       AVG(ma.nota_final) promedio
FROM matriculadas ma
INNER JOIN materias m
ON ma.cod_materia=m.cod_materia
GROUP BY m.nombre;
```

VISUALIZACION:

<img width="346" height="262" alt="image" src="https://github.com/user-attachments/assets/8f2673a3-d4ec-41ec-a6bc-f37b486911eb" />

# CONSULTA #9
Mostrar el promedio de notas por estudiante, ordenado de mayor a menor.

```sql
SELECT e.nombre_completo,
       AVG(ma.nota_final) promedio
FROM estudiante e
INNER JOIN matriculadas ma
ON e.cod_estudiante=ma.cod_estudiante
GROUP BY e.cod_estudiante,e.nombre_completo
ORDER BY promedio DESC;
```

VISUALIZACION:

<img width="341" height="294" alt="image" src="https://github.com/user-attachments/assets/d8daaefb-e455-4ea6-95f6-2064e6c92529" />

# CONSULTA #10
Mostrar solo los estudiantes con promedio general mayor o igual a 4.0.

```sql
SELECT e.nombre_completo,
       AVG(ma.nota_final) promedio
FROM estudiante e
INNER JOIN matriculadas ma
ON e.cod_estudiante=ma.cod_estudiante
GROUP BY e.cod_estudiante,e.nombre_completo
HAVING AVG(ma.nota_final) >= 4.0;
```

VISUALIZACION:

<img width="334" height="206" alt="image" src="https://github.com/user-attachments/assets/bbb9f830-d719-4361-8115-c23ab91fe8c9" />

# CONSULTA #11 
Mostrar las carreras que tienen más de 3 estudiantes matriculados en total.

```sql
SELECT c.nombre,
       COUNT(*) total
FROM estudiante e
INNER JOIN carrera c
ON e.cod_carrera=c.cod_carrera
GROUP BY c.nombre
HAVING COUNT(*) > 3;
```

VISUALIZACION:

<img width="340" height="418" alt="image" src="https://github.com/user-attachments/assets/de0abfbc-ea6e-4502-bccf-464524a1126e" />

# CONSULTA #12
Mostrar por cada profesor cuántas materias ha dictado en total.

```sql
SELECT p.nombre,
       COUNT(*) materias
FROM profesor p
INNER JOIN materias m
ON p.cedula=m.cedula_profesor
GROUP BY p.cedula,p.nombre;
```

VISUALIZACION:

<img width="332" height="195" alt="image" src="https://github.com/user-attachments/assets/056b5ae7-c5b4-4c82-bc4c-efe9b95db425" />

# CONSULTA #13
Mostrar el año y semestre con mayor cantidad de matrículas registradas

```sql
SELECT anio,
       semestre,
       COUNT(*) total
FROM matriculadas
GROUP BY anio,semestre
ORDER BY total DESC
LIMIT 1;
```

VISUALIZACION:

<img width="332" height="139" alt="image" src="https://github.com/user-attachments/assets/c5a07931-1d8c-4401-b30a-6334d6dce90c" />

# CONSULTA #14
Mostrar las materias cuyo promedio de nota sea inferior a 3.5. 

```sql
SELECT m.nombre,
       AVG(ma.nota_final) promedio
FROM matriculadas ma
INNER JOIN materias m
ON ma.cod_materia=m.cod_materia
GROUP BY m.nombre
HAVING AVG(ma.nota_final) < 3.5;
```

VISUALIZACION:

<img width="330" height="145" alt="image" src="https://github.com/user-attachments/assets/550f1bb8-11c5-4a06-943f-e78e34950df0" />

# CONSULTA #15
Listar los estudiantes cuya nota en alguna materia supera el promedio general de todas las matrículas. 

```sql
SELECT DISTINCT e.nombre_completo
FROM estudiante e
INNER JOIN matriculadas ma
ON e.cod_estudiante=ma.cod_estudiante
WHERE ma.nota_final >
(
    SELECT AVG(nota_final)
    FROM matriculadas
);
```

VISUALIZACION:

<img width="332" height="214" alt="image" src="https://github.com/user-attachments/assets/1aebe964-4120-478d-97e8-c8cec6703fea" />

# CONSULTA #16
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #17
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #18
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #19
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #20
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #21
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #22
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #23
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #24
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #25
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #26
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #27
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #28
no se we

```sql

```

VISUALIZACION:

-

# CONSULTA #29
no se we

```sql

```

VISUALIZACION:

-


# CONSULTA #30
no se we

```sql

```

VISUALIZACION:

-
