### Bloque 1

##### Consultas

1. Listar los nombres de los usuarios

   ```sql
   SELECT nombre FROM tblUsuarios;
   +-----------+
   | nombre    |
   +-----------+
   | BRENDA    |
   | OSCAR     |
   | JOSE      |
   | LUIS      |
   | LUIS      |
   | DANIEL    |
   | JAQUELINE |
   | ROMAN     |
   | BLAS      |
   | JESSICA   |
   | DIANA     |
   | RICARDO   |
   | VALENTINA |
   | BRENDA    |
   | LUCIA     |
   | JUAN      |
   | ELPIDIO   |
   | JESSICA   |
   | LETICIA   |
   | LUIS      |
   | HUGO      |
   +-----------+
   
   ```

2. Calcular el saldo máximo de los usuarios de sexo “Mujer”

     ```sql
     SELECT sexo,max(saldo)  FROM tblUsuarios where sexo='M';
     +------+------------+
     | sexo | max(saldo) |
     +------+------------+
     | M    |        500 |
     +------+------------+
     
     ```

3. Listar nombre y teléfono de los usuarios con teléfono NOKIA, BLACKBERRY o SONY

     ```sql
     select nombre,telefono,marca from tblUsuarios where marca='NOKIA' or marca='BLACKBERRY' or marca='SONY';
     +-----------+--------------+------------+
     | nombre    | telefono     | marca      |
     +-----------+--------------+------------+
     | JOSE      | 655-143-3922 | NOKIA      |
     | LUIS      | 655-100-8260 | NOKIA      |
     | DANIEL    | 655-145-2586 | SONY       |
     | JAQUELINE | 655-330-5514 | BLACKBERRY |
     | DIANA     | 655-143-3952 | SONY       |
     | VALENTINA | 655-137-4253 | BLACKBERRY |
     | LUCIA     | 655-145-4992 | BLACKBERRY |
     | JESSICA   | 655-330-5143 | SONY       |
     | LETICIA   | 655-143-4019 | BLACKBERRY |
     | LUIS      | 655-100-5085 | SONY       |
     +-----------+--------------+------------+
     ```

4. Contar los usuarios sin saldo o inactivos

     ```sql
     select saldo,activo,count(*) as inactivos_sinSaldo  from tblUsuarios where saldo=0 or activo=0 group by saldo, activo;
     +-------+--------+--------------------+
     | saldo | activo | inactivos_sinSaldo |
     +-------+--------+--------------------+
     |     0 |      1 |                  3 |
     |    50 |      0 |                  2 |
     |   100 |      0 |                  1 |
     |     0 |      0 |                  1 |
     +-------+--------+--------------------+
     
     ```

5. Listar el login de los usuarios con nivel 1, 2 o 3

     ```sql
     select usuario,email,nivel from tblUsuarios where nivel=1 or nivel=2 or nivel=3;
     +---------+---------------------+-------+
     | usuario | email               | nivel |
     +---------+---------------------+-------+
     | BRE2271 | brenda@live.com     |     2 |
     | OSC4677 | oscar@gmail.com     |     3 |
     | JOS7086 | francisco@gmail.com |     3 |
     | LUI7072 | luis@hotmail.com    |     1 |
     | ROM6520 | roman@gmail.com     |     2 |
     | JES4752 | jessica@hotmail.com |     1 |
     | DIA6570 | diana@live.com      |     1 |
     | RIC8283 | ricardo@hotmail.com |     2 |
     | BRE8106 | brenda2@gmail.com   |     3 |
     | LUC4982 | lucia@gmail.com     |     3 |
     | ELP2984 | elpidio@outlook.com |     1 |
     | JES9640 | jessica2@live.com   |     3 |
     | LET4015 | leticia@yahoo.com   |     2 |
     | LUI1076 | luis2@live.com      |     3 |
     | HUG5441 | hugo@live.com       |     2 |
     +---------+---------------------+-------+
     15 rows in set (0,00 sec)
     
     
     ```

6. Listar los números de teléfono con saldo menor o igual a 300

     ```sql
      select telefono,saldo from tblUsuarios where saldo <= 300;
     +--------------+-------+
     | telefono     | saldo |
     +--------------+-------+
     | 655-330-5736 |   100 |
     | 655-143-4181 |     0 |
     | 655-143-3922 |   150 |
     | 655-137-1279 |    50 |
     | 655-100-8260 |    50 |
     | 655-145-2586 |   100 |
     | 655-330-5514 |     0 |
     | 655-330-3263 |    50 |
     | 655-330-3871 |   100 |
     | 655-143-3952 |   100 |
     | 655-145-6049 |   150 |
     | 655-137-4253 |    50 |
     | 655-100-1351 |   150 |
     | 655-145-4992 |     0 |
     | 655-100-6517 |     0 |
     | 655-330-5143 |   200 |
     | 655-143-4019 |   100 |
     | 655-100-5085 |   150 |
     +--------------+-------+
     18 rows in set (0,00 sec)
     
     ```

