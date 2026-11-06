# Líder · Sebas · gamma (M1 y M4)

> Leé primero el `gamma-00-MASTER-v1.2.md` (secciones 2 a 5). Las tarjetas con ticket `GAMMA-…` van como issue en `bolsa-it-gamma`; las marcadas `GAMMA-DOC` también son issues (label `tipo:doc`) y sus archivos van en `docs/gamma/`.
> **Tu rol:** convertís la visión en contratos, definís quién puede qué, generás el código con Claude Code a partir de fichas aprobadas y con tests en rojo, y aprobás la intención de cada tarea (P1).

**Hasta la demo del 3/11:** LID-02 → LID-04 → LID-07 → LID-10 (contra la Auth simulada; el 3/11 se conecta a Supabase).

| ID | Tarea | Fase | Ticket | Depende de | Valida | Puerta |
|---|---|---|---|---|---|---|
| LID-01 | Cierre de gobernanza | F0 | GAMMA-DOC | — | Hugo | — |
| LID-02 | Carga del tablero y documentos en el repo | F0 | GAMMA-DOC | INT-03 | Ivo | — |
| LID-03 | Contexto para agentes | F0 | GAMMA-DOC | — | Ivo | — |
| LID-04 | Contrato del M1 v1.0 | F1 | GAMMA-M1-001 | LID-03 | Thiago → revisor de alfa | P4 |
| LID-05 | Matriz de permisos | F1 | GAMMA-M1-002 | LID-04 | Ivo + Hugo | P2 |
| LID-06 | ADR 0004 (Supabase Auth) | F1 | GAMMA-M1-003 | — | Hugo | — |
| LID-07 | Ficha ALG-M1-P1 · Guardar un usuario nuevo | F1 | GAMMA-M1-005 | LID-04 | Ivo → auditora | P2 |
| LID-08 | Lista y reparto de fichas de M1 y M4 | F1 | GAMMA-DOC | LID-04 | Ivo | P1 |
| LID-09 | Revisión de completitud de las fichas | F3 | GAMMA-DOC | ANA-07, ANA-08, ANM-05, ANM-06 | Ivo | P2 |
| LID-10 | Genera el login del PoC | F1 | GAMMA-M1-011 | VA1-05, LID-07, REV-03 | Ivo → revisor de alfa | P4 |
| LID-11 | Entrega y demo del PoC | F1 | GAMMA-DOC | LID-10, INT-11 | Hugo | — |
| LID-12 | Genera el resto del M1 | F2 | GAMMA-M1-018 | REV-06, VA1-07/08/09 | Ivo → revisor de alfa | P4 |
| LID-13 | Contrato del M4 (T61) | F3 | GAMMA-M4-001 | LID-05 | Ivo | P2 |
| LID-14 | Genera el núcleo del M4 (P40 y P42) | F3 | GAMMA-M4-010 | REV-06, VA2-07/08/09/10 | Ivo o quien defina el Consejo → P4 | P4 |
| LID-15 | Correcciones por auditoría (T30) | F3 | GAMMA-M1/M4 según el hallazgo | Informe de la auditora | Auditora | P2 |
| LID-16 | Paquete de despliegue M1 y M4 | F4 | GAMMA-DOC | LID-12, LID-14, LID-15 | DevSecOps | P5 |
| LID-17 | Cierre y ensayo | F4 | GAMMA-DOC | todas | Hugo | — |

---

### LID-01 · Cierre de gobernanza
- **Hace:** cerrar lo pendiente de la constitución del equipo (7 aprobaciones en el PR) y del Consejo (9 integrantes, mayoría 5 de 9). Llevar la constitución a la validación de Hugo.
- **Listo cuando:** el PR tiene las 7 aprobaciones, el Consejo votó y la v1.0 está publicada. Si ya pasó, se marca *Hecho* con el enlace.
- **Valida:** Hugo.

### LID-02 · Carga del tablero y documentos en el repo
- **Depende:** INT-03 (repos clonados).
- **Hace:** subir el MASTER v1.2 y los 7 archivos a `docs/gamma/plan/`. Junto con Nico, cargar **todas** las tarjetas como issues del Project: las que implementan con `GAMMA-M1/M4-NNN` y las de documentación con `GAMMA-DOC-NNN` y label `tipo:doc`. Revisar con cada uno qué quedó hecho del kit 20 al 26/10.
- **Listo cuando:** cada tarjeta tiene responsable, validador distinto y columna inicial; lo hecho del kit está marcado con evidencia.
- **Valida:** Ivo.

