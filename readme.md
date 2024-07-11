# DOCUMENTACION ENDPOINT FORMULARIO DE CONTACTO
Una API  escita en PHP  que permite enviar un correo con el metodo POST y con los campos 'name', 'email' y 'message'. Una vez valida la entrada, envía el correo al webmaster y devuelve respuesta JSON con la repsuesta ya sea fallo o éxito. 

 
## Endpoint URL:
 -  http://localhost/api/v1/endpoint-webservice/

## Método utilizado: 
- POST

## Encabezados del endpoint: 

- Content-Type: application/json
- Access-Control-Allow-Origin: *
- Access-Control-Allow-Methods: POST
- Access-Control-Allow-Headers: Authorization, Content-Type

## Configuración del correo del webmaster:
- correo: andrae.tandemaranjuez@gmail.com

## Obtenemos datos de la soliciutd JSON con las variables: 
- $input
- $name
- $email
- $message

## En caso de exito: 
Se envia el correo con los campos declarados y cogiendo las variables, por ejemplo:
- $subject = "Mensaje de $name";
- $body = "Nombre: $name\nCorreo: $email\n\nMensaje:\n$message";
- $headers = 'From: ' . $webmaster_email . "\r\n" .
    'Reply-To: ' . $email . "\r\n" .
    'X-Mailer: PHP/' . phpversion() . "\r\n" .
    'Return-Path: ' . $webmaster_email;

Sale el mensaje en JSON: 
- 'status' => 'success',
- 'message' => 'Correo enviado correctamente.'

# En caso de error: 
Mediante el codigo 500, sale error con el mensaje: 'message' => 'Error al enviar el correo.'

##
##


# DOCUMENTACION ARCHIVO 'sendmail.http' PRUEBAS DE INTEGRACIÓN DEL ENDPOINT


### PRUEBA CORREO EXITOSO:
POST http://localhost/api/v1/endpoint-webservice/ 
Content-Type: application/json

{
    "name": "Andra EG",
    "email": "andrae.tandemaranjuez@gmail.com",
    "message":"jeliu"
}


### PRUEBA CORREO CON ALGUN DATO FALTANTE:
POST http://localhost/api/v1/endpoint-webservice/ 
Content-Type: application/json

{
    "name": "",
    "email": "andrae.tandemaranjuez@gmail.com",
    "message":"jeliu"
}



###  PRUEBA CORREO EMAIL ERRONEO:

POST http://localhost/api/v1/endpoint-webservice/ 
Content-Type: application/json

{
    "name": "Andra EG",
    "email": "",
    "message":"jeliu"
}





### PRUEBA CORREO CON TODOS LOS DATOS FALTANTES: 

POST http://localhost/api/v1/endpoint-webservice/ 
Content-Type: application/json

{
    "name": "",
    "email": "",
    "message":""
}
