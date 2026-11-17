# Contrato del M1 · Usuarios · v1.0

> Ticket: `GAMMA-M1-001 · LID-04 · Contrato del M1 v1.0` · Autor: Sebas · Fecha: 06/11/2026
> Valida: Thiago (control interno) → revisor de alfa (P4). Comentan: DevSecOps [Seguridad], auditora [Privacidad] y [Sesgo].
> Ubicación: `docs/gamma/contratos/contrato-m1.md`

## 1. Propósito

Define **qué ofrece el M1 al resto del sistema** (M2, M3, M4 y la interfaz), sin decir cómo está hecho por dentro. Ningún otro módulo lee la tabla de usuarios ni Supabase Auth directamente: **todo pasa por estas funciones**.

## 2. Alcance

| Incluye | No incluye |
|---|---|
| Saber quién está logueado (F1) | El login en sí: lo hace Supabase Auth |
| Saber si un usuario tiene un rol (F2) | Qué puede hacer cada rol en cada módulo: matriz de permisos (LID-05) |
| Datos públicos de un usuario (F3) | Registro, perfil y habilitación: fichas propias del M1 |
| Baja lógica de una cuenta (F4) | Qué pasa con ofertas y búsquedas de quien se da de baja: lo decide cada módulo |

**Versiones:** F1, F2 y F3 entran en **v1.0** (las necesita el PoC). F4 entra en **v1.1** (cambio menor: agrega, no rompe).

## 3. Tipos

### `Rol`

Enumeración. Valores exactos:

| Valor | Quién |
|---|---|
| `talento` | Alumno con perfil IT |
| `empresa` | Publicante empresa |
| `particular` | Publicante particular |
| `moderador` | Modera, con alcance global; nada más |
| `admin_n1` | Docente: todo |
| `admin_n2` | Líder de grupo: lo de su grupo; reporta, no modera |

### `TipoCuenta`

Enumeración: `talento`, `empresa`, `particular`. Es **qué es** la cuenta; no da permisos. Los permisos salen solo de los roles (ver decisión 9.2).

### `UsuarioPublico`

Inmutable. Es lo único que el M1 entrega hacia afuera.

| Campo | Tipo | Nota |
|---|---|---|
| `id` | `str` (UUID) | El mismo id de Supabase Auth |
| `nombre_visible` | `str` | Nombre que se muestra en el sistema |
| `tipo` | `TipoCuenta` | |
| `roles` | `frozenset[Rol]` | Al menos uno |
| `habilitado` | `bool` | Un talento recién registrado viene en `False` hasta que lo habilita un admin |

**No tiene** correo, contraseña, token ni ningún dato del perfil marcado como privado o visible para empresas (ver §7).

## 4. Funciones

### F1 · `usuario_actual(sesion_id: str) -> UsuarioPublico`

Devuelve el usuario dueño de la sesión.
- `sesion_id` es el token de acceso de Supabase Auth (decisión 9.1).
- Lanza `SesionInvalida` si la sesión no sirve, por cualquier motivo.
- Un usuario **no habilitado** sí se devuelve, con `habilitado = False`: la interfaz decide qué mostrarle.

### F2 · `tiene_rol(usuario: UsuarioPublico, rol: Rol | str) -> bool`

Dice si el usuario tiene ese rol.
- Acepta el rol como `Rol` o como texto exacto (`"moderador"`).
- Lanza `RolInexistente` si el texto no es uno de los 6 roles.
- Un usuario **no habilitado** da `False` para cualquier rol.
- **No hay herencia:** `admin_n1` no tiene `moderador` salvo que se le haya asignado (decisión 9.3).

### F3 · `obtener_usuario_publico(usuario_id: str) -> UsuarioPublico`

Devuelve los datos públicos de cualquier usuario.
- Lanza `UsuarioNoEncontrado` si no existe, si está dado de baja o si el id no tiene formato válido.
- No exige sesión: solo devuelve datos públicos.

### F4 · `dar_de_baja_usuario(sesion_id: str, usuario_id: str) -> None` · v1.1

Baja lógica: marca `eliminado_en` con la fecha y hora. **Nunca borra.**
- Puede darse de baja a sí mismo cualquier usuario; puede dar de baja a otro solo `admin_n1`. Lo de `admin_n2` sobre su grupo lo define la matriz (LID-05).
- Lanza `SesionInvalida`, `PermisoDenegado` o `UsuarioNoEncontrado`.
- Después de la baja, las sesiones de ese usuario dejan de servir (F1 lanza `SesionInvalida`).

## 5. Casos

Cada fila es al menos un test (VA1).

### F1 · `usuario_actual`

| # | Dado | Cuando | Entonces |
|---|---|---|---|
| F1-01 | Talento habilitado con sesión vigente | `usuario_actual(token)` | Devuelve su `UsuarioPublico` con `roles = {talento}` |
| F1-02 | Talento registrado y **no habilitado** con sesión vigente | `usuario_actual(token)` | Devuelve el usuario con `habilitado = False` |
| F1-03 | Sesión vencida | `usuario_actual(token)` | `SesionInvalida` |
| F1-04 | Token alterado o inventado | `usuario_actual(token)` | `SesionInvalida` |
| F1-05 | Texto vacío o `None` | `usuario_actual("")` | `SesionInvalida` |
| F1-06 | Usuario dado de baja con un token que antes servía | `usuario_actual(token)` | `SesionInvalida` |
| F1-07 | Cualquier caso válido | Se inspecciona el resultado | No contiene correo, contraseña ni token |

### F2 · `tiene_rol`

