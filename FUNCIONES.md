## CONCACT
~~~
SELECT nombre, apellido, CONCAT(nombre, ' ' ,apellido) AS 'Nombre completo' FROM empleados;

CONCAT_WS()
~~~

## REPLACE
~~~
SELECT email, REPLACE(email, 'gmail', 'outlook') AS 'E-mail reemplazado' FROM empleados;
~~~

## SUM 
~~~
SELECT SUM(total) AS 'Total' FROM ventas;
~~~

## MAX/MIN
~~~
SELECT MIN(total) AS 'Venta Minima' FROM ventas;

SELECT MAX(total) AS 'Venta Maxima' FROM ventas;
~~~

## AVG
~~~
SELECT AVG(total) AS 'Venta Promedio' FROM ventas;

~~~

## DATEDIFF podemos obtener la diferencia en días entre dos fechas. Por ejemplo, vamos a obtener los días que pasaron entre la fecha de una venta y el día actual con la función NOW
~~~
SELECT fecha AS 'Fecha venta', DATEDIFF(NOW(), fecha) AS 'Antiguedad en dias' FROM ventas;

~~~ 

## DAY / MONTH / YEAR: Podemos obtener el dia, el mes o el año de una fecha respectivamente. Veamos un ejemplo con el MES.
~~~
SELECT fecha AS 'Fecha venta', MONTH(fecha) AS 'Mes' FROM ventas;

~~~