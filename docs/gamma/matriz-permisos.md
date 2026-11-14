# Matriz de permisos · v1.0

> Ticket: `GAMMA-M1-002 · LID-05 · Matriz de permisos` · Autor: Sebas · Fecha: 14/11/2026
> Valida: Ivo + Hugo (P2) · Ubicación: `docs/gamma/matriz-permisos.md`
> Se apoya en el contrato del M1 v1.0 (roles y `tiene_rol`). Las reglas de M2 y M3 las implementan alfa y beta; acá queda lo que gamma necesita que se cumpla.

## 1. Cómo se lee

- **Rol** es uno de los 6 del contrato M1. Un usuario **no habilitado** no tiene ningún permiso, salvo ver y editar su propio perfil.
- **Alcance:** *propio* (lo suyo), *grupo* (lo de su grupo), *global* (todo).
- **Regla RLS:** la política de Supabase que lo hace cumplir, en pseudo-SQL. Usa estas funciones auxiliares:

| Función SQL | Devuelve verdadero si… |
|---|---|
| `es_dueno(fila)` | `fila.usuario_id = auth.uid()` |
| `tiene_rol(r)` | el usuario logueado tiene el rol `r`, está habilitado y no está dado de baja |
| `mismo_grupo(fila)` | `fila.grupo_id` = grupo del usuario logueado |
| `no_eliminado(fila)` | `fila.eliminado_en is null` |

- **Por defecto se niega:** toda tabla tiene RLS activado; lo que no figura en la matriz está prohibido.
- **Bajas:** siempre lógicas (`eliminado_en`). Ninguna política permite `DELETE`.

## 2. Matriz

### M1 · Usuarios (tabla `usuarios`, perfil `perfiles`)

| # | Rol | Acción | Alcance | Regla RLS |
|---|---|---|---|---|
| M1-01 | Cualquiera logueado | Ver su propio usuario y perfil completo | propio | `select: es_dueno(fila)` |
| M1-02 | Cualquiera logueado | Editar su propio perfil | propio | `update: es_dueno(fila) and no_eliminado(fila)` |
| M1-03 | Cualquiera, incluso sin sesión | Ver datos **públicos** de un usuario | global | Vista `usuarios_publicos` (solo `id`, `nombre_visible`, `tipo`, `roles`); `select: no_eliminado(fila)` |
| M1-04 | `empresa`, `particular` | Ver campos **visibles para empresas** del perfil de un talento | global | Vista `perfiles_para_empresas`; `select: (tiene_rol('empresa') or tiene_rol('particular')) and no_eliminado(fila)` |
| M1-05 | Cualquiera logueado | Darse de baja | propio | `update(eliminado_en): es_dueno(fila)` |
| M1-06 | `admin_n1` | Ver todos los usuarios y perfiles | global | `select: tiene_rol('admin_n1')` |
| M1-07 | `admin_n1` | Habilitar un talento | global | `update(habilitado): tiene_rol('admin_n1')` |
| M1-08 | `admin_n1` | Asignar o quitar roles (incluido `moderador`) | global | `insert/delete en usuario_roles: tiene_rol('admin_n1')` |
| M1-09 | `admin_n1` | Restablecer la contraseña de un usuario | global | No es RLS: función de servidor con la clave de servicio, que primero verifica `tiene_rol('admin_n1')` |
| M1-10 | `admin_n1` | Dar de baja a cualquier usuario | global | `update(eliminado_en): tiene_rol('admin_n1')` |
| M1-11 | `admin_n2` | Ver los usuarios de su grupo | grupo | `select: tiene_rol('admin_n2') and mismo_grupo(fila)` |
| M1-12 | `admin_n2` | Habilitar talentos de su grupo | grupo | `update(habilitado): tiene_rol('admin_n2') and mismo_grupo(fila)` |

### M2 · Ofertas (tabla `ofertas`, de alfa)

| # | Rol | Acción | Alcance | Regla RLS |
|---|---|---|---|---|
| M2-01 | Cualquiera | Ver ofertas **publicadas** | global | `select: estado = 'publicada' and no_eliminado(fila)` |
| M2-02 | `empresa`, `particular` | Crear, editar, enviar, pausar, cerrar y dar de baja **sus** ofertas | propio | `insert/update: es_dueno(fila) and (tiene_rol('empresa') or tiene_rol('particular'))` |
| M2-03 | `empresa`, `particular` | Ver sus ofertas en cualquier estado | propio | `select: es_dueno(fila)` |
| M2-04 | `moderador` | Ver ofertas *en revisión* | global | `select: estado = 'en_revision' and tiene_rol('moderador')` |
| M2-05 | `admin_n1` | Ver todas; dar de baja y restaurar | global | `select/update(eliminado_en): tiene_rol('admin_n1')` |
| M2-06 | `admin_n2` | Ver las de su grupo | grupo | `select: tiene_rol('admin_n2') and mismo_grupo(fila)` |