7. Calcular la suma de los saldos de los usuarios de la compañia telefónica NEXTEL

     ```sql
      select sum(saldo) usuario,compañia from tblUsuarios where compañia='NEXTEL';
     +---------+-----------+
     | usuario | compañia  |
     +---------+-----------+
     |     150 | NEXTEL    |
     +---------+-----------+
     1 row in set (0,00 sec)
     
     ```

8. Contar el número de usuarios por compañía telefónica

     ```sql
      select compañia,count(*) as usuarios_Compañia  from tblUsuarios group by compañia;
     +-----------+--------------------+
     | compañia  | usuarios_Compañia  |
     +-----------+--------------------+
     | IUSACELL  |                  6 |
     | TELCEL    |                  3 |
     | MOVISTAR  |                  2 |
     | UNEFON    |                  5 |
     | AXEL      |                  2 |
     | AT&T      |                  2 |
     | NEXTEL    |                  1 |
     +-----------+--------------------+
     7 rows in set (0,00 sec)
     
     ```

9. Contar el número de usuarios por nivel

     ```sql
      select nivel,count(*) as usuarios_Nivel  from tblUsuarios group by nivel;
     +-------+----------------+
     | nivel | usuarios_Nivel |
     +-------+----------------+
     |     2 |              5 |
     |     3 |              6 |
     |     0 |              6 |
     |     1 |              4 |
     +-------+----------------+
     4 rows in set (0,00 sec)
     ```

10. Listar el login de los usuarios con nivel 2

       ```sql
        select usuario,email,nivel from tblUsuarios where nivel=2;
       +---------+---------------------+-------+
       | usuario | email               | nivel |
       +---------+---------------------+-------+
       | BRE2271 | brenda@live.com     |     2 |
       | ROM6520 | roman@gmail.com     |     2 |
       | RIC8283 | ricardo@hotmail.com |     2 |
       | LET4015 | leticia@yahoo.com   |     2 |
       | HUG5441 | hugo@live.com       |     2 |
       +---------+---------------------+-------+
       5 rows in set (0,00 sec)
       
       ```

11. Mostrar el email de los usuarios que usan gmail

        ```sql
         select email from tblUsuarios where email like '%gmail%';
        +---------------------+
        | email               |
        +---------------------+
        | oscar@gmail.com     |
        | francisco@gmail.com |
        | roman@gmail.com     |
        | brenda2@gmail.com   |
        | lucia@gmail.com     |
        +---------------------+
        5 rows in set (0,00 sec)
        
        ```

12. Listar nombre y teléfono de los usuarios con teléfono LG, SAMSUNG o MOTOROLA

      ```sql
      select nombre,telefono from tblUsuarios where marca='LG' or marca='SAMSUNG' or marca='MOTOROLA';
      +---------+--------------+
      | nombre  | telefono     |
      +---------+--------------+
      | BRENDA  | 655-330-5736 |
      | OSCAR   | 655-143-4181 |
      | LUIS    | 655-137-1279 |
      | ROMAN   | 655-330-3263 |
      | BLAS    | 655-330-3871 |
      | JESSICA | 655-143-6861 |
      | RICARDO | 655-145-6049 |
      | BRENDA  | 655-100-1351 |
      | JUAN    | 655-100-6517 |
      | ELPIDIO | 655-145-9938 |
      | HUGO    | 655-137-3935 |
      +---------+--------------+
      11 rows in set (0,00 sec)
      
      ```

------

### Bloque 2

##### Consultas

1. Listar nombre y teléfono de los usuarios con teléfono que no sea de la marca LG o SAMSUNG

     ```sql
     select nombre,telefono,marca from tblUsuarios where marca <> 'LG' and marca <> 'SAMSUNG';
     +-----------+--------------+------------+
     | nombre    | telefono     | marca      |
     +-----------+--------------+------------+
     | JOSE      | 655-143-3922 | NOKIA      |
     | LUIS      | 655-100-8260 | NOKIA      |
     | DANIEL    | 655-145-2586 | SONY       |
     | JAQUELINE | 655-330-5514 | BLACKBERRY |
     | DIANA     | 655-143-3952 | SONY       |
     | RICARDO   | 655-145-6049 | MOTOROLA   |
     | VALENTINA | 655-137-4253 | BLACKBERRY |
     | BRENDA    | 655-100-1351 | MOTOROLA   |
     | LUCIA     | 655-145-4992 | BLACKBERRY |
     | ELPIDIO   | 655-145-9938 | MOTOROLA   |
     | JESSICA   | 655-330-5143 | SONY       |
     | LETICIA   | 655-143-4019 | BLACKBERRY |
     | LUIS      | 655-100-5085 | SONY       |
     | HUGO      | 655-137-3935 | MOTOROLA   |
     +-----------+--------------+------------+
     14 rows in set (0,00 sec)
     
     ```

