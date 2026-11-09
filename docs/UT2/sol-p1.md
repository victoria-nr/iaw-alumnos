# Práctica 1 Solución · Formulario de presupuesto de alojamiento web

A continuación, se muestra una posible solución de la práctica 1 en un solo fichero index.php.

```php
<?php
// Valores iniciales del formulario
$nombre = "";
$correo = "";
$plan = "";
$meses = "";
$backup = false;
$soporte = false;

// Array donde guardaremos los mensajes de error
$errores = [];

// Esta variable nos indica si podemos mostrar el presupuesto
$presupuestoCorrecto = false;

// Una única función propia: devuelve el precio mensual del plan
function obtenerPrecioPlan($plan)
{
    if ($plan == "basico") {
        return 5;
    } elseif ($plan == "profesional") {
        return 9;
    } elseif ($plan == "empresa") {
        return 15;
    }

    return 0;
}

// Solo procesamos datos cuando el formulario se ha enviado por POST
if ($_SERVER["REQUEST_METHOD"] == "POST") {

    // 1. Recoger los datos del formulario
    if (isset($_POST["nombre"])) {
        $nombre = trim($_POST["nombre"]);
    }

    if (isset($_POST["correo"])) {
        $correo = trim($_POST["correo"]);
    }

    if (isset($_POST["plan"])) {
        $plan = $_POST["plan"];
    }

    if (isset($_POST["meses"])) {
        $meses = $_POST["meses"];
    }

    $backup = isset($_POST["backup"]);
    $soporte = isset($_POST["soporte"]);

    // 2. Validar los datos
    if ($nombre == "") {
        $errores[] = "Debes escribir un nombre.";
    }

    if ($correo == "") {
        $errores[] = "Debes escribir un correo electrónico.";
    } elseif (!filter_var($correo, FILTER_VALIDATE_EMAIL)) {
        $errores[] = "El correo electrónico no es válido.";
    }

    if ($plan != "basico" && $plan != "profesional" && $plan != "empresa") {
        $errores[] = "Debes seleccionar un plan válido.";
    }

    if ($meses == "" || filter_var($meses, FILTER_VALIDATE_INT) === false) {
        $errores[] = "Debes indicar un número entero de meses.";
    } elseif ($meses < 1 || $meses > 24) {
        $errores[] = "Los meses deben estar entre 1 y 24.";
    }

    // 3. Si no hay errores, calcular el presupuesto
    if (count($errores) == 0) {
        $precioBase = obtenerPrecioPlan($plan);
        $precioExtras = 0;

        if ($backup) {
            $precioExtras = $precioExtras + 2;
        }

        if ($soporte) {
            $precioExtras = $precioExtras + 3;
        }

        $totalMensual = $precioBase + $precioExtras;
        $totalFinal = $totalMensual * $meses;

        // Texto que mostraremos en el resultado
        if ($plan == "basico") {
            $nombrePlan = "Básico";
        } elseif ($plan == "profesional") {
            $nombrePlan = "Profesional";
        } else {
            $nombrePlan = "Empresa";
        }

        $presupuestoCorrecto = true;
    }
}
?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Presupuesto de alojamiento web</title>
</head>
<body>

    <h1>Presupuesto de alojamiento web</h1>

    <?php if ($presupuestoCorrecto) { ?>

        <h2>Presupuesto calculado</h2>

        <p><strong>Nombre:</strong> <?php echo htmlspecialchars($nombre); ?></p>
        <p><strong>Correo:</strong> <?php echo htmlspecialchars($correo); ?></p>
        <p><strong>Plan:</strong> <?php echo $nombrePlan; ?></p>
        <p><strong>Meses:</strong> <?php echo $meses; ?></p>

        <h3>Extras</h3>

        <?php if (!$backup && !$soporte) { ?>
            <p>No has seleccionado ningún extra.</p>
        <?php } ?>

        <?php if ($backup) { ?>
            <p>Copia de seguridad avanzada: +2 €/mes</p>
        <?php } ?>

        <?php if ($soporte) { ?>
            <p>Soporte prioritario: +3 €/mes</p>
        <?php } ?>

        <h3>Desglose</h3>
        <p>Precio del plan: <?php echo $precioBase; ?> €/mes</p>
        <p>Precio de los extras: <?php echo $precioExtras; ?> €/mes</p>
        <p>Total mensual: <?php echo $totalMensual; ?> €/mes</p>
        <p><strong>Total final: <?php echo $totalFinal; ?> €</strong></p>

        <p><a href="index.php">Calcular otro presupuesto</a></p>

    <?php } else { ?>

        <?php if (count($errores) > 0) { ?>
            <h2>Hay errores en el formulario</h2>
            <ul>
                <?php foreach ($errores as $error) { ?>
                    <li><?php echo $error; ?></li>
                <?php } ?>
            </ul>
        <?php } ?>

        <form action="index.php" method="post">

            <p>
                <label for="nombre">Nombre de contacto:</label><br>
                <input
                    type="text"
                    id="nombre"
                    name="nombre"
                    value="<?php echo htmlspecialchars($nombre); ?>"
                >
            </p>

            <p>
                <label for="correo">Correo electrónico:</label><br>
                <input
                    type="email"
                    id="correo"
                    name="correo"
                    value="<?php echo htmlspecialchars($correo); ?>"
                >
            </p>

            <p>
                <label for="plan">Tipo de plan:</label><br>
                <select id="plan" name="plan">
                    <option value="">-- Selecciona un plan --</option>

                    <option value="basico" <?php if ($plan == "basico") { echo "selected"; } ?>>
                        Básico - 5 €/mes
                    </option>

                    <option value="profesional" <?php if ($plan == "profesional") { echo "selected"; } ?>>
                        Profesional - 9 €/mes
                    </option>

                    <option value="empresa" <?php if ($plan == "empresa") { echo "selected"; } ?>>
                        Empresa - 15 €/mes
                    </option>
                </select>
            </p>

            <p>
                <label for="meses">Meses de contratación:</label><br>
                <input
                    type="number"
                    id="meses"
                    name="meses"
                    min="1"
                    max="24"
                    value="<?php echo htmlspecialchars($meses); ?>"
                >
            </p>

            <p>
                <input type="checkbox" id="backup" name="backup" <?php if ($backup) { echo "checked"; } ?>>
                <label for="backup">Copia de seguridad avanzada (+2 €/mes)</label>
            </p>

            <p>
                <input type="checkbox" id="soporte" name="soporte" <?php if ($soporte) { echo "checked"; } ?>>
                <label for="soporte">Soporte prioritario (+3 €/mes)</label>
            </p>

            <button type="submit">Calcular presupuesto</button>

        </form>

    <?php } ?>

</body>
</html>
```