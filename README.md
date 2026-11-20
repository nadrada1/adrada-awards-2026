# ADRADA AWARDS 2026 — V10.4

**Versión: V10.4**  
**Fecha: 21 de noviembre de 2026**

## Cambios de interfaz

1. En la **votación oficial**, los botones **Siguiente** y **Atrás** desplazan la vista al inicio de la pregunta siguiente o anterior, también en móvil.
2. Desde **Revisa tus votos**, pulsar **Editar** abre solo ese premio. Se añade **Guardar cambio y volver al resumen** y **Volver al resumen** para no tener que pasar por todas las preguntas otra vez.
3. Seleccionar un candidato **no desplaza la pantalla**, para evitar saltos molestos.
4. Se retiran de la pantalla pública los textos sobre versión, instrucciones DEMO y la entrada visible a la organización de pruebas. El botón de administración se presenta como **Administración**.
5. Se conservan los códigos DEMO, las fotos, los códigos reales, el almacenamiento de votos y el panel de resultados.

## Instalación

En GitHub, repositorio `nadrada1/adrada-awards-2026`, usar **Add file → Upload files** y subir **`index.html`** y **`README.md`** de esta carpeta a la raíz. Confirmar con **Commit changes**. Comprobar luego desde `https://nadrada1.github.io/adrada-awards-2026/`.

**No hay que ejecutar SQL, cambiar Edge Functions, secretos ni permisos de Supabase.** La función desplegada V10.3 permanece tal cual.

## Pruebas recomendadas

- Entrar con el código oficial previamente creado.
- Elegir candidato y pulsar **Siguiente**: debe empezar arriba la siguiente categoría.
- Llegar a **Revisa tus votos**, tocar **Editar** en una categoría intermedia, cambiarla y pulsar **Guardar cambio y volver al resumen**. Debe regresar directamente al resumen.
- Pulsar **Guardar mis votos oficiales** y verificar que los resultados actualizan el recuento, sin sumar votos duplicados.
- Verificar que la página de inicio ya no muestra instrucciones ni números de versión.
- Opcional: `DEMO01` sigue operativo, pero ya no se anuncia en la pantalla pública.

## Nota

Esta entrega modifica solo el HTML/JavaScript del navegador. No altera votos ya registrados ni la base de datos.
