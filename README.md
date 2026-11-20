# ADRADA AWARDS 2026 — V10

**Versión actual: V10**  
**Fecha: 20 de noviembre de 2026**  
**Estado: preparada para instalar y probar; NO se ha desplegado ni probado contra el Supabase real.**

## Novedades de la V10

- Se mantienen todas las funciones V9, fotos en Supabase y modo `DEMO01`–`DEMO18` local, sin mezclar votos.
- Acceso oficial con códigos aleatorios `ADR-XXXXXXXXXXXX`, generados desde Administrador Supabase → Códigos reales; el código se muestra una sola vez y se guarda como hash HMAC, nunca en GitHub.
- Voto oficial en Supabase, modificable hasta el cierre. Una elección por categoría publicada, validada en servidor y guardada en transacción.
- Administrador Supabase → Resultados en directo: votos por candidatura, porcentajes, participación por familiar, apertura/cierre; actualización cada 15 segundos mientras se visualiza.
- El administrador puede publicar los premios inicialmente en borrador desde Resultados en directo.
- El administrador puede copiar o abrir WhatsApp con el código personal. El envío por WhatsApp requiere pulsar y confirmar el envío; la aplicación no envía mensajes automáticamente.

## Instalación: NO subas todavía `index.html` sin completar el servidor

### Paso 1 — SQL en Supabase

Proyecto: `adrada-awards-2026`. En SQL Editor, nueva consulta con nombre **`10 - Votacion segura ADRADA AWARDS`**. Copia y ejecuta `10-SUPABASE-VOTACION.sql`. No borra fotos, candidaturas ni votos.

### Paso 2 — Secreto de la función

En Supabase → Edge Functions → Secrets, crea un secreto **`AWARDS_CODE_SECRET`** con una cadena criptográficamente aleatoria de al menos 32 caracteres. No lo pongas en GitHub, ni en HTML, ni lo envíes por chat. Puedes generar un secreto seguro en tu ordenador mediante Python:

```bash
python -c "import secrets; print(secrets.token_urlsafe(48))"
```

Supabase proporciona automáticamente a Edge Functions `SUPABASE_URL` y `SUPABASE_SERVICE_ROLE_KEY` en proyectos compatibles. Comprueba que están disponibles; no copies el service-role key a GitHub.

### Paso 3 — Edge Function

En Supabase → Edge Functions, crea la función **`adrada-vote`** y copia el contenido de `supabase/functions/adrada-vote/index.ts` en su editor. **Desactiva Verify JWT / Verify JWT with legacy secret** para esta función antes de desplegar: el código valida por sí mismo la sesión del administrador o el token firmado del votante. Es necesario porque los códigos de votantes no son cuentas de Supabase Auth y se usa una clave `sb_publishable_`.

La función tiene CORS limitado al dominio de GitHub Pages de este proyecto, límites de intentos de códigos y tokens firmados de siete días que se invalidan al regenerar el código. No modifiques el nombre `adrada-vote`.

### Paso 4 — GitHub

En el repositorio `nadrada1/adrada-awards-2026`, usa **Add file → Upload files** para subir **`index.html` y `README.md`** (de esta carpeta) a la raíz. No subas el ZIP ni `build.py` ni ningún secreto.

### Paso 5 — Pruebas, SIN enviar aún códigos a toda la familia

1. Comprueba `DEMO01` y que las fotografías siguen apareciendo.
2. En Administrador Supabase comprueba las pestañas **Códigos reales** y **Resultados en directo**. Si la función no está desplegada, mostrarán un error; esto es esperado hasta terminar pasos 1–3.
3. En Resultados, comprueba los premios: la carga inicial dejó las 10 categorías en estado `draft`. Pulsa **Publicar los 10 premios** solo cuando estén revisados.
4. En Códigos reales, genera **un solo código de prueba** para Nacho A. Cópialo y consérvalo; no es recuperable más tarde. La regeneración invalida el anterior.
5. En Resultados, pulsa **Abrir votación**. Vota con ese código, revisa los 10 premios y guarda. Comprueba en el administrador que aparecen 10 votos, 1 participante completo y los recuentos correspondientes.
6. Vuelve a entrar con el mismo código y cambia un voto. Comprueba que el total sigue siendo 10 y cambia la clasificación correspondiente.
7. Pulsa **Cerrar votación** y verifica que el usuario no puede guardar nuevos votos. Puedes reabrirla para continuar las pruebas.
8. Una vez probado, decide si mantener o borrar los votos oficiales de prueba antes de distribuir códigos. **Esta V10 no incluye botón para borrar votos reales**, precisamente para evitar borrados accidentales.

## Notas y limitaciones

- Los resultados oficiales solo se sirven a un administrador autenticado; los votantes no reciben los resultados.
- Los códigos oficiales se muestran solo una vez; para recuperar acceso se regenera un código nuevo.
- Los datos DEMO siguen guardándose únicamente en el navegador, nunca en Supabase.
- Las fotos están en un bucket público; cualquiera con la URL de una foto puede verla.
- Las 10 categorías se publican en bloque desde el panel. Editar candidaturas después de iniciar las votaciones puede alterar el significado de resultados; revisa los premios antes de abrir.
- La V10 no incluye gestión avanzada de candidaturas ni exportación de votos oficiales. No se ha probado la ejecución real de la Edge Function ni la instalación en la cuenta del usuario: se debe validar con la secuencia anterior.
