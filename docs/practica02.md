# PRÁCTICA DE POST: FORMULARIO DE CLIENTE

## Fichero ut02-p02-a: Parte Cliente

```html
<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>Cliente</title>
</head>
<body>
    <h1>Formulario de Cliente</h1>

    <form name="myform" action="ut02_p02.php" method="post">
        <label for="sueldo">Sueldo:</label>
        <input type="number" id="sueldo" name="sueldo" required><br><br>
        <label for="email">Puesto:</label>
        <select id="puesto" name="puesto" required>
            <option value="Base">Base</option>
            <option value="Directivo">Directivo</option>
            <option value="Alto cargo">Alto_cargo</option>
        </select><br><br>
        <input type="submit" value="Enviar">

    </form>
</body>
</html>
```

Como vemos, para este fichero he creado un formulario que nos permita recolectar la información sobre el cliente. Los datos que vamos a utilizar son: __"Sueldo"__ y __"Puesto"__. Para el campo de __Sueldo__ , más adelante se pondrá una condición para que sea más de 1000 y para el __Puesto__, tendremos 3 opciones para elegir y realizar unos calculos, para poder calcular su precio final con un complemento según el puesto. Todo esto, se enviará al servidor mediante el atributo del "form" y el método que utilicemos: __action="ut02_p02.php" method="post"__

## Fichero ut02_p02: Parte Servidor

```php
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Servidor</title>
</head>

<body>
    <?php
    $sueldo = $_POST['sueldo'];
    $puesto = $_POST['puesto'];
    $complemento = 0 ?? 10;
    $sueldo_final = 0;

    if ($sueldo < 1000) {
        $sueldo = 0;
        echo 'Tu sueldo es menor a 1000. Cálculo no hecho.';
    }

    switch ($puesto) {
        case 'Base':
            $complemento = 10;
            $sueldo_final = ($sueldo * 10) / 100;
            $sueldo_final = $sueldo + $sueldo_final;
            break;
        case 'Directivo':
            $complemento = 15;
            $sueldo_final = ($sueldo * 15) / 100;
            $sueldo_final = $sueldo + $sueldo_final;
            break;
        case 'Alto cargo':
            $complemento = 20;
            $sueldo_final = ($sueldo * 20) / 100;
            $sueldo_final = $sueldo + $sueldo_final;
            break;
    }

    echo "<h1>El sueldo final es: </h1>";
    echo  "<p> El sueldo base es: $sueldo </p>";
    echo "<p> Su complemento es: $complemento </p>";
    echo "<p> El sueldo final es: $sueldo_final </p>";


    ?>
</body>
```

Aquí es donde haremos todo lo necesario para calcular el sueldo final. Para empezar, he declarado 4 variables:

- __Sueldo__: obtendrá el sueldo que el cliente escriba.
- __Puesto__: obtendrá el puesto del cliente.
- __Complemento__: este nos servirá, para aplicar el X% dependiendo del puesto, y si no, le pondremos uno por defecto. 
- __Sueldo final__: nos servirá para almacenar el resultado final del sueldo más el complemento.

Una vez declarado lo necesario, preguntaremos si el sueldo es menor a 1000, en el caso de que lo sea, le daremos el 0 como se valor y un mensaje.

Si es mayor, pasaremos al switch que hay a continuación, que dependiendo que puesto sea el cliente, hará el cálcula para su sueldo final.

- Si es __Base__, su complemento será del 10%. 
- Si es __Directivo__, su complemento será del 15%.
- Si es __Alto cargo__, su complemento será del 20%.

Para cada uno, le haré el cálculo de su precio X el complemento / 100. Y al final, le sumaré el resultado a el sueldo base que tiene. Con ello dándonos el sueldo final.

Por último, hago un resumen del cambio de sueldo.

