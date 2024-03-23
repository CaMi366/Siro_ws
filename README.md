# PROYECTO ROS2 HUMBLE

Aquí va que es ros.....
## Preparación espacio de trabajo

### Creación del proyecto ros

1. Creación del workspace 

    ### `mkdir - siro_ws/src`

2. Ingresamos a `siro_ws`

    ### `cd siro_ws`

3. Compilación del proyecto

    ### `colcon build`

    se crearon las carpetas de compilación de este proyecto

    ```
    /build
    /install
    /log

    ```

4. Ingresar al directorio en `src`

    ###`cd src`

5. Creación paquete con ament_cmake `cpp_siro` con C++

    ### `ros2 pkg create --build-type ament_cmake cpp_siro`

    Se crea la carpeta del paquete `cpp_siro` que es la que contiene los archivos de compilación del paquete y archivos de dependencias e información

    ```
    /cpp_siro
    ```

6. Ingresamos a la carpeta del paquete

    ### `cd cpp_siro`

    Aquí encontramos varios documentos y directorios

    ```
    /inclues
    /cpp_siro
    CMakeList.txt
    package.xml
    ```

    En el directorio `include` se guardan archivos necesarios paea la compilación 

    En el directorio `cpp_siro` se guardan los nodos

    El archivo `CMakeList.txt` guarda la configuración del paquete como dependencias , registro de nodos, directorios, versión de c++,...

    El arcgivo package `package.xml` contiene información del paquete como la descrpción, el autor, el contacto, las depensencias y herramientas.

## Creación de nodos 

1. Para crear un nodo nod ubicamos en el directorio `src` del paquete 

    ## `cd siro_ws/src/cpp_siro/src`

2. Creamos un nodo de publicación `siro_node_publicador.cpp` que va a estar publicando en el topico `chatter`

    Escribimos el código del nodo

3. Creamos un nodo de publicación `siro_node_suscriptor.cpp` que va a estar suscrito al topico `chatter`

    Escribimos el código del nodo

4. Configurar el archivo `CMakelist.txt`

    Configurar la versión y el nombre del paquete 
    ```
    cmake_minimum_required(VERSION 3.5)
    project(cpp_siro)

    ```
    Especificar la versión de C++

    ```
    # Default to C++14
    if(NOT CMAKE_CXX_STANDARD)
        set(CMAKE_CXX_STANDARD 14)
    endif()
    ```
    Especificar dependencias del paquete `ament_cmake`,`rclpp` y `std_msgs`

    Creamos los nodos como ejecutables 

    ```
    #Agrega el ejecutable del nodo
    add_executable(siro_node_suscriptor src/siro_node_suscriptor.cpp)
    add_executable(siro_node_publicador src/siro_node_publicador.cpp)
    ```
    Instalar las dependencias de los nodos
    ```
    # Instala el ejecutable
    install(TARGETS
        siro_node_suscriptor
        siro_node_publicador
        DESTINATION lib/${PROJECT_NAME}
        )
    ```

    Creación de un directorio `/launch` para crear lanzaderas y compilación

    ```
    # Instala los scripts y los recursos
    install(DIRECTORY
        launch
        DESTINATION share/${PROJECT_NAME}
    )          

    ament_package()
    ```

5. Compilar el proyecto

Ir a la raíz del proyecto

### `cd siro_ws`

Compilar

### `colcon build`

    ```
    Starting >>> cpp_siro
    Finished <<< cpp_siro [0.26s]                     

    Summary: 1 package finished [0.60s]

    ```

6. Compilar fuentes del proyecto

### `source install/setup.bash`

7. Correr nodo publicador
### `ros2 run cpp_siro siro_node_publicador`

```
[INFO] [1711217747.376664166] [siro_node_publicador]: Publicando: '¡Hola desde siro_node_publicador!'
[INFO] [1711217748.377069188] [siro_node_publicador]: Publicando: '¡Hola desde siro_node_publicador!'
[INFO] [1711217749.376591410] [siro_node_publicador]: Publicando: '¡Hola desde siro_node_publicador!'
[INFO] [1711217750.376572167] [siro_node_publicador]: Publicando: '¡Hola desde siro_node_publicador!'
.
.
.

```

Nodo suscriptor

### `ros2 run cpp_siro siro_node_suscriptor`

```
[INFO] [1711217924.490143182] [siro_node_suscriptor]: Mensaje recibido: '¡Hola desde siro_node_publicador!'
[INFO] [1711217924.827877291] [siro_node_suscriptor]: Esperando mensajes...
[INFO] [1711217925.489910209] [siro_node_suscriptor]: Mensaje recibido: '¡Hola desde siro_node_publicador!'
[INFO] [1711217925.827847970] [siro_node_suscriptor]: Esperando mensajes...
[INFO] [1711217926.490030936] [siro_node_suscriptor]: Mensaje recibido: '¡Hola desde siro_node_publicador!'
[INFO] [1711217926.827891610] [siro_node_suscriptor]: Esperando mensajes...
[INFO] [1711217927.490078601] [siro_node_suscriptor]: Mensaje recibido: '¡Hola desde siro_node_publicador!'
.
.
.
```

# Eso es todo?