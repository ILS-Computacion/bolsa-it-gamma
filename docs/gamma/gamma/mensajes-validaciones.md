# Mensajes y validaciones
Reglas: nunca revelar si un correo existe. El límite de ~300 palabras aplica solo a textos libres, no a listas.
## Iniciar sesión (P11)
| Campo | Regla | Mensaje si está mal |
|---|---|---|
| Correo | Tiene que tener @ | Ingresá un correo válido |
| Contraseña | No vacía | Ingresá tu contraseña |
| Ambos | Credenciales incorrectas | Correo o contraseña incorrectos |
| Cuenta | No habilitada | Tu cuenta está pendiente de habilitación |
## Registrarse (P10)
| Campo | Regla | Mensaje si está mal |
|---|---|---|
| Nombre | No vacío | Ingresá tu nombre |
| Correo | Tiene que tener @ | Ingresá un correo válido |
| Contraseña | Mínimo 8 caracteres <confirmar con Supabase> | La contraseña debe tener al menos 8 caracteres |
| Repetir contraseña | Igual a la anterior | Las contraseñas no coinciden |
| Rol | Elegido de la lista | Elegí un rol |
| Descripción | Máx. ~300 palabras (texto libre) | La descripción es demasiado larga |
| Envío OK | (correo nuevo o ya registrado, mismo mensaje) | Revisá tu correo. Tu cuenta está pendiente de habilitación |
## Moderación (P42) y reportes
| Campo | Regla | Mensaje |
|---|---|---|
| Motivo de rechazo | Obligatorio | Escribí el motivo del rechazo |
| Motivo de reporte | Obligatorio | Escribí el motivo del reporte |
| Aviso al autor | Publicación en revisión | Un moderador la va a revisar |
