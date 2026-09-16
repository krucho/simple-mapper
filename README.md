# SimpleMapper

Herramienta de mapping 2D autocontenida. Abrí **index.html** con un navegador moderno (Chrome, Edge o Firefox). No necesita servidor, instalación, frameworks, conexión ni dependencias externas.

## Uso

1. Llevá la ventana a la pantalla o proyector de destino y activá pantalla completa con **F**. La tecla **F11** del navegador también sirve.
2. Agregá imágenes con el botón o arrastrando archivos. Las transparencias se conservan. «Probar con ejemplo» agrega un patrón transparente incorporado.
3. En **Transformar**, arrastrá para mover, usá los tiradores para escalar y el punto superior para rotar. Podés editar posición, escala por eje, rotación y opacidad con valores numéricos. La posición corresponde al promedio de las cuatro esquinas. Desmarcá «Mantener relación de aspecto» para escalar cada eje por separado.
4. En **Esquinas**, arrastrá cualquiera de los cuatro puntos para corregir perspectiva con una transformación proyectiva (corner pinning). Elegí una esquina para ajustar sus coordenadas o moverla con el teclado. No se permiten esquinas cruzadas o superficies colapsadas.
5. **G** muestra la grilla de líneas o damero, con separación, color y opacidad ajustables.
6. **H** oculta o muestra todos los controles, incluidos los tiradores y el cursor, sin desplazar las imágenes. **Esc** también recupera los controles. La grilla tiene su propio interruptor y permanece visible hasta apagarla con **G**.
7. **Guardar** descarga un JSON que incluye las imágenes y la calibración. **Abrir proyecto** permite recuperarlo sin depender de los archivos originales.

## Ajuste fino y atajos

| Acción | Atajo |
| --- | --- |
| Arrastre diez veces más lento | Ctrl + arrastrar (⌘ en Mac) |
| Mover imagen o esquina activa 1 px | Flechas |
| Mover 0,1 px | Ctrl/⌘ + flechas |
| Mover 10 px | Shift + flechas |
| Rotar en incrementos de 15° | Shift + arrastrar el punto de rotación |
| Transformar / esquinas | 1 / 2 |
| Recorrer esquinas con el foco en el lienzo | Tab / Shift + Tab |
| Deshacer / rehacer | Ctrl/⌘ + Z / Ctrl/⌘ + Shift + Z |
| Eliminar selección | Supr |
| Guardar proyecto | Ctrl/⌘ + S |
| Cancelar arrastre | Esc |

Los campos numéricos conservan sus atajos habituales mientras se editan. La lista permite seleccionar, ocultar, duplicar, eliminar y ordenar elementos. El elemento superior en la lista se proyecta por encima de los demás. Se guardan hasta 60 pasos de deshacer durante la sesión.

## Coordenadas y alcance

El lienzo ocupa la ventana completa; los paneles flotan sobre él. Las coordenadas son píxeles CSS. Al cambiar la ventana o abrir un proyecto en otra resolución, los vértices se adaptan proporcionalmente en cada eje. Para una calibración precisa, usá siempre la resolución y la pantalla finales. Una relación de aspecto diferente puede modificar la forma proyectada.

Cada imagen se transforma como un plano mediante una homografía CSS `matrix3d`, con transparencia nativa. El fondo de proyección es negro. Es una primera versión orientada a imágenes: no incluye video, edge blending, corrección de lente ni una ventana de salida separada. Los GIF animados se muestran según el soporte del navegador.

Los archivos se procesan localmente. No se envían a ningún servicio. El proyecto se guarda mediante descarga manual; no hay guardado automático. Las imágenes se limitan a 40 MB por archivo y los proyectos a 200 MB y 100 elementos al importar.

## Verificación de desarrollo

`node tests/geometry.cjs` comprueba la sintaxis y 300 transformaciones de perspectiva, conservación de rectas, rotación, escala por eje y validación de archivos de proyecto. Node se usa solo para estas pruebas; no es necesario para utilizar la herramienta.
