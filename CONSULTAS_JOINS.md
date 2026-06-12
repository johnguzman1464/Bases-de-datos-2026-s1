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
Listar los estudiantes que tienen nota mayor al promedio de notas de su propia carrera.

```sql
SELECT DISTINCT e.nombre_completo
FROM estudiante e
INNER JOIN matriculadas ma
ON e.cod_estudiante=ma.cod_estudiante
WHERE ma.nota_final >
(
    SELECT AVG(ma2.nota_final)
    FROM matriculadas ma2
    INNER JOIN estudiante e2
    ON ma2.cod_estudiante=e2.cod_estudiante
    WHERE e2.cod_carrera=e.cod_carrera
);
```

VISUALIZACION:

<img width="331" height="209" alt="image" src="https://github.com/user-attachments/assets/8acbaf8e-67bc-43b3-8f54-a5ca9a0e1a08" />

# CONSULTA #17
Mostrar los estudiantes que nunca han reprobado (ninguna nota menor a 3.0). 

```sql
SELECT e.nombre_completo
FROM estudiante e
WHERE NOT EXISTS
(
    SELECT *
    FROM matriculadas ma
    WHERE ma.cod_estudiante=e.cod_estudiante
    AND ma.nota_final < 3.0
);
```

VISUALIZACION:

<img width="334" height="244" alt="image" src="https://github.com/user-attachments/assets/eee322c8-6450-41b9-9fe0-ae83952236fd" />

# CONSULTA #18
Mostrar la materia con la nota más alta registrada en toda la universidad. 

```sql
SELECT m.nombre,
       ma.nota_final
FROM matriculadas ma
INNER JOIN materias m
ON ma.cod_materia=m.cod_materia
WHERE ma.nota_final=
(
    SELECT MAX(nota_final)
    FROM matriculadas
);
```

VISUALIZACION:

<img width="332" height="161" alt="image" src="https://github.com/user-attachments/assets/301660c9-af19-41cb-a1c6-f769dc5fb38f" />

# CONSULTA #19
Listar los estudiantes que han cursado más materias que el promedio de materias cursadas por todos los estudiantes. 

```sql
SELECT e.nombre_completo
FROM estudiante e
INNER JOIN matriculadas ma
ON e.cod_estudiante=ma.cod_estudiante
GROUP BY e.cod_estudiante,e.nombre_completo
HAVING COUNT(*) >
(
    SELECT AVG(cantidad)
    FROM
    (
        SELECT COUNT(*) cantidad
        FROM matriculadas
        GROUP BY cod_estudiante
    ) t
);
```

VISUALIZACION:

<img width="335" height="141" alt="image" src="https://github.com/user-attachments/assets/07325d23-85d7-479a-9c12-ef01ca9e9ac3" />

# CONSULTA #20
Mostrar los profesores que dictan materias en más de una carrera.

```sql
SELECT p.nombre
FROM profesor p
INNER JOIN materias m
ON p.cedula=m.cedula_profesor
GROUP BY p.cedula,p.nombre
HAVING COUNT(DISTINCT m.cod_carrera) > 1;
```

VISUALIZACION:

<img width="331" height="143" alt="image" src="https://github.com/user-attachments/assets/de0913dd-81fa-4232-8f2e-355188943826" />

# CONSULTA #21
Asignar un ranking de notas por materia, donde el estudiante con mayor nota queda en puesto 1. 

```sql
SELECT m.nombre,
       e.nombre_completo,
       ma.nota_final,
       RANK() OVER
       (
           PARTITION BY m.cod_materia
           ORDER BY ma.nota_final DESC
       ) ranking
FROM matriculadas ma
INNER JOIN estudiante e
ON ma.cod_estudiante=e.cod_estudiante
INNER JOIN materias m
ON ma.cod_materia=m.cod_materia;
```

VISUALIZACION:

<img width="561" height="493" alt="image" src="https://github.com/user-attachments/assets/f39dee25-01a7-481e-ba2d-d7c83464b8d5" />

# CONSULTA #22
Mostrar la nota de cada estudiante junto con el promedio de notas de su carrera en la misma fila.

```sql
SELECT e.nombre_completo,
       ma.nota_final,
       AVG(ma.nota_final)
       OVER(PARTITION BY e.cod_carrera)
       promedio_carrera
FROM estudiante e
INNER JOIN matriculadas ma
ON e.cod_estudiante=ma.cod_estudiante;
```

VISUALIZACION:

<img width="463" height="492" alt="image" src="https://github.com/user-attachments/assets/e99297a0-794d-44dc-8dba-4bebeb7c5372" />

# CONSULTA #23
Mostrar la nota actual de cada estudiante junto con la nota de su matrícula anterior. 

```sql
SELECT cod_estudiante,
       nota_final,
       LAG(nota_final)
       OVER(
           PARTITION BY cod_estudiante
           ORDER BY anio,semestre
       ) nota_anterior
FROM matriculadas;
```