2. Listar el login y teléfono de los usuarios con compañia telefónica IUSACELL

     ```sql
     select usuario,email,telefono,compañia from tblUsuarios where compañia='IUSACELL';
     +---------+---------------------+--------------+-----------+
     | usuario | email               | telefono     | compañia  |
     +---------+---------------------+--------------+-----------+
     | BRE2271 | brenda@live.com     | 655-330-5736 | IUSACELL  |
     | LUI7072 | luis@hotmail.com    | 655-100-8260 | IUSACELL  |
     | ROM6520 | roman@gmail.com     | 655-330-3263 | IUSACELL  |
     | RIC8283 | ricardo@hotmail.com | 655-145-6049 | IUSACELL  |
     | LUC4982 | lucia@gmail.com     | 655-145-4992 | IUSACELL  |
     | JES9640 | jessica2@live.com   | 655-330-5143 | IUSACELL  |
     +---------+---------------------+--------------+-----------+
     6 rows in set (0,00 sec)
     
     
     ```

3. Listar el login y teléfono de los usuarios con compañia telefónica que no sea TELCEL

     ```sql
     select usuario,email,telefono,compañia from tblUsuarios where compañia='TELCEL';
     +---------+---------------------+--------------+-----------+
     | usuario | email               | telefono     | compañia  |
     +---------+---------------------+--------------+-----------+
     | OSC4677 | oscar@gmail.com     | 655-143-4181 | TELCEL    |
     | LUI6115 | enrique@outlook.com | 655-137-1279 | TELCEL    |
     | JES4752 | jessica@hotmail.com | 655-143-6861 | TELCEL    |
     +---------+---------------------+--------------+-----------+
     3 rows in set (0,00 sec)
     
     
     ```

4. Calcular el saldo promedio de los usuarios que tienen teléfono marca NOKIA

     ```sql
     select avg(saldo) as Promedio_Saldo, marca from tblUsuarios where marca='NOKIA';
     +----------------+-------+
     | Promedio_Saldo | marca |
     +----------------+-------+
     |            100 | NOKIA |
     +----------------+-------+
     1 row in set (0,00 sec)
     
     ```

     

5. Mostrar el email de los usuarios que no usan yahoo

     ```sql
     select email from tblUsuarios where email not like '%yahoo%';
     +-----------------------+
     | email                 |
     +-----------------------+
     | brenda@live.com       |
     | oscar@gmail.com       |
     | francisco@gmail.com   |
     | enrique@outlook.com   |
     | luis@hotmail.com      |
     | daniel@outlook.com    |
     | jaqueline@outlook.com |
     | roman@gmail.com       |
     | blas@hotmail.com      |
     | jessica@hotmail.com   |
     | diana@live.com        |
     | ricardo@hotmail.com   |
     | valentina@live.com    |
     | brenda2@gmail.com     |
     | lucia@gmail.com       |
     | juan@outlook.com      |
     | elpidio@outlook.com   |
     | jessica2@live.com     |
     | luis2@live.com        |
     | hugo@live.com         |
     +-----------------------+
     20 rows in set (0,00 sec)
     
     ```

6. Listar el login y teléfono de los usuarios con compañia telefónica que no sea TELCEL o IUSACELL

     ```sql
     select usuario,email,telefono from tblUsuarios where compañia not like '%TELCEL%' or 'IUSACELL';
     +---------+-----------------------+--------------+
     | usuario | email                 | telefono     |
     +---------+-----------------------+--------------+
     | BRE2271 | brenda@live.com       | 655-330-5736 |
     | JOS7086 | francisco@gmail.com   | 655-143-3922 |
     | LUI7072 | luis@hotmail.com      | 655-100-8260 |
     | DAN2832 | daniel@outlook.com    | 655-145-2586 |
     | JAQ5351 | jaqueline@outlook.com | 655-330-5514 |
     | ROM6520 | roman@gmail.com       | 655-330-3263 |
     | BLA9739 | blas@hotmail.com      | 655-330-3871 |
     | DIA6570 | diana@live.com        | 655-143-3952 |
     | RIC8283 | ricardo@hotmail.com   | 655-145-6049 |
     | VAL6882 | valentina@live.com    | 655-137-4253 |
     | BRE8106 | brenda2@gmail.com     | 655-100-1351 |
     | LUC4982 | lucia@gmail.com       | 655-145-4992 |
     | JUA2337 | juan@outlook.com      | 655-100-6517 |
     | ELP2984 | elpidio@outlook.com   | 655-145-9938 |
     | JES9640 | jessica2@live.com     | 655-330-5143 |
     | LET4015 | leticia@yahoo.com     | 655-143-4019 |
     | LUI1076 | luis2@live.com        | 655-100-5085 |
     | HUG5441 | hugo@live.com         | 655-137-3935 |
     +---------+-----------------------+--------------+
     18 rows in set, 1 warning (0,00 sec)
     
     
     ```

