# Datos ficticios para pruebas — INT-01

Estos perfiles son datos sintéticos para usar en pruebas. Todos los correos usan el dominio reservado `ejemplo.com`. No se incluyen contraseñas ni datos personales reales.

| ID de prueba | Perfil o rol | Correo ficticio | Estado inicial | Uso |
|---|---|---|---|---|
| empresa-01 | Empresa | test-empresa@ejemplo.com | Habilitada | Probar funciones de una empresa publicante |
| particular-01 | Particular | test-particular@ejemplo.com | Habilitada | Probar funciones de un particular publicante |
| talento-activo-01 | Talento IT | test-talento-activo@ejemplo.com | Habilitado y activo | Probar el acceso normal de un talento |
| talento-pendiente-01 | Talento IT | test-talento-pendiente@ejemplo.com | Sin habilitar | Probar el acceso antes de la habilitación |
| talento-baja-01 | Talento IT | test-talento-baja@ejemplo.com | Dado de baja lógicamente | Probar el comportamiento de una cuenta dada de baja |
| moderador-01 | Moderador | test-moderador@ejemplo.com | Habilitado | Probar moderación; no gestiona usuarios ni configuración |
| admin-nivel-1-01 | Administrador nivel 1 | test-admin-nivel-1@ejemplo.com | Habilitado | Probar permisos de administración de nivel 1 |
| admin-nivel-2-01 | Administrador nivel 2 | test-admin-nivel-2@ejemplo.com | Habilitado | Probar permisos limitados al grupo |

## Notas

- Estos perfiles no representan personas reales.
- No guardar contraseñas, tokens ni claves en este documento.
- La baja del talento de prueba es lógica: no implica borrar sus datos.
- El moderador tiene alcance global únicamente para moderar.