VISUALIZACION:

<img width="405" height="491" alt="image" src="https://github.com/user-attachments/assets/77845e80-d250-4039-81eb-e288b470d4a2" />

# CONSULTA #24
Mostrar la nota actual y la nota de la siguiente matrícula para ver si el estudiante mejoró o bajó. 

```sql
SELECT cod_estudiante,
       nota_final,
       LEAD(nota_final)
       OVER(
           PARTITION BY cod_estudiante
           ORDER BY anio,semestre
       ) nota_siguiente
FROM matriculadas;
```

VISUALIZACION:

<img width="413" height="489" alt="image" src="https://github.com/user-attachments/assets/b806e6f9-5a03-4a96-95f3-4b39ac82d397" />

# CONSULTA #25
Mostrar el ranking general de estudiantes ordenado por promedio de mayor a menor. 

```sql
SELECT *,
       RANK() OVER
       (
           ORDER BY promedio DESC
       ) ranking_general
FROM
(
    SELECT cod_estudiante,
           AVG(nota_final) promedio
    FROM matriculadas
    GROUP BY cod_estudiante
) t;
```

VISUALIZACION:

<img width="421" height="293" alt="image" src="https://github.com/user-attachments/assets/8308fa82-164b-427f-aa4b-a4734faaa994" />

# CONSULTA #26
Calcular la diferencia entre la nota actual y la nota anterior de cada estudiante para ver su progreso.

```sql
SELECT cod_estudiante,
       nota_final,
       nota_final -
       LAG(nota_final)
       OVER(
           PARTITION BY cod_estudiante
           ORDER BY anio,semestre
       ) diferencia
FROM matriculadas;
```

VISUALIZACION:

<img width="432" height="492" alt="image" src="https://github.com/user-attachments/assets/5cc94776-8072-4115-b2ef-6351299e0cd7" />

# CONSULTA #27
Numerar las matrículas de cada estudiante en orden cronológico. 

```sql
SELECT *,
       ROW_NUMBER()
       OVER(
           PARTITION BY cod_estudiante
           ORDER BY anio,semestre
       ) numero_matricula
FROM matriculadas;
```

VISUALIZACION:

<img width="691" height="488" alt="image" src="https://github.com/user-attachments/assets/ca29266c-cabe-4e11-9559-b5461c4e6620" />

# CONSULTA #28
Mostrar la mejor nota acumulada de cada estudiante a medida que avanza en sus matrículas.

```sql
SELECT cod_estudiante,
       nota_final,
       MAX(nota_final)
       OVER(
           PARTITION BY cod_estudiante
           ORDER BY anio,semestre
           ROWS UNBOUNDED PRECEDING
       ) mejor_hasta_ahora
FROM matriculadas;
```

VISUALIZACION:

<img width="422" height="488" alt="image" src="https://github.com/user-attachments/assets/ff974bb6-52af-47d8-97f1-6c3d659d90d6" />

# CONSULTA #29
Por cada carrera mostrar: total de estudiantes, promedio general de notas y nombre de alguna materia de esa carrera. 

```sql
SELECT c.nombre,
       COUNT(DISTINCT e.cod_estudiante) total_estudiantes,
       AVG(ma.nota_final) promedio_general,
       MIN(m.nombre) materia_ejemplo
FROM carrera c
LEFT JOIN estudiante e
ON c.cod_carrera=e.cod_carrera
LEFT JOIN materias m
ON c.cod_carrera=m.cod_carrera
LEFT JOIN matriculadas ma
ON m.cod_materia=ma.cod_materia
GROUP BY c.nombre;
```

VISUALIZACION:

<img width="638" height="191" alt="image" src="https://github.com/user-attachments/assets/ea09fca4-bb2f-45a5-adec-38e29bc9a0ec" />

# CONSULTA #30
Listar el estudiante con mayor promedio por carrera usando funciones de ventana.

```sql
WITH Promedios AS
(
    SELECT c.nombre AS carrera,
           e.cod_estudiante,
           e.nombre_completo,
           AVG(ma.nota_final) promedio,

           RANK() OVER
           (
               PARTITION BY c.cod_carrera
               ORDER BY AVG(ma.nota_final) DESC
           ) posicion

    FROM estudiante e
    INNER JOIN carrera c
    ON e.cod_carrera=c.cod_carrera

    INNER JOIN matriculadas ma
    ON e.cod_estudiante=ma.cod_estudiante

    GROUP BY
        c.cod_carrera,
        c.nombre,
        e.cod_estudiante,
        e.nombre_completo
)
SELECT *
FROM Promedios
WHERE posicion = 1;
```

VISUALIZACION:

<img width="696" height="189" alt="image" src="https://github.com/user-attachments/assets/b1e1d5c9-6983-403f-99e8-74cf3339f972" />
