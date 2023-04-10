Setup - ejecutar para instalar todas las dependencias del proyecto.
npm install

Compilación - ejecutar para lanzar la app-
npm run serve

- La aplicación está desarrollada en Vue en su versión 2.
- Se utiliza también la librería bootstrap en su versión 5.
- La aplicación es compatible con los navegadores más actuales como Chrome o Firefox.
- La aplicación muestra un listado en modo "grid" del listado procedente de la api.
- En la parte superior hay un combobox para filtrar los productos por categorias (también procedentes de la api)
- No he podido reproducir el máximo de 200 peticiones, por eso ese error como tal no se ha controlado por no
    poder probarlo. No obstante, cuando la API devuelva un error de cualquier tipo, sea el 429 o cualquier otro,
    devolverá un ALERT con el texto: "Error en el servidor. Inténtelo de nuevo más tarde.".
- Hasta que no se haya encontrado respuesta de la api (dos llamadas) mostrará el texto: "Cargando recursos..."
- La aplicación es responsive, adaptando el grid al ancho del terminal (móviles, tablets, etc.).
