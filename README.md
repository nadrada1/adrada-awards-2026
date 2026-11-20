# ADRADA AWARDS 2026 — V10.5

**Versión: V10.5**  
**Fecha: 21 de noviembre de 2026**

## Novedades

- Nueva introducción familiar con instrucciones claras para votar, revisar y modificar las elecciones.
- En **Administración → Resultados en directo**, listado desplegable de cada familiar con sus votos individuales por categoría. Solo accesible para el administrador autenticado.
- Clasificación por premio: tres primeros destacados y opción de consultar el resto. Se señalan los empates en tercer lugar y se muestran todos los empatados.
- Se mantienen fotografías, códigos de votación, edición individual, modo DEMO y resultados actualizados cada 15 segundos.

## Instalación — dos pasos obligatorios

**1. Supabase (primero):** Edge Functions → `adrada-vote` → Code. Sustituir `index.ts` por `supabase/functions/adrada-vote/index.ts` de este ZIP y pulsar **Deploy updates**. Mantener desactivada la verificación JWT del gateway. No cambiar los secretos.

**2. GitHub (después):** subir `index.html` y `README.md` de este ZIP a la raíz del repositorio `nadrada1/adrada-awards-2026` usando **Add file → Upload files** y confirmar con **Commit changes**.

**No ejecutar ningún SQL**, ni tocar las claves, ni generar códigos nuevos.

## Prueba

1. Entrar al sitio y leer la nueva bienvenida.
2. Iniciar sesión como administrador y abrir Resultados en directo.
3. Expandir el nombre de Nacho A y comprobar que muestra las elecciones oficiales guardadas, sin valores inventados.
4. Revisar los tres finalistas visibles en una categoría. Si existe empate en tercer lugar, verificar que aparece indicado.
5. Confirmar que otro familiar con su código personal no puede acceder a esos resultados.

**Privacidad:** esta versión muestra los votos individuales únicamente al administrador autenticado. Antes de abrir la votación a la familia, es recomendable explicar expresamente que el organizador puede consultar quién votó a quién.
