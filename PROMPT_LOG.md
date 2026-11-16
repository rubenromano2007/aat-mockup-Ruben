# PROMPT LOG — Assignment 2: Primera funcionalidad real end-to-end

VecinoPaso — Función 1: texto libre → aviso listo para publicar
Repo: https://github.com/rubenromano2007/aat-mockup-Ruben
Deploy: https://aat-mockup-ruben.vercel.app/
Commit de la función: 41c448a8511f56a4394a1d3e578851a6f4905e3e ("Add aviso publication with keyword classification (proposal A: simple lists, most matches wins)")

## Paso 1 — Especificación de la función

1. **Qué hace:** El vecino escribe un aviso en texto libre; la app propone la categoría (seguridad, servicios, eventos, compra-venta) contando palabras clave y arma un aviso listo para publicar con los 5 campos del esquema (id, texto, categoría, fecha y hora, resuelto = "no"). El aviso se publica en una lista visible ("Avisos publicados") que persiste en el navegador (localStorage).
2. **Datos que necesita y de dónde vienen:** Solo el texto que escribe el usuario. La clasificación usa listas de palabras clave dentro de la app (sin API externa ni modelo de IA).
3. **Cómo se sabe que funciona (criterio verificable + caso de prueba):** Caso de prueba: entrada "Se fue la luz en la calle Olmos" → la categoría propuesta debe ser "servicios" y el aviso publicado debe mostrar los 5 campos con resuelto "No".

## Paso 2 — Registro de decisiones (aceptar / rechazar / revisar)

- **Decisión 1 (2026-11-16):** Mike propuso tres formas de clasificar por palabras clave: A) listas simples (gana la categoría con más coincidencias), B) orden de prioridad (gana la primera categoría con cualquier coincidencia), C) puntaje ponderado con "no estoy seguro" si hay empate o cero coincidencias. Decidí usar la **A**. Rechacé la B porque el orden decide los empates en vez del texto, y dejé la C de lado porque la A es más simple de explicar y de probar.
- **Decisión 2 (2026-11-16):** Mike agregó un botón "Marcar como resuelto" en cada aviso publicado, que cambia el campo resuelto a "Sí" (y permite reabrirlo). No estaba en la especificación — la especificación solo pedía resuelto = "no" al crear el aviso. Decidí **quedármelo**.
- **Decisión 3 (2026-11-16):** Mike propuso que cuando hay empate entre categorías o el texto no tiene palabras clave, la app muestre "sin clasificar" y pida al vecino elegir la categoría a mano antes de publicar. Decidí **quedármelo**, porque le da al usuario la opción de elegir cuál es el problema.

## Paso 3 — Registro de validación

**Entrada exacta usada:** `Se fue la luz en la calle Olmos`

**Salida real (copiada, no resumida):**

Categoría propuesta: servicios (2 coincidencia(s): luz, calle)

Vista previa mostrada antes de publicar:
Texto: Se fue la luz en la calle Olmos
Categoría: servicios
Fecha y hora: al publicar
Resuelto: No

Aviso publicado:
- Badge: servicios
- Texto: Se fue la luz en la calle Olmos
- ID: AV-JCTBHY · 16/11/26, 1:28 p.m. · Resuelto: No

Después de hacer clic en "Marcar como resuelto":
- Resuelto: Sí (el botón cambió a "Reabrir aviso"; el ID y la fecha/hora no cambiaron)

Después de recargar la página:
- El aviso sigue listado con el mismo contenido (ID: AV-JCTBHY · 16/11/26, 1:28 p.m. · Resuelto: Sí)

**Veredicto:** Accept — Rubén, 2026-11-16. Motivo: acepto porque la prueba dio servicios con las coincidencias luz y calle, y el aviso publicado mostró los cinco campos correctos.

## Uso de IA

- **Herramientas usadas:** Muse (asistente de IA) para escribir el código de la función, y el navegador para probar el despliegue en vivo.
- **Para qué:** Generar el código HTML/CSS/JS de la sección "Publica un aviso" a partir de mi especificación, y verificar la prueba en el sitio en vivo.
- **Qué decidí y verifiqué yo:** Elegí la propuesta A de clasificación entre las tres opciones; revisé la salida real de la prueba en el sitio en vivo antes de dar el veredicto; el veredicto y su motivo son míos.
