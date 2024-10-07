# Tarefa: P2. Montando volumes en apache

Este repositorio, creado por **Martín Álvarez Comesaña** mostra como configurar múltiples servidores Apache dentro de contedores Docker utilizando bind mounts para compartir o mesmo directorio `htdocs`. Tamén se mapean diferentes portos para acceder a cada servidor dende o navegador.

## Pasos e comandos realizados:

### 1. Comprobar se a imaxe de `httpd` está dispoñible

Para verificar se xa tes a imaxe de `httpd` (Apache) no teu sistema, executa:

```bash
docker images
```
Se a imaxe non está dispoñible, podes descargala executando:

```bash
docker pull httpd
```

### 2. Crear o contenedor *asir_httpd* e mapeor o porto 80 a 8080

Crea un contedor chamado *asir_httpd*, mapeando o porto 80 do contedor ao porto 8080 da máquina anfitrioa. Usa bind mount para que o directorio htdocs sexa accesible dende o sistema local. Utilizaremos o seguinte comando:

```bash
docker run -d --name asir_httpd -p 8080:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd
```
  **docker run** Executa un novo contedor a partir dunha imaxe de Docker (neste caso, a imaxe é httpd, que é o servidor web Apache).

  **-d:** Executa o contedor en modo "desprendido" (detached mode), o que significa que o contedor corre en segundo plano sen bloquear o terminal.

  **--name asir_httpd:** Asigna o nome asir_httpd ao contedor, facilitando a súa identificación e manipulación no futuro.

  **-p 8080:80:** Mapea o porto 8080 da máquina anfitrioa (o teu ordenador) co porto 80 do contedor. Isto permite acceder ao servidor Apache (que         normalmente serve contido no porto 80) a través do porto 8080 na túa máquina anfitrioa. Así, podes acceder ao servidor desde o teu navegador a través de http://localhost:8080.

  **-v "$PWD"/htdocs:/usr/local/apache2/htdocs/:** Crea un bind mount, que significa que o directorio htdocs do sistema anfitrión (no camiño actual $PWD) está montado dentro do contedor no camiño /usr/local/apache2/htdocs/. Este é o directorio onde Apache serve os ficheiros, polo que o contido do directorio htdocs na túa máquina será accesible como contido do servidor web Apache.

  **httpd:** Especifica a imaxe de Docker que se utilizará para crear o contedor. Neste caso, a imaxe httpd, que é unha implementación do servidor web Apache.

### 3. Crear unha páxina HTML

Crear un fichero index.html dentro del directorio htdocs, en los archivos. En Visual Studio Code o en bash:
```
mkdir htdocs
echo "<h1>Benvido ao servidor Apache</h1>" > htdocs/index.html
```
Unha vez feito, abre o navegador web e accede a http://localhost:8080 para visualizar a páxina.

### 4. Crear os contedores *asir_web1* e *asir_web2*
Agora añadiremos dous contenedores máis, ambos usando o mesmo directorio **htdocs**, pero con portos distintos:

  - asir_web1 no porto 8000:
    ```bash
    docker run -d --name asir_web1 -p 8000:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd
    ```
  - asir_web2 no porto 8090:
    ```
    docker run -d --name asir_web2 -p 8090:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd

- **Verificar no navegador**
  Xa creados os dous contenedores facemos como no paso anterior, comprobar no navegador web os respectivos localhost deberían mostrar a mesma páxina HTML.

## Conclusión

Este proxecto ilustra como utilizar contedores Docker para configurar múltiples servidores Apache compartindo o mesmo contido. Cada servidor está accesible a través de diferentes portos na máquina anfitrioa, permitindo a implementación e o testeo rápido de servidores web.