7. Listar el login y teléfono de los usuarios con compañia telefónica UNEFON

     ```sql
     select usuario,email,telefono from tblUsuarios where compañia='UNEFON';
     +---------+--------------------+--------------+
     | usuario | email              | telefono     |
     +---------+--------------------+--------------+
     | DAN2832 | daniel@outlook.com | 655-145-2586 |
     | BLA9739 | blas@hotmail.com   | 655-330-3871 |
     | DIA6570 | diana@live.com     | 655-143-3952 |
     | LET4015 | leticia@yahoo.com  | 655-143-4019 |
     | LUI1076 | luis2@live.com     | 655-100-5085 |
     +---------+--------------------+--------------+
     5 rows in set (0,00 sec)
     
     ```

8. Listar las diferentes marcas de celular en orden alfabético descendentemente

     ```sql
     select marca from tblUsuarios ORDER BY marca ASC;
     +------------+
     | marca      |
     +------------+
     | BLACKBERRY |
     | BLACKBERRY |
     | BLACKBERRY |
     | BLACKBERRY |
     | LG         |
     | LG         |
     | LG         |
     | MOTOROLA   |
     | MOTOROLA   |
     | MOTOROLA   |
     | MOTOROLA   |
     | NOKIA      |
     | NOKIA      |
     | SAMSUNG    |
     | SAMSUNG    |
     | SAMSUNG    |
     | SAMSUNG    |
     | SONY       |
     | SONY       |
     | SONY       |
     | SONY       |
     +------------+
     21 rows in set (0,00 sec)
     
     ```

9. Listar las diferentes compañias en orden alfabético aleatorio

       ```sql
       select compañia from tblUsuarios ORDER BY RAND();
       +-----------+
       | compañia  |
       +-----------+
       | AXEL      |
       | IUSACELL  |
       | MOVISTAR  |
       | UNEFON    |
       | UNEFON    |
       | MOVISTAR  |
       | IUSACELL  |
       | TELCEL    |
       | TELCEL    |
       | IUSACELL  |
       | IUSACELL  |
       | UNEFON    |
       | AXEL      |
       | NEXTEL    |
       | IUSACELL  |
       | AT&T      |
       | UNEFON    |
       | TELCEL    |
       | UNEFON    |
       | IUSACELL  |
       | AT&T      |
       +-----------+
       21 rows in set (0,00 sec)
       select distinct compañia from tblUsuarios ORDER BY RAND();
       +-----------+
       | compañia  |
       +-----------+
       | TELCEL    |
       | NEXTEL    |
       | UNEFON    |
       | IUSACELL  |
       | MOVISTAR  |
       | AXEL      |
       | AT&T      |
       +-----------+
       7 rows in set (0,00 sec)
       
       select compañia from tblUsuarios GROUP BY compañia ORDER BY RAND();
       +-----------+
       | compañia  |
       +-----------+
       | AXEL      |
       | IUSACELL  |
       | TELCEL    |
       | NEXTEL    |
       | AT&T      |
       | UNEFON    |
       | MOVISTAR  |
       +-----------+
       7 rows in set (0,00 sec)
       
       ```

10. Listar el login de los usuarios con nivel 0 o 2

      ```sql
      select usuario,email,nivel from tblUsuarios where nivel=0 or nivel=2;
      +---------+-----------------------+-------+
      | usuario | email                 | nivel |
      +---------+-----------------------+-------+
      | BRE2271 | brenda@live.com       |     2 |
      | LUI6115 | enrique@outlook.com   |     0 |
      | DAN2832 | daniel@outlook.com    |     0 |
      | JAQ5351 | jaqueline@outlook.com |     0 |
      | ROM6520 | roman@gmail.com       |     2 |
      | BLA9739 | blas@hotmail.com      |     0 |
      | RIC8283 | ricardo@hotmail.com   |     2 |
      | VAL6882 | valentina@live.com    |     0 |
      | JUA2337 | juan@outlook.com      |     0 |
      | LET4015 | leticia@yahoo.com     |     2 |
      | HUG5441 | hugo@live.com         |     2 |
      +---------+-----------------------+-------+
      11 rows in set (0,00 sec)
      
      ```

