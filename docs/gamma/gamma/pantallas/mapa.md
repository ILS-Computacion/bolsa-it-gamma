# Mapa de pantallas
| Código | Pantalla | Módulo | Rol que la usa | Caso de uso (Thiago) |
|---|---|---|---|---|
| P00 | Inicio (sin sesión) | M1 | visitante | <ID> |
| P01 | Inicio con sesión | M1 | todos los roles | <ID> |
| P10 | Registrarse | M1 | visitante | <ID> |
| P11 | Iniciar sesión | M1 | visitante | <ID> |
| — | Mi perfil | M1 | talento, empresa, particular | <ID> |
| — | Habilitar cuentas | M1 | admin | <ID> |
| P40 | Panel | M4 | moderador, admin 1, admin 2 | <ID> |
| P42 | Cola de moderación | M4 | moderador | <ID> |
| — | Historial | M4 | moderador, admins | <ID> |
| — | Reportes | M4 | admin 2 | <ID> |

## Recorridos
- Talento / empresa / particular: P00 → P11 → P01 → Mi perfil
- Cuenta nueva: P00 → P10 → aviso "pendiente de habilitación" → (admin habilita) → P11
- Admin: P11 → P01 → Habilitar cuentas / P40
- Moderador: P11 → P01 → P40 → P42 → Historial
- Admin 2: P40 → Reportes