| # | Dado | Cuando | Entonces |
|---|---|---|---|
| F2-01 | Empresa habilitada | `tiene_rol(u, Rol.empresa)` | `True` |
| F2-02 | Empresa habilitada | `tiene_rol(u, Rol.talento)` | `False` |
| F2-03 | Usuario con roles `{talento}` | `tiene_rol(u, "talento")` (texto) | `True` |
| F2-04 | Cualquier usuario | `tiene_rol(u, "superadmin")` | `RolInexistente` |
| F2-05 | `admin_n1` sin `moderador` asignado | `tiene_rol(u, Rol.moderador)` | `False` |
| F2-06 | `admin_n1` con `moderador` asignado | `tiene_rol(u, Rol.moderador)` | `True` |
| F2-07 | `admin_n2` | `tiene_rol(u, Rol.moderador)` | `False` |
| F2-08 | Talento **no habilitado** | `tiene_rol(u, Rol.talento)` | `False` |
| F2-09 | Cualquier usuario | `tiene_rol(u, "Talento")` (mayúscula) | `RolInexistente` (el texto debe ser exacto) |

### F3 · `obtener_usuario_publico`

| # | Dado | Cuando | Entonces |
|---|---|---|---|
| F3-01 | Usuario existente y activo | `obtener_usuario_publico(id)` | Devuelve su `UsuarioPublico` |
| F3-02 | Id que no existe | `obtener_usuario_publico(id)` | `UsuarioNoEncontrado` |
| F3-03 | Usuario dado de baja | `obtener_usuario_publico(id)` | `UsuarioNoEncontrado` |
| F3-04 | Id con formato inválido (`"abc"`) | `obtener_usuario_publico("abc")` | `UsuarioNoEncontrado` |
| F3-05 | Usuario con campos privados en el perfil | Se inspecciona el resultado | No aparece ningún campo privado ni visible solo para empresas |

### F4 · `dar_de_baja_usuario` (v1.1)

| # | Dado | Cuando | Entonces |
|---|---|---|---|
| F4-01 | Talento logueado | Se da de baja a sí mismo | `eliminado_en` queda marcado; el registro sigue existiendo |
| F4-02 | `admin_n1` logueado | Da de baja a otro usuario | `eliminado_en` queda marcado |
| F4-03 | Empresa logueada | Intenta dar de baja a otro usuario | `PermisoDenegado`; nada cambia |
| F4-04 | Usuario ya dado de baja | Se lo intenta dar de baja otra vez | `UsuarioNoEncontrado` |
| F4-05 | Sesión vencida | Cualquier baja | `SesionInvalida`; nada cambia |
| F4-06 | Baja hecha | `usuario_actual` con el token anterior | `SesionInvalida` |
| F4-07 | Baja hecha | `obtener_usuario_publico(id)` | `UsuarioNoEncontrado` |

## 6. Errores

| Error | Cuándo |
|---|---|
| `SesionInvalida` | Sesión vacía, vencida, alterada o de un usuario dado de baja |
| `UsuarioNoEncontrado` | El usuario no existe, está dado de baja o el id es inválido |
| `RolInexistente` | El rol pedido no es uno de los 6 |
| `PermisoDenegado` | Quien pide la acción no tiene permiso para hacerla |

Todos heredan de `ErrorM1`. **Los mensajes no dicen por qué falló la sesión** (vencida, alterada o de una cuenta de baja): solo "sesión inválida".

## 7. Datos que el M1 no expone

- Correo, contraseña, tokens y cualquier dato de Supabase Auth.
- Campos del perfil marcados como **privados** o **visibles para empresas**: esos tendrán su propia función cuando exista la ficha del perfil.
- Nunca existen en el sistema: **edad, género, origen ni domicilio**.

## 8. Simulados

Con `GAMMA_AUTH_SIMULADA=1`, las cuatro funciones trabajan sobre los usuarios ficticios de Nico (correos `test-…@ejemplo.com`) y un token falso por usuario. **Cumplen exactamente estos mismos casos.** Pasar a Supabase real no cambia el contrato.

## 9. Decisiones

| # | Pregunta | Decisión |
|---|---|---|
| 9.1 | ¿`sesion_id` es el token de Supabase? | **Sí**, el token de acceso. Ningún módulo lo interpreta: solo lo pasa a F1. |
| 9.2 | ¿Rol es lo mismo que tipo de cuenta? | **No.** El tipo dice qué es la cuenta; los permisos salen solo de los roles. |
| 9.3 | ¿`admin_n1` pasa cualquier `tiene_rol`? | **No.** No hay herencia: un admin no pasa roles que no tiene asignados. Lo que puede hacer el admin lo dice la matriz (LID-05). |
| 9.4 | ¿El correo con mayúsculas entra? | **Sí**, pero se normaliza a minúsculas antes de guardar o comparar. |
| 9.5 | ¿Un usuario no habilitado tiene sesión? | **Sí:** F1 lo devuelve con `habilitado = False`, pero F2 da `False` para todo. |
| 9.6 | ¿Qué pasa con las ofertas y búsquedas de una cuenta dada de baja? | **Fuera de este contrato:** pregunta abierta del modelo de dominio (C4). El M1 solo marca la baja. |

## 10. Comentarios de revisión

| Quién | Etiqueta | Comentario | Resuelto |
|---|---|---|---|
| DevSecOps | [Seguridad] | | ☐ |
| Auditora | [Privacidad] | | ☐ |
| Auditora | [Sesgo] | | ☐ |
| Thiago | Control interno | | ☐ |
| Revisor de alfa | P4 | | ☐ |

## 11. Cambios

| Versión | Fecha | Cambio |
|---|---|---|
| 1.0 | 06/11/2026 | F1, F2 y F3, tipos, errores, casos y decisiones |
| 1.1 | — | F4 `dar_de_baja_usuario` (prevista) |