11. Calcular el saldo promedio de los usuarios que tienen teléfono marca LG

        ```sql
         select avg(saldo),marca from tblUsuarios where marca='LG';
        +------------+-------+
        | avg(saldo) | marca |
        +------------+-------+
        |         50 | LG    |
        +------------+-------+
        1 row in set (0,00 sec)
        ```

------

### Bloque 3

##### Consultas

1. Listar el login de los usuarios con nivel 1 o 3

     ```sql
     select usuario,email,nivel from tblUsuarios where nivel=1 or nivel=3;
     +---------+---------------------+-------+
     | usuario | email               | nivel |
     +---------+---------------------+-------+
     | OSC4677 | oscar@gmail.com     |     3 |
     | JOS7086 | francisco@gmail.com |     3 |
     | LUI7072 | luis@hotmail.com    |     1 |
     | JES4752 | jessica@hotmail.com |     1 |
     | DIA6570 | diana@live.com      |     1 |
     | BRE8106 | brenda2@gmail.com   |     3 |
     | LUC4982 | lucia@gmail.com     |     3 |
     | ELP2984 | elpidio@outlook.com |     1 |
     | JES9640 | jessica2@live.com   |     3 |
     | LUI1076 | luis2@live.com      |     3 |
     +---------+---------------------+-------+
     10 rows in set (0,00 sec)
     
     
     ```

2. Listar nombre y teléfono de los usuarios con teléfono que no sea de la marca BLACKBERRY

     ```sql
     select nombre,telefono,marca from tblUsuarios where marca not like '%BLACKBERRY%';
     +---------+--------------+----------+
     | nombre  | telefono     | marca    |
     +---------+--------------+----------+
     | BRENDA  | 655-330-5736 | SAMSUNG  |
     | OSCAR   | 655-143-4181 | LG       |
     | JOSE    | 655-143-3922 | NOKIA    |
     | LUIS    | 655-137-1279 | SAMSUNG  |
     | LUIS    | 655-100-8260 | NOKIA    |
     | DANIEL  | 655-145-2586 | SONY     |
     | ROMAN   | 655-330-3263 | LG       |
     | BLAS    | 655-330-3871 | LG       |
     | JESSICA | 655-143-6861 | SAMSUNG  |
     | DIANA   | 655-143-3952 | SONY     |
     | RICARDO | 655-145-6049 | MOTOROLA |
     | BRENDA  | 655-100-1351 | MOTOROLA |
     | JUAN    | 655-100-6517 | SAMSUNG  |
     | ELPIDIO | 655-145-9938 | MOTOROLA |
     | JESSICA | 655-330-5143 | SONY     |
     | LUIS    | 655-100-5085 | SONY     |
     | HUGO    | 655-137-3935 | MOTOROLA |
     +---------+--------------+----------+
     17 rows in set (0,00 sec)
     
     ```

3. Listar el login de los usuarios con nivel 3

     ```sql
     select usuario,email,nivel from tblUsuarios where nivel=3;
     +---------+---------------------+-------+
     | usuario | email               | nivel |
     +---------+---------------------+-------+
     | OSC4677 | oscar@gmail.com     |     3 |
     | JOS7086 | francisco@gmail.com |     3 |
     | BRE8106 | brenda2@gmail.com   |     3 |
     | LUC4982 | lucia@gmail.com     |     3 |
     | JES9640 | jessica2@live.com   |     3 |
     | LUI1076 | luis2@live.com      |     3 |
     +---------+---------------------+-------+
     6 rows in set (0,00 sec)
     
     
     
     ```

4. Listar el login de los usuarios con nivel 0

     ```sql
     select usuario,email,nivel from tblUsuarios where nivel=0;
     +---------+-----------------------+-------+
     | usuario | email                 | nivel |
     +---------+-----------------------+-------+
     | LUI6115 | enrique@outlook.com   |     0 |
     | DAN2832 | daniel@outlook.com    |     0 |
     | JAQ5351 | jaqueline@outlook.com |     0 |
     | BLA9739 | blas@hotmail.com      |     0 |
     | VAL6882 | valentina@live.com    |     0 |
     | JUA2337 | juan@outlook.com      |     0 |
     +---------+-----------------------+-------+
     6 rows in set (0,00 sec)
     
     
     ```