### M3 · Búsquedas (tabla `busquedas`, de beta)

| # | Rol | Acción | Alcance | Regla RLS |
|---|---|---|---|---|
| M3-01 | Cualquiera logueado | Ver búsquedas **publicadas** | global | `select: estado = 'publicada' and no_eliminado(fila)` |
| M3-02 | `talento` | Crear, editar, enviar, pausar y dar de baja **sus** búsquedas | propio | `insert/update: es_dueno(fila) and tiene_rol('talento')` |
| M3-03 | `talento` | Ver sus búsquedas en cualquier estado | propio | `select: es_dueno(fila)` |
| M3-04 | `moderador` | Ver búsquedas *en revisión* | global | `select: estado = 'en_revision' and tiene_rol('moderador')` |
| M3-05 | `admin_n1` | Ver todas; dar de baja y restaurar | global | `select/update(eliminado_en): tiene_rol('admin_n1')` |
| M3-06 | `admin_n2` | Ver las de su grupo | grupo | `select: tiene_rol('admin_n2') and mismo_grupo(fila)` |

### M4 · Panel y moderación (tablas `moderaciones`, `reportes`)

| # | Rol | Acción | Alcance | Regla RLS |
|---|---|---|---|---|
| M4-01 | `moderador` | Ver la cola *en revisión* (P42) | global | `select en moderaciones: tiene_rol('moderador')` |
| M4-02 | `moderador` | Aprobar o rechazar con motivo | global | `insert en moderaciones: tiene_rol('moderador') and motivo is not null cuando decision = 'rechazada'` |
| M4-03 | `admin_n1` | Todo lo del moderador, como último recurso | global | Mismas políticas con `or tiene_rol('admin_n1')` |
| M4-04 | `admin_n1` | Ver el panel con métricas de todo (P40) | global | `select en vistas del panel: tiene_rol('admin_n1')` |
| M4-05 | `admin_n2` | Ver el panel de su grupo (P40) | grupo | `select en vistas del panel: tiene_rol('admin_n2') and mismo_grupo(fila)` |
| M4-06 | `admin_n2` | **Reportar** una publicación de su grupo | grupo | `insert en reportes: tiene_rol('admin_n2') and mismo_grupo(publicacion)` |
| M4-07 | `admin_n2` | **No** moderar | — | Ninguna política de `moderaciones` incluye `admin_n2` |
| M4-08 | `moderador` | **No** gestionar usuarios ni configuración | — | Ninguna política de M1 incluye `moderador` (salvo M1-01 a M1-05, que son de cualquiera) |
| M4-09 | Sistema (T6) | Pasar una publicación a *publicada* o *en revisión* | global | Función de servidor de DevSecOps con la clave de servicio; no pasa por RLS de usuario |
| M4-10 | Cualquiera | Toda decisión queda en el historial T58 | — | Lo garantiza T58 (DevSecOps); M4 no escribe el historial a mano |

## 3. Supuestos

| # | Supuesto | A confirmar con |
|---|---|---|
| S1 | El "grupo" de `admin_n2` se guarda como `grupo_id` en `usuarios`, y cada oferta y búsqueda hereda el `grupo_id` de su dueño | Hugo |
| S2 | `admin_n2` puede habilitar talentos de su grupo (M1-12) | Hugo |
| S3 | `admin_n2` **no** puede dar de baja usuarios, ni siquiera de su grupo; lo pide al nivel 1 | Hugo |
| S4 | Las búsquedas publicadas solo las ven usuarios logueados; las ofertas publicadas las ve cualquiera | Líderes de alfa y beta |
| S5 | Un usuario puede tener más de un rol (por ejemplo, `talento` y `moderador`) | Hugo |
| S6 | El moderador no modera lo propio: si es dueño de la publicación, no puede decidir sobre ella | Ivo |

## 4. Pendientes

Ninguno sin marcar: los puntos abiertos son los supuestos S1 a S6.

## 5. Cambios

| Versión | Fecha | Cambio |
|---|---|---|
| 1.0 | 14/11/2026 | Matriz inicial de los 4 módulos con sus reglas RLS |
