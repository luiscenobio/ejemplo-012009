<?
$datos = parse_url($_ENV["DATABASE_URL"]);
// conectarse
$conn = pg_connect(
  "host=" . $datos["host"] . 
  " port=" . $datos["port"] . 
  " dbname=" . substr($datos["path"], 1) . 
  " user=" . $datos["user"] . 
  " password=" . $datos["pass"]);
// indicar que el resultado es JSON
header("Content-type: application/json; charset=utf-8");
// permitir acceso de otros lugares fuera del servidor
header('Access-Control-Allow-Origin: *');
// imprimir si la conexion funciono o no
$exito = !($conn === FALSE);
echo json_encode($exito);