5. Listar el login de los usuarios con nivel 1

     ```sql
     select usuario,email,nivel from tblUsuarios where nivel=1;
     +---------+---------------------+-------+
     | usuario | email               | nivel |
     +---------+---------------------+-------+
     | LUI7072 | luis@hotmail.com    |     1 |
     | JES4752 | jessica@hotmail.com |     1 |
     | DIA6570 | diana@live.com      |     1 |
     | ELP2984 | elpidio@outlook.com |     1 |
     +---------+---------------------+-------+
     4 rows in set (0,00 sec)
     
     ```

6. Contar el número de usuarios por sexo

     ```sql
     select sexo,count(*) as num_Usuarios  from tblUsuarios group by sexo;
     +------+--------------+
     | sexo | num_Usuarios |
     +------+--------------+
     | M    |            9 |
     | H    |           12 |
     +------+--------------+
     2 rows in set (0,00 sec)
     
     ```

7. Listar el login y teléfono de los usuarios con compañia telefónica AT&T

     ```sql
     select usuario,email,telefono,compañia from tblUsuarios where compañia like '%AT&T%';
     +---------+--------------------+--------------+-----------+
     | usuario | email              | telefono     | compañia  |
     +---------+--------------------+--------------+-----------+
     | VAL6882 | valentina@live.com | 655-137-4253 | AT&T      |
     | HUG5441 | hugo@live.com      | 655-137-3935 | AT&T      |
     +---------+--------------------+--------------+-----------+
     2 rows in set (0,00 sec)
     
     ```

8. Listar las diferentes compañias en orden alfabético descendentemente

     ```sql
     select compañia from tblUsuarios order by compañia DESC;
     +-----------+
     | compañia  |
     +-----------+
     | UNEFON    |
     | UNEFON    |
     | UNEFON    |
     | UNEFON    |
     | UNEFON    |
     | TELCEL    |
     | TELCEL    |
     | TELCEL    |
     | NEXTEL    |
     | MOVISTAR  |
     | MOVISTAR  |
     | IUSACELL  |
     | IUSACELL  |
     | IUSACELL  |
     | IUSACELL  |
     | IUSACELL  |
     | IUSACELL  |
     | AXEL      |
     | AXEL      |
     | AT&T      |
     | AT&T      |
     +-----------+
     21 rows in set (0,00 sec)
     
     ```

9. Listar el login de los usuarios inactivos

     ```sql
     select usuario,email,activo from tblUsuarios where activo=0;
     +---------+--------------------+--------+
     | usuario | email              | activo |
     +---------+--------------------+--------+
     | LUI7072 | luis@hotmail.com   |      0 |
     | DIA6570 | diana@live.com     |      0 |
     | VAL6882 | valentina@live.com |      0 |
     | JUA2337 | juan@outlook.com   |      0 |
     +---------+--------------------+--------+
     ```

10. Listar los números de teléfono sin saldo

       ```sql
       select telefono,saldo from tblUsuarios where saldo=0;
       +--------------+-------+
       | telefono     | saldo |
       +--------------+-------+
       | 655-143-4181 |     0 |
       | 655-330-5514 |     0 |
       | 655-145-4992 |     0 |
       | 655-100-6517 |     0 |
       +--------------+-------+
       4 rows in set (0,00 sec)
       ```

11. Calcular el saldo mínimo de los usuarios de sexo “Hombre”

        ```sql
        SELECT sexo,min(saldo) FROM tblUsuarios where sexo='M';
        +------+------------+
        | sexo | min(saldo) |
        +------+------------+
        | M    |          0 |
        +------+------------+
        ```

12. Listar los números de teléfono con saldo mayor a 300

      ```sql
      select telefono,saldo from tblUsuarios where saldo>300;
      +--------------+-------+
      | telefono     | saldo |
      +--------------+-------+
      | 655-143-6861 |   500 |
      | 655-145-9938 |   500 |
      | 655-137-3935 |   500 |
      +--------------+-------+
      ```

------

### Bloque 4

##### Consultas

1. Contar el número de usuarios por marca de teléfono

     ```sql
     select marca,count(*) as num_Usuarios_M_T  from tblUsuarios group by marca;
     +------------+------------------+
     | marca      | num_Usuarios_M_T |
     +------------+------------------+
     | SAMSUNG    |                4 |
     | LG         |                3 |
     | NOKIA      |                2 |
     | SONY       |                4 |
     | BLACKBERRY |                4 |
     | MOTOROLA   |                4 |
     +------------+------------------+
     6 rows in set (0,00 sec)
     
     ```

