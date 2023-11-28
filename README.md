# 1.  
Primero debemos crear nuestro docker-compose.yml y configurarlo. Tenemos que añadir un contenedor con nuestro servidor de apache y otro con bind que usaremos como cliente.  

# 2.  
Después tenemos que crear las carpetas para meter nuestros archivos de configuración. Tanto de la configuración de nuestro apache, como la de la configuración del cliente de bind. Recordar que tenemos que mapear ambas carpetas en nuestro docker-compose.yml.   

# 3. 
También tenemos que crear nuestros ficheros de zona y configurarlos.

# 4.  
Una vez hemos tenemos todo configurado, podemos levantar el docker compose para probar si funciona. 

# 5. 
Hacemos un attach shell en nuestro contenedor de bind y probamos: 
apt update  
apt install dnsutils   
dig @10.1.0.2 www.fabulasoscuras.int  
dig @10.1.0.2 www.fabulasoscuras.int   
Comprobamos que recibimos la ip de nuestro contenedor Apache.  

# 6.  
Una vez hemos vemos que nos devuelve la ip correctamente haciendo dig, vamos a proceder a crear dos carpetas con dos archivos index.html en nuestra carpeta mapeada "paginas" anteriormente. Tenemos que modificar el archivo de configuracion de apache para que resuelva la dirección posteriormente usando nuestro dns. Para ello tenemos que agregar las siguientes lineas de código al archivo htttpd.conf: 

< VirtualHost *:100 >  
  DocumentRoot /usr/local/apache2/htdocs/www1  
  ServerName    www.fabulasmaravillosas.int  
</ VirtualHost >  

< VirtualHost *:100 >  
  DocumentRoot /usr/local/apache2/htdocs/www2  
  ServerName    www.fabulasoscuras.int  
</ VirtualHost >  

# 7.  
Una vez configurado vamos a comprobar que funciona. Para ello hacemos un attach shell en nuestro contenedor de bind. Recordar reiniciar el servicio una vez hemos efectuado los cambios.  
Instalamos lynx para comprobar que podemos resolver la dirección mediante nuestro dns. Para ello:  
apt update  
apt install lynx  
lynx www.fabulasoscuras.int  
lynx www.fabulasmaravillosas.int   

Comprobamos que puede resolver. Adjunto las capturas en la carpet imagenes.  










