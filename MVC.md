
## Modelo Vista Controlador

El Modelo Vista Controlador (MVC) es un estilo de arquitectura de software que separa los datos de una aplicación, la interfaz de usuario, y la lógica de control en tres componentes distintos.

Se trata de un modelo muy maduro y que ha demostrado su validez a lo largo de los años en todo tipo de aplicaciones, y sobre multitud de lenguajes y plataformas de desarrollo.


### Modelo:

Es la capa donde se trabaja con los datos, por tanto contendrá mecanismos para acceder a la información y también para actualizar su estado. Los datos los tendremos habitualmente en una base de datos, por lo que en los modelos tendremos todas las funciones que accederán a las tablas y harán los correspondientes selects, updates, inserts, etc.
## Ejemplo de MVC

Creación del Index donde estará la interfaz:

```bash
  <!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8" />
    <title>Modelo-vista-controlador</title>
</head>
<body>

//Creación de una interfaz sencilla
    <h1>Bienvenido al restaurant Chefcito</h1>
    <section>
        <a href="controlador.php">Solicite nuestro menú</a>
    </section>
</body>
</html>
```

Creación del Controlador por medio de PHP:
```bash
//este será el puente entre la vista y el modelo
 <?php
    require_once('modelo.php');
    $menu = new Platillo();
    $pd = $menu->lista_platillos();
    require_once('vista.php');
?>
```

Creación del archivo modelo en PHP:
```bash
<?php
class Platillo
{
    private $platillo;
    private $dbh;

    public function __construct()
    {
        $this->platillo = array();
        $this->dbh = new PDO(‘mysql:host=localhost;dbname=restaurante’, 'root'», '');
    }

    private function set_names()
    {
        return $this->dbh->query('SET NAMES ‘utf8′');
    }

//recopila toda la información de platillos 
disponibles mediante una consulta a la base de datos.

    public function lista_platillos()
    {
        self::set_names();
        $sql='SELECT nombre, precio from platillos where disponible = 1';
        foreach ($this->dbh->query($sql) as $res)
        {
            $this->platillo[]=$res;
        }
        return $this->platillo;
        $this->dbh=null;
    }
}
?>
```

Creación de la vista:
```bash
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8" />
    <title>Modelo-vista-controlador</title>
</head>
<body>
    <h1>Platillos disponibles</h1>
    <table border="1">
        <tr>
            <td><strong>Nombre platillo</strong></td>
            <td><strong>Precio platillo</strong></td>
        </tr>
        <?php
            for($i=0;$i<count($pd);$i++)
            {
                ?>
                    <tr>
                        <td><?php echo $pd[$i]['nombre']; ?></td>
                        <td><?php echo $pd[$i]['precio']; ?> USD.</td>
                    </tr>
                <?php
            }
        ?>
    </table>
</body>
</html>
```
## Funcionalidades de una aplicación

- Presentar una interfaz fácil e intuitiva para el usuario.
- Seguridad, protección e invulnerabilidad.
- Comunicación (Notificaciones).
- Buena interacción en la aplicación.

## Infraestructura para el almacenamiento y recuperación de datos

Definir una infraestructura para el almacenamiento de datos es escencial debido a la demasiada información que hay, por lo que es necesario que sea gestionada de buena manera. Estos sistemas te permiten realizar:
- Recopilación de datos
- Backup automatizado
- Recuperación de información
- Datos ante desastres