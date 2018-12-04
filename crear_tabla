<?
$datos = parse_url($_ENV["DATABASE_URL"]);
// conectarse
$conexion = pg_connect(
  "host=" . $datos["host"] . 
  " port=" . $datos["port"] . 
  " dbname=" . substr($datos["path"], 1) . 
  " user=" . $datos["user"] . 
  " password=" . $datos["pass"]);
// preparar consultas
pg_prepare($conexion, "sql1", 'DROP TABLE IF EXISTS gente');
pg_prepare($conexion, "sql2", 'CREATE TABLE gente (nombre VARCHAR(30), edad INT)');
pg_prepare($conexion, "sql3", 'INSERT INTO gente (nombre, edad) VALUES ($1, $2)');
pg_prepare($conexion, "sql4", 'SELECT * FROM gente');
// ejecutar consultas
pg_execute($conexion, "sql1", array());
pg_execute($conexion, "sql2", array());
pg_execute($conexion, "sql3", array("Oscar", 28));
pg_execute($conexion, "sql3", array("Carlos", 28));
$resultado = pg_execute($conexion, "sql4", array());
// indicar que el resultado es JSON
header("Content-type: application/json; charset=utf-8");
// permitir acceso de otros lugares fuera del servidor
header('Access-Control-Allow-Origin: *');
// imprimir resultado
$gente = array();
while ($fila = pg_fetch_assoc($resultado)) {
  $fila["edad"] = intval($fila["edad"]);
  array_push($gente, $fila);
}
echo json_encode($gente);
