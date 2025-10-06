# Poryecto de Docker
Un pequeño proyecto en **Docker** que, utilizando **Docker Compose**, levanta dos contenedores.  
Uno contiene una simple aplicación en **Java** que se conecta a una base de datos en **PostgreSQL** con **JPA**,  
y el otro contenedor tiene **Data Miner** expuesto en un puerto público para poder acceder a él desde fuera del contenedor.  

# Como usar:
- 1-Párese en la carpeta2 y ponga "sudo docker build -t jose ."
- 2-Párese en la carpeta1 y haga el "docker compose up" de toda la vida
- 3-Espere, como, un ratito importante. La aplicación en java demora un rato después de que se inicia
el sercivio de Postgresql, la consola se queda congelada como por medio minuto.

### Datos cargados: 
#### Usuarios:  
-	El Listo  
-	Popo  
-	EstoyCansado  

#### Adminer:  
-	Usuario: postgres  
-	Contraseña: 121212  
-	Server: db  
-	Base de datos: espotify21  
