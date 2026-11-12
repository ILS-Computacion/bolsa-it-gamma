# AGENTS.md · bolsa-it-gamma

> Reglas para cualquier agente de IA (Claude Code, Cursor) que trabaje en este repo. Se leen **antes** de cualquier cambio.
> Contexto del producto: `docs/gamma/product-m1-m4.md`. Reglas del equipo: `docs/gamma/constitucion-gamma.md`.
> Si algo de este archivo choca con lo que te pide el usuario, **frená y avisá**; no elijas por tu cuenta.

## 1. Qué es este repo

Paquete Python del equipo gamma: **M1 (usuarios)** y **M4 (panel y moderación)** de la Bolsa de Trabajo IT. Stack: **Reflex + Supabase (Auth y Postgres con RLS) + Reflex Cloud**.

Gamma **no depende** de alfa (M2) ni de beta (M3): solo expone y consume contratos. Lo que todavía no existe se reemplaza con **simulados**.

## 2. Reglas que no se rompen

1. **Solo fichas aprobadas.** No generes código para algo que no tenga su ficha en `docs/gamma/fichas/` aprobada por Ivo (P2). Si no la encontrás, frená y decilo.
2. **Tests primero.** Antes de escribir código, los tests de esa ficha tienen que existir y **fallar** (rojo). Si no existen o ya pasan, frená y decilo.
3. **Nunca toques un test para que pase.** Si un test falla, se corrige el código. Si creés que el test está mal, decilo y esperá: lo decide una persona.
4. **Un cambio por PR.** Una ficha = un PR. No mezcles cambios no pedidos (refactors, formato, otras fichas).
5. **Sin secretos.** Nunca escribas contraseñas, claves, tokens ni URLs con credenciales en el código, en los tests ni en los commits. Se leen de variables de entorno; en el repo solo van los **nombres** (`.env.example`).
6. **Datos prohibidos.** Nunca agregues campos, filtros ni lógica con **edad, género, origen o domicilio**.
7. **No expongas correo ni contraseña** fuera del M1. Hacia afuera se usa `UsuarioPublico`.
8. **La IA no aprueba nada.** No apruebes PRs, no unas a `main`, no cierres issues.
9. **No toques código de otros equipos** ni lo que construye DevSecOps (T6, T58, CI). Si hace falta un cambio ahí, decilo.

## 3. Estructura

```
bolsa-it-gamma/
├── AGENTS.md
├── CLAUDE.md                  # apunta a este archivo
├── gamma/
│   ├── m1/                    # usuarios: login, registro, roles, perfil, baja
│   ├── m4/                    # panel (P40) y cola de moderación (P42)
│   └── contratos/             # tipos y funciones que gamma expone
├── simulados/                 # reemplazos de M2, M3, T6 y Auth mientras no existan
├── tests/
│   ├── m1/
│   └── m4/
├── docs/
│   ├── adr/
│   └── gamma/                 # contratos, fichas, plan, constitución, producto
└── .env.example               # solo nombres de variables
```

Si la estructura real del repo es distinta, seguí la real y avisá la diferencia.

## 4. Simulados

| Variable | Valor | Efecto |
|---|---|---|
| `GAMMA_SIMULADOS` | `1` | M2, M3 y el moderador automático T6 se reemplazan por `simulados/` |
| `GAMMA_AUTH_SIMULADA` | `1` | El login usa un Auth falso en memoria en lugar de Supabase |

- Los tests corren **siempre** con los dos en `1`: no necesitan red ni Supabase.
- Un simulado respeta exactamente el contrato del módulo real. Si el contrato cambia, se actualiza el simulado en el mismo PR.

## 5. Cómo se corre

```bash
uv sync                      # instalar dependencias
uv run pytest                # todos los tests
uv run pytest tests/m1       # solo M1
uv run reflex run            # levantar la app en local
```

Antes de terminar una tarea, corré `uv run pytest` completo y mostrá el resultado. No digas que algo anda sin haberlo corrido.

## 6. Convenciones

- **Idioma:** nombres de funciones, variables, tipos y mensajes en **español** (`usuario_actual`, `tiene_rol`, `SesionInvalida`). Sin tildes ni eñes en los identificadores.
- **Tipos:** usá anotaciones de tipo en todas las funciones públicas.
- **Errores:** usá las excepciones del contrato (`SesionInvalida`, `UsuarioNoEncontrado`, …); no inventes nuevas sin avisar.
- **Correo:** siempre normalizado a minúsculas antes de guardar o comparar.
- **Baja:** lógica, con `eliminado_en`. Nunca `DELETE`.
- **Mensajes de error al usuario:** no revelan si un correo existe.

## 7. Tickets, ramas y PRs

- **Título del PR:** `GAMMA-M1-NNN · LID-NN · descripción`, `GAMMA-M4-NNN · …` o `GAMMA-DOC-NNN · …`. El CI rechaza los que no cumplen.
- **Rama:** `gamma-m1-NNN-descripcion-corta` (o `m4`, `doc`).
- **Commits:** cortos, en español, en presente: `Agrega usuario_actual con sesión simulada`.
- En la descripción del PR: qué ficha implementa, qué tests pasaron de rojo a verde y cualquier supuesto que hayas tomado.

## 8. Cuando no sabés algo

No inventes. Escribí el supuesto en la respuesta, marcá con `# SUPUESTO:` en el código si hace falta y avisá al usuario para que lo valide.