### LID-03 · Contexto para agentes
- **Hace:** `docs/gamma/product-m1-m4.md` y `AGENTS.md` en `bolsa-it-gamma`. Incluyen: stack (Reflex, Supabase, Reflex Cloud), ADR 0004, conceptos del modelo de dominio (Publicante, Empresa, Particular, TalentoIT), reglas D-01 a D-09, datos prohibidos (edad, género, origen, domicilio), PRD-01 a PRD-03, PRD-14, NF8 y NF9. Reglas para el agente: solo fichas aprobadas, tests primero, un cambio por PR, sin secretos.
- **Listo cuando:** los archivos están en el repo y no contradicen la constitución.
- **Valida:** Ivo.

### LID-04 · Contrato del M1 v1.0 (B12)
- **Ticket:** GAMMA-M1-001 · **Depende:** LID-03 y el modelo de dominio v0.1.
- **Hace:** completar el contrato del kit. Las funciones que el PoC necesita van primero:
  - **F1** `usuario_actual(sesion_id) -> UsuarioPublico`
  - **F2** `tiene_rol(usuario, rol) -> bool`
  - **F3** `obtener_usuario_publico(usuario_id)`
  - **F4** `dar_de_baja_usuario(...)`, versión menor.

  Define los tipos `UsuarioPublico` y `Rol` (talento, empresa, particular, moderador, admin_n1, admin_n2), los errores (`SesionInvalida`, `UsuarioNoEncontrado`, rol inexistente), los datos que no expone (correo, contraseña) y la sección 5 con la tabla de casos de cada función. Decidir las preguntas abiertas (MASTER §11.3) y escribirlas en la sección 9.
- **Listo cuando:** el contrato tiene la tabla de casos de cada función; Thiago lo validó como control interno; tiene los comentarios de DevSecOps [Seguridad] y de la auditora [Privacidad] y [Sesgo] resueltos; y está aprobado por el revisor de alfa (C6). Si las funciones del PoC ya estaban publicadas el 23/10, solo falta cerrar la aprobación.
- **Valida:** Thiago (interno) → revisor de alfa (P4).

### LID-05 · Matriz de permisos
- **Ticket:** GAMMA-M1-002 · **Depende:** LID-04.
- **Hace:** tabla rol × acción × módulo, con la regla de base de datos (RLS) que hace cumplir cada fila:
  - Nivel 1: todo, y modera como último recurso.
  - Nivel 2: lo de su grupo y la publicación de lo que hace el grupo. **Reporta** pero no modera.
  - **Moderador:** una sola fila, alcance global, una sola acción: moderar.
  - Empresa y particular: sus ofertas.
  - Talento: su perfil y sus búsquedas.
- **Listo cuando:** cada fila tiene su regla de datos y no quedan pendientes sin marcar.
- **Valida:** Ivo + Hugo.

### LID-06 · ADR 0004
- **Ticket:** GAMMA-M1-003.
- **Hace:** `docs/adr/0004-autenticacion.md`: contexto, decisión (Supabase Auth, 15/10), alternativa descartada (autenticación propia) y consecuencias (qué delega el M1 a Supabase y qué sigue siendo nuestro: roles, perfil, habilitación).
- **Valida:** Hugo.

### LID-07 · Ficha ALG-M1-P1 · Guardar un usuario nuevo (B13)
- **Ticket:** GAMMA-M1-005 · **Depende:** LID-04.
- **Hace:** completar la ficha del kit:
  - La contraseña la maneja Supabase Auth y nunca se guarda tal cual.
  - Correo duplicado: el error no revela que existe.
  - El correo se normaliza a minúsculas.
  - El usuario se crea sin habilitar si es talento (lo habilita el admin).
  - Nada queda a medias.
  - Al menos 5 casos de ejemplo, datos que no usa, eficiencia (índice único sobre el correo) y riesgos para la auditoría.
- **Listo cuando:** Ivo la revisó en el par.
- **Valida:** Ivo → revisor de alfa (C2) → auditora (C3).