2. Listar nombre y teléfono de los usuarios con teléfono que no sea de la marca LG

     ```sql
     select nombre,telefono,marca from tblUsuarios where marca not like '%LG%';
     +-----------+--------------+------------+
     | nombre    | telefono     | marca      |
     +-----------+--------------+------------+
     | BRENDA    | 655-330-5736 | SAMSUNG    |
     | JOSE      | 655-143-3922 | NOKIA      |
     | LUIS      | 655-137-1279 | SAMSUNG    |
     | LUIS      | 655-100-8260 | NOKIA      |
     | DANIEL    | 655-145-2586 | SONY       |
     | JAQUELINE | 655-330-5514 | BLACKBERRY |
     | JESSICA   | 655-143-6861 | SAMSUNG    |
     | DIANA     | 655-143-3952 | SONY       |
     | RICARDO   | 655-145-6049 | MOTOROLA   |
     | VALENTINA | 655-137-4253 | BLACKBERRY |
     | BRENDA    | 655-100-1351 | MOTOROLA   |
     | LUCIA     | 655-145-4992 | BLACKBERRY |
     | JUAN      | 655-100-6517 | SAMSUNG    |
     | ELPIDIO   | 655-145-9938 | MOTOROLA   |
     | JESSICA   | 655-330-5143 | SONY       |
     | LETICIA   | 655-143-4019 | BLACKBERRY |
     | LUIS      | 655-100-5085 | SONY       |
     | HUGO      | 655-137-3935 | MOTOROLA   |
     +-----------+--------------+------------+
     
     ```

3. Listar las diferentes compañias en orden alfabético ascendentemente

     ```sql
     select compañia from tblUsuarios ORDER BY compañia ASC;
     +-----------+
     | compañia  |
     +-----------+
     | AT&T      |
     | AT&T      |
     | AXEL      |
     | AXEL      |
     | IUSACELL  |
     | IUSACELL  |
     | IUSACELL  |
     | IUSACELL  |
     | IUSACELL  |
     | IUSACELL  |
     | MOVISTAR  |
     | MOVISTAR  |
     | NEXTEL    |
     | TELCEL    |
     | TELCEL    |
     | TELCEL    |
     | UNEFON    |
     | UNEFON    |
     | UNEFON    |
     | UNEFON    |
     | UNEFON    |
     +-----------+
     21 rows in set (0,00 sec)
     
     ```

4. Calcular la suma de los saldos de los usuarios de la compañia telefónica UNEFON

     ```sql
     select sum(saldo) usuario,compañia from tblUsuarios where compañia='UNEFON';
     +---------+-----------+
     | usuario | compañia  |
     +---------+-----------+
     |     550 | UNEFON    |
     +---------+-----------+
     1 row in set (0,00 sec)
     
     ```

5. Mostrar el email de los usuarios que usan hotmail

     ```sql
     select usuario,email from tblUsuarios where email like '%hotmail%';
     +---------+---------------------+
     | usuario | email               |
     +---------+---------------------+
     | LUI7072 | luis@hotmail.com    |
     | BLA9739 | blas@hotmail.com    |
     | JES4752 | jessica@hotmail.com |
     | RIC8283 | ricardo@hotmail.com |
     +---------+---------------------+
     4 rows in set (0,00 sec)
     
     ```

6. Listar los nombres de los usuarios sin saldo o inactivos

     ```sql
     select nombre from tblUsuarios where saldo=0 or activo=0;
     +-----------+
     | nombre    |
     +-----------+
     | OSCAR     |
     | LUIS      |
     | JAQUELINE |
     | DIANA     |
     | VALENTINA |
     | LUCIA     |
     | JUAN      |
     +-----------+
     7 rows in set (0,00 sec)
     ```

7. Listar el login y teléfono de los usuarios con compañia telefónica IUSACELL o TELCEL

     ```sql
     select usuario,email,compañia from tblUsuarios where compañia='IUSACELL' or compañia='TELCEL';
     +---------+---------------------+-----------+
     | usuario | email               | compañia  |
     +---------+---------------------+-----------+
     | BRE2271 | brenda@live.com     | IUSACELL  |
     | OSC4677 | oscar@gmail.com     | TELCEL    |
     | LUI6115 | enrique@outlook.com | TELCEL    |
     | LUI7072 | luis@hotmail.com    | IUSACELL  |
     | ROM6520 | roman@gmail.com     | IUSACELL  |
     | JES4752 | jessica@hotmail.com | TELCEL    |
     | RIC8283 | ricardo@hotmail.com | IUSACELL  |
     | LUC4982 | lucia@gmail.com     | IUSACELL  |
     | JES9640 | jessica2@live.com   | IUSACELL  |
     +---------+---------------------+-----------+
     9 rows in set (0,00 sec)
     
     ```

