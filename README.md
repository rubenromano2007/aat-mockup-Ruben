# VecinoPaso

VecinoPaso conecta vecinos para reportes urbanos, fondos comunitarios y favores locales.

## Decisiones de diseño vs. sugerencias del IS

### 1. Avisos en localStorage (escalabilidad)

- **Sugerencia del IS:** construir primero la tabla compartida en Supabase para que los avisos se compartan entre usuarios.
- **Mi decisión:** guardar los avisos en localStorage primero y migrar a la tabla compartida después.
- **Razón técnica:** primero hay que comprobar que los flujos (publicar, clasificar, resolver) funcionan; no pagar el costo de complejidad de la base de datos antes de saber que la función sirve.

### 2. Llave publicable + RLS (seguridad)

- **Sugerencia del IS:** esconder el acceso a la base de datos detrás de funciones del servidor.
- **Mi decisión:** llamar directo a Supabase con la llave publicable y proteger los datos con políticas RLS.
- **Razón técnica:** es más simple de depurar y auditar, la llave publicable está diseñada para ser pública, y lo que protege los datos son las políticas RLS, no esconder la llave.
