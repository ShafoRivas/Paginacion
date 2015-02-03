<?php
//aqui va la conexion y toda la info mas pendejadas//
////////////////////////////////////////////////////

	//$_GET['pageu'] = esta es una varible que viaja por la url(por get) inicialmente no existe, cuando existe lleva la pagina visitada
	//$pageu = es la varible con la que se trabaja todo el paginado es la pagina que se ve
	
	//al entrar al if verifica que no existe y $pageu toma el valor de 1 en el else
    if(isset($_GET['pageu']))
    {
        $pageu = $_GET['pageu']; // en el casa que si existe toma el $pageu toma el valos de $_GET['pageu']
    }else{

        $pageu = 1; 
    }
$maxu = 5; //El numero total de registros  mostrados por pagina. 
//$curu = es el numero inicial de los registros a mostrar inicialmente es 0
$curu = (($pageu * $maxu) - $maxu); 
	$tuconsulta="SELECT * FROM tuculo ORDER BY campo ASC";// la consulta
	$result2=mysql_query($tuconsulta." LIMIT ".$curu.", ".$maxu);// resultado de una pagina tiene los limites inicialmente seria LIMIT 0,5
	$counttotalu = mysql_query($tuconsulta);// esta consulta es para sacar el total de registros si te fijas esta recupera todos los registros sin limites
 
$counttotalu = mysql_num_rows($counttotalu); //contamos el numero de filas $counttotalu = seria el numero total de registros
$total_pagesu = ceil($counttotalu / $maxu);// se divide el numero total de registros entre el maximo de registros por paginas, ejemplo hay unos 50 registros esto seria 50/5 
//$total_pagesu = esta seria el total de paginas resultado de lo explicado en la linea anterior
?>
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<link rel="shortcut icon" href="../ima/ico.png"/>
<title>Sistema</title>
</head>
<body>
<center>
<div id="cont">
	<!--usuarios-->
      <fieldset>
      <legend><span class="style2">ADMINISTRACI&Oacute;N DE USUARIOS </span></legend>
      <table  align="center" width="99%"  bordercolor="#CCCCCC" border="0">
        <tr>
          <td width="269"  align="center" >Nombre</td>
          <td width="183"  align="center">Usuario</td>
          <td width="119" align="center">Contrase&ntilde;a</td>
        </tr>
        <?php      
   
   while($row = mysql_fetch_array($result2)) //mostramos los datos
   {
	   ?>
			<tr>
              <td colspan="6"   align="center"><hr color="#CCCCCC"></td>
            </tr>
        <tr bordercolor="#CCCCCC">
          <td align="center"><?php echo $row["nombre"]// estos son nombre de los campos de la base maje?></td>
          <td align="center"><?php echo $row["correo"]?></td>
          <td align="center"><?php  echo $row["pass"]?></td>
          </tr>
        <?php
   }
  ?>
      </table>
      </fieldset>
<div align="center"><span>
              <?php
			  
			  //este fragmento de codigo es para operar la paginacion//
			  /////////////////////////////////////////////////////////
if($pageu > 1){ //si $pageu es mayor que 1 significa que hay paginas atras entonces hay que poner el link anterior
                $prevu = ($pageu - 1); //$prevu = variable que contiene la pagina de atras
                echo '<a href="?pageu=' . $prevu . '"> <span> &laquo;Anterior </span>  </a>'; // se imprime el link anterior al al darle clic se redirecciona aqui mismo 
				//pero $pageu recibira el numero de la pagina anterior y hara un corte diferente en la consulta
                }
for($i = 1; $i <= $total_pagesu; $i++) 
                {
                    if($pageu == $i) 
                        {
                            echo'<b>' . $i .'</b> '; //da el numero de paginas vista actualmente
                                } else {
                            echo '<a href="?pageu=' . $i . '"><span>' . $i . '</span></a> '; //genera los demas numeros de paginas
                        }
                }
if($pageu < $total_pagesu){ 
                    $nextu = ($pageu + 1); 
                echo '<a href="?pageu=' . $nextu . '"><span>Siguiente &raquo;</span></a>';//crea el link siguiente
                    } 
?>
          </span> </div>
<!--usuarios-->
</div>
</center>
</body>
</html>