8. Listar las diferentes marcas de celular en orden alfabético ascendentemente

     ```sql
     select marca from tblUsuarios ORDER BY marca ASC;
     +------------+
     | marca      |
     +------------+
     | BLACKBERRY |
     | BLACKBERRY |
     | BLACKBERRY |
     | BLACKBERRY |
     | LG         |
     | LG         |
     | LG         |
     | MOTOROLA   |
     | MOTOROLA   |
     | MOTOROLA   |
     | MOTOROLA   |
     | NOKIA      |
     | NOKIA      |
     | SAMSUNG    |
     | SAMSUNG    |
     | SAMSUNG    |
     | SAMSUNG    |
     | SONY       |
     | SONY       |
     | SONY       |
     | SONY       |
     +------------+
     21 rows in set (0,00 sec)
     
     ```

9. Listar las diferentes marcas de celular en orden alfabético aleatorio

     ```sql
     select marca from tblUsuarios order by RAND();
     +------------+
     | marca      |
     +------------+
     | MOTOROLA   |
     | LG         |
     | MOTOROLA   |
     | SAMSUNG    |
     | SAMSUNG    |
     | SONY       |
     | LG         |
     | BLACKBERRY |
     | NOKIA      |
     | NOKIA      |
     | BLACKBERRY |
     | BLACKBERRY |
     | MOTOROLA   |
     | SAMSUNG    |
     | SONY       |
     | LG         |
     | SAMSUNG    |
     | BLACKBERRY |
     | SONY       |
     | SONY       |
     | MOTOROLA   |
     +------------+
     21 rows in set (0,00 sec)
     
     ```

10. Listar el login y teléfono de los usuarios con compañia telefónica IUSACELL o UNEFON

       ```sql
       select usuario,email,compañia from tblUsuarios where compañia='IUSACELL' or compañia='UNEFON';
       +---------+---------------------+-----------+
       | usuario | email               | compañia  |
       +---------+---------------------+-----------+
       | BRE2271 | brenda@live.com     | IUSACELL  |
       | LUI7072 | luis@hotmail.com    | IUSACELL  |
       | DAN2832 | daniel@outlook.com  | UNEFON    |
       | ROM6520 | roman@gmail.com     | IUSACELL  |
       | BLA9739 | blas@hotmail.com    | UNEFON    |
       | DIA6570 | diana@live.com      | UNEFON    |
       | RIC8283 | ricardo@hotmail.com | IUSACELL  |
       | LUC4982 | lucia@gmail.com     | IUSACELL  |
       | JES9640 | jessica2@live.com   | IUSACELL  |
       | LET4015 | leticia@yahoo.com   | UNEFON    |
       | LUI1076 | luis2@live.com      | UNEFON    |
       +---------+---------------------+-----------+
       11 rows in set (0,00 sec)
       
       ```

11. Listar nombre y teléfono de los usuarios con teléfono que no sea de la marca MOTOROLA o NOKIA

        ```sql
        select nombre,telefono,marca from tblUsuarios where marca<>'MOTOROLA' and marca<>'NOKIA';
        +-----------+--------------+------------+
        | nombre    | telefono     | marca      |
        +-----------+--------------+------------+
        | BRENDA    | 655-330-5736 | SAMSUNG    |
        | OSCAR     | 655-143-4181 | LG         |
        | LUIS      | 655-137-1279 | SAMSUNG    |
        | DANIEL    | 655-145-2586 | SONY       |
        | JAQUELINE | 655-330-5514 | BLACKBERRY |
        | ROMAN     | 655-330-3263 | LG         |
        | BLAS      | 655-330-3871 | LG         |
        | JESSICA   | 655-143-6861 | SAMSUNG    |
        | DIANA     | 655-143-3952 | SONY       |
        | VALENTINA | 655-137-4253 | BLACKBERRY |
        | LUCIA     | 655-145-4992 | BLACKBERRY |
        | JUAN      | 655-100-6517 | SAMSUNG    |
        | JESSICA   | 655-330-5143 | SONY       |
        | LETICIA   | 655-143-4019 | BLACKBERRY |
        | LUIS      | 655-100-5085 | SONY       |
        +-----------+--------------+------------+
        15 rows in set (0,00 sec)
        
        ```

12. Calcular la suma de los saldos de los usuarios de la compañia telefónica TELCEL

      ```sql
      select sum(saldo) usuario,compañia from tblUsuarios where compañia='TELCEL';
      +---------+-----------+
      | usuario | compañia  |
      +---------+-----------+
      |     550 | TELCEL    |
      +---------+-----------+
      1 row in set (0,01 sec)
      
      ```
