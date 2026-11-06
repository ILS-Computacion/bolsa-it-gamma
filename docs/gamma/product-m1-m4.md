# Producto · M1 (usuarios) y M4 (panel y moderación) · gamma

> Contexto para agentes de IA (Claude Code, Cursor) y para el equipo. Se lee **antes** de tocar el repo.
> Si algo de acá contradice el contrato o la constitución, manda el otro documento: avisá al líder.
> Versión 0.1 · 06/11/2026 · Ticket: GAMMA-DOC-NNN · LID-03

## 1. Qué es el producto

La **Bolsa de Trabajo IT** conecta **publicantes** (empresas o particulares) que proponen proyectos para resolver con personas + IA, con **talentos IT** (alumnos) que publican en qué quieren trabajar. El sistema **sugiere cruces**; no contrata.

| Módulo | Qué hace | Equipo |
|---|---|---|
| **M1 · Usuarios** | Registro, inicio de sesión, roles, perfil, habilitación y baja | **gamma** |
| M2 · Ofertas | Ofertas de los publicantes | alfa |
| M3 · Búsquedas | Búsquedas de los talentos y cruces | beta |
| **M4 · Panel y moderación** | Panel con métricas, cola de moderación, reportes | **gamma** |

## 2. Qué NO hace gamma

- No implementa ofertas (M2) ni búsquedas o cruces (M3): solo usa sus contratos o los **simulados** (`GAMMA_SIMULADOS`).
- No implementa el moderador automático **T6** ni el historial de cambios **T58**: los construye DevSecOps; M1 y M4 los consumen.
- No implementa el login por su cuenta: lo hace **Supabase Auth**.

## 3. Stack

| Pieza | Uso |
|---|---|
| **Reflex** (Python) | Interfaz y lógica |
| **Supabase** | Base de datos (Postgres con RLS) y **Supabase Auth** |
| **Reflex Cloud** | Ambientes de test y producción |
| pytest + GitHub Actions | Tests y ticket-check en cada PR |

Descartados: Railway, FastAPI, Nextcloud, Paca-AI y autenticación propia.

### ADR 0004 · Autenticación (resumen)

- **Decisión (15/10):** Supabase Auth (opción B).
- **Descartada:** autenticación propia (opción A).
- **Supabase se encarga de:** contraseñas, sesiones y tokens.
- **M1 se encarga de:** roles, perfil, privacidad por campo, habilitación y baja.
- Documento completo: `docs/adr/0004-autenticacion.md` (LID-06).

## 4. Conceptos

| Concepto | Qué es |
|---|---|
| Publicante | Quien publica ofertas: una **Empresa** o un **Particular**. |
| Talento IT | Alumno con perfil técnico; publica búsquedas y recibe cruces. |
| Usuario | Cuenta en el sistema; tiene uno o más **roles**. |
| Habilitación | El talento se registra **sin habilitar**; lo habilita un admin. |
| Baja | Lógica: se marca `eliminado_en`, no se borra. |

### Roles

| Rol | Puede |
|---|---|
| `talento` | Su perfil y sus búsquedas |
| `empresa` / `particular` | Sus ofertas |
| `moderador` | Solo moderar, con alcance global |
| `admin_n1` | Todo; modera como último recurso |
| `admin_n2` | Lo de su grupo; **reporta, no modera** |

El detalle por acción está en la matriz de permisos (LID-05).

### Moderación

```
borrador → enviada → publicada
                   ↘ en revisión → publicada
                                 ↘ rechazada (con motivo)
```

- T6 decide automáticamente si pasa directo o va a *en revisión*.
- El M4 atiende la cola *en revisión* (P42) y muestra el panel (P40).
- Cada cambio queda en el historial T58.

## 5. Reglas del dominio

| ID | Regla |
|---|---|
| D-01 | Una oferta requiere al menos un perfil humano. |
| D-02 | Presupuesto mayor que cero; plazo de al menos 1 día. |
| D-03 | Solo el publicante dueño edita, pausa, cierra o da de baja su oferta. |
| D-04 | Una oferta publicada no se modifica directo: se prepara un borrador y se confirma. |
| D-05 | Un perfil requerido nunca pide edad, género, origen ni domicilio. |
| D-06 | Solo el talento dueño edita, pausa o da de baja su búsqueda. |
| D-07 | Un cruce solo se sugiere entre oferta publicada y búsqueda publicada. |
| D-08 | El cruce no usa edad, género, origen ni domicilio. |
| D-09 | Un cruce descartado no se vuelve a sugerir (**provisoria**). |

Fuente: modelo de dominio v0.1 (20/10).

## 6. Datos prohibidos y privacidad

- **Nunca** se pide, guarda ni usa: **edad, género, origen, domicilio**.
- Correo y contraseña **no se exponen** fuera del M1 (`UsuarioPublico` no los tiene).
- El correo se guarda normalizado en minúsculas.
- Perfil con campos **públicos / visibles para empresas / privados**. Currículum opcional. *(Qué campo va en cada nivel: se define en la ficha del perfil.)*
- En pruebas, solo datos ficticios (`test-…@ejemplo.com`). Recuperación de cuenta: la restablece el admin.

## 7. Dónde está cada cosa

| Qué | Dónde |
|---|---|
| Reglas para el agente | `AGENTS.md` |
| Contrato del M1 | `docs/gamma/contratos/` (LID-04) |
| Contrato del M4 | `docs/gamma/contratos/` (LID-13) |
| Fichas | `docs/gamma/fichas/` |
| Constitución del equipo | `docs/gamma/constitucion-gamma.md` |
| Plan | `docs/gamma/plan/` |