### LID-08 · Lista y reparto de fichas de M1 y M4
- **Depende:** LID-04.
- **Hace:** listar todas las fichas de gamma (persistencia, lógica e interfaz) con su autor:
  - **Persistencia:** ALG-M1-P1 (Sebas), P2 (Ivo), P3 actualizar perfil y P4 dar de baja (Thiago).
  - **Lógica:** M1 y M4 para Thiago.
  - **Interfaz:** P10, P11, perfil, P40 y P42 para Vicente.
- **Listo cuando:** cada ficha tiene autor, estado y requisito asociado.
- **Valida:** Ivo.

### LID-09 · Revisión de completitud de las fichas
- **Depende:** las fichas redactadas.
- **Hace:** controlar que cada ficha sea coherente con su contrato y con la matriz de permisos antes de que Ivo la apruebe. No reemplaza a REV-06.
- **Valida:** Ivo.

### LID-10 · Genera el login del PoC
- **Ticket:** GAMMA-M1-011 · **Depende:** VA1-05 (tests en rojo), fichas P1 y P2.
- **Hace:** con Claude Code, generar P11 (iniciar sesión), P00 y P01, `usuario_actual` y `tiene_rol` hasta poner los tests en verde. Guardar los prompts en el repo privado.
- **Listo cuando:** los tests de VA1-05 están en verde en el CI, Ivo revisó el PR y el revisor de alfa dio la P4. **Objetivo: lunes 2/11 contra la Auth simulada**; el martes 3/11 se conecta a Supabase real, se corren los tests otra vez y Nico integra para la demo.
- **Valida:** Ivo → revisor de alfa.

### LID-11 · Entrega y demo del PoC
- **Depende:** LID-10, INT-11.
- **Hace:** hoy 29/10, entregar lo que hay (contrato, fichas P1 y P2, casos y tests en rojo, esqueleto) explicando que Supabase llega el 3/11. En la demo del 3/11, mostrar la v0.1.0 con el login en verde dentro del recorrido "una empresa publica una oferta y un talento la encuentra", sumando lo ampliado (registro, perfil, recuperación) solo si tiene tests en verde.
- **Valida:** Hugo.

### LID-12 · Genera el resto del M1
- **Ticket:** GAMMA-M1-018 · **Depende:** fichas aprobadas (REV-06), tests en rojo (VA1-07, 08 y 09).
- **Hace:** registro (P10) con habilitación por admin, perfil con privacidad por campo y currículum opcional, restablecimiento de contraseña por el admin, baja lógica (`eliminado_en`), políticas RLS y `obtener_usuario_publico`. Lotes chicos, un PR por ficha.
- **Valida:** Ivo → revisor de alfa (P4).

### LID-13 · Contrato del M4 (T61)
- **Ticket:** GAMMA-M4-001 · **Depende:** LID-05.
- **Hace:** contrato B12 del M4:
  - Máquina de estados (`enviada → en revisión → publicada / rechazada` con motivo).
  - Consumo del resultado del moderador automático T6.
  - Cola *en revisión* (P42) y panel con métricas (P40).
  - Reportes del nivel 2.
  - Uso de las funciones de baja y restauración que M2 y M3 ofrecen al admin.
  - Historial T58.
- **Listo cuando:** la máquina de estados está dibujada y los permisos salen de LID-05.
- **Valida:** Ivo.

### LID-14 · Genera el núcleo del M4
- **Ticket:** GAMMA-M4-010 · **Depende:** fichas del M4 aprobadas y tests en rojo de Agustín.
- **Hace:** P40 (panel y métricas) y P42 (cola de moderación: aprobar o rechazar con motivo). Cada cambio queda en el historial (T58).
- **Valida:** Ivo, o quien defina el Consejo → P4.

### LID-15 · Correcciones por auditoría (T30)
- **Hace:** una tarjeta por hallazgo; se corrige la ficha y el código y los tests vuelven a verde. Los críticos se cierran antes del despliegue.
- **Valida:** auditora.

### LID-16 · Paquete de despliegue M1 y M4
- **Hace:** junto con Nico, dejar el checklist listo: variables (solo nombres), migraciones y arranque desde cero.
- **Valida:** DevSecOps (P5).

### LID-17 · Cierre y ensayo
- **Hace:** tablero sin tarjetas abiertas sin justificar, documentación reunida con Vicente y ensayo de la presentación del 27/11.
- **Valida:** Hugo.
