# MASTER v1.2 · Plan de trabajo de gamma · M1 (usuarios) y M4 (panel y moderación)

> Bolsa de Trabajo IT · 6.º Año Desarrollo de Sistemas 2026
> Versión 1.2 · 29/10/2026 · **Cambios de Hugo del 29/10: Nextcloud descartado y proyecto Supabase de la organización disponible el martes 3/11.** Incorpora además la **Devolución al plan MASTER (v2, 20/10)**, el **Kit de la semana 20 al 26/10** y el **Modelo de dominio v0.1**.
> Plan **no cronometrado**: cuenta cumplir la tarjeta. Las fechas de la sección 2 son las únicas fijas; las de cada fase son **objetivos** de referencia.
> Cada integrante trabaja con su archivo: `gamma-01` a `gamma-07`.

---

## 1. El equipo

| Prefijo | Rol | Integrante | Archivo | Foco |
|---|---|---|---|---|
| `LID-` | Líder | **Sebas** | gamma-01-LIDER.md | Contratos, matriz de permisos, ficha P1, genera el código con Claude Code |
| `REV-` | Revisor | **Ivo** | gamma-02-REVISOR.md | Ficha P2, aprueba fichas y PRs, revisión cruzada del M3 de beta |
| `ANA-` | Analista mayor | **Thiago** | gamma-03-ANALISTA-MAYOR.md | Casos de uso, modelo de datos, fichas de lógica M1 y M4, aceptación |
| `VA1-` | Validador 1 | **Facu** | gamma-04-VALIDADOR-1.md | Tests del M1 escritos antes del código (T31) |
| `VA2-` | Validador 2 | **Agustín** | gamma-05-VALIDADOR-2.md | Tests del M4 (T61), historial (T58) e integración |
| `ANM-` | Analista menor + Documentador | **Vicente** | gamma-06-ANALISTA-MENOR-DOC.md | Pantallas y fichas de interfaz, registro, documentación y memoria |
| `INT-` | Integrador | **Nico** | gamma-07-INTEGRADOR.md | Repos, CI, datos ficticios, integración con alfa y beta, despliegue en test |

**Externos que validan o entregan:** Hugo (docente, admin nivel 1), Auditora algorítmica (Emma), DevSecOps, community manager (catálogo y datos ficticios), revisor de alfa (puerta P4), líderes de alfa y beta.

## 2. Fechas fijas

| Fecha | Hito |
|---|---|
| **Jue 29/10** | **PoC:** como Supabase no existe todavía, gamma entrega contrato M1, fichas P1 y P2, casos y tests del login en rojo, y el esqueleto |
| **Mar 3/11** | **Llega el proyecto Supabase de la organización** y es la demo del PoC: login (P11 + P00, P01) con `usuario_actual` y `tiene_rol` en verde. Hasta ese día se construye contra la **Auth simulada** (INT-00) |
| Jue 5/11 | Fin estimado de la auditoría algorítmica (T23) |
| Jue 12/11 | Referencia del plan para el núcleo del M4. **Gamma diseña antes (T61)** |
| Mar 17/11 | Borrador completo interno de la memoria |
| **Jue 19/11** | **Deadline gamma: M1 y M4 en test y con validación de DevSecOps (P5)** |
| Mar 24/11 | Entrega final: prototipo, documentación (T69) y trazas |
| Vie 27/11 | Presentación y defensa |
| Mar 1/12 | Memoria técnica (T40), 23:59 |

## 3. Decisiones confirmadas por Hugo (ya no son preguntas)

| Tema | Decisión |
|---|---|
| Autenticación | Supabase Auth (ADR 0004, decidida el 15/10) |
| Talentos de la v1.0 | Alumnos de la escuela con perfil IT. Electrónica y artística quedan afuera, pero preparadas (categoría configurable, PRD-NF8) |
| Roles | Talento (alumno), empresa, particular, moderador, admin nivel 1 (docente: todo), admin nivel 2 (líder de grupo: lo de su grupo y la publicación de lo que hace el grupo) |
| **Moderador** | **Rol propio de alcance global que solo modera.** No gestiona usuarios ni configuración. Lo asigna el nivel 1, que también puede moderar como último recurso. El nivel 2 **reporta** lo de su grupo pero **no lo modera** |
| **Moderación** | Nada se publica sin el OK de al menos un moderador (PRD-14). El primero es **automático (T6, lo construye DevSecOps)**. Si encuentra un problema, la publicación queda *en revisión* y la atiende el **M4 (P42)**. El M4 **no hace** la moderación automática: consume su resultado |
| **Estados** | `borrador → enviada → publicada`, o bien `enviada → en revisión → publicada / rechazada` |
| Perfil | Currículum opcional. Cada campo es público, visible para empresas o privado. La empresa no ve lo que no hace falta para trabajar (PRD-02) |
| Datos personales | Si un dato no hace falta para trabajar, no se pide. **Nunca edad, género, origen ni domicilio.** La auditora revisa ANA-03 **antes** de programar el registro |
| Verificación de alumno | Propuesta: el administrador habilita la cuenta (se confirma en la C6) |
| Textos libres | Límite de unas 300 palabras solo para descripciones que no salen de un catálogo (PRD-NF9) |
| Recuperación de cuenta | Supabase la hace por correo, pero los correos de prueba son ficticios. **Propuesta de gamma para el PoC:** el administrador restablece la contraseña (ANA-07, VA1-07) |
| Historial (T58) | Lo construye DevSecOps. Gamma aporta casos y pruebas y lo consume en M1 y M4 |
| T31 / T61 | Son **de gamma**. T31 = pruebas del M1 escritas antes del código. T61 = diseño adelantado del M4 |
| T53 | Fichas y bocetos de pantallas: los cubren ANM-04 a ANM-06 |
| Pruebas | `pytest`. No hay porcentaje de cobertura: **cada requisito REQ-… tiene al menos una prueba que lo cita** |
| Despliegue | Gamma lo prepara y lo levanta en **test** con el integrador. DevSecOps valida y hace el pase a producción (P5) |
| Plantillas | Ficha: B5 (B13 para persistencia). Contrato: B12. Caso de uso: B11. Issue: formulario "Tarea o infraestructura" (página 26) |
| Catálogo y datos ficticios | Los arma el community manager. Gamma le pasa lo que necesita el M1 |
| Votaciones | Constitución del equipo: 7 aprobaciones. Consejo: 9 integrantes, mayoría 5 de 9 |
| **Nextcloud** | **Descartado (29/10).** Todo el seguimiento va en GitHub (issues y Project) y los documentos en el repo, en `docs/gamma/` |
| **Supabase** | El proyecto de la organización está el **martes 3/11**. Hasta entonces se trabaja contra una Auth simulada con los usuarios ficticios de Nico; conectar el real es cambiar un interruptor |

## 4. Repositorios, tickets y puertas

**Repositorios** (punto de encaje 2):

| Repo | Visibilidad | Qué va | Protección |
|---|---|---|---|
| `bolsa-it-gamma` | Público | Código, specs, contratos, fichas, tests | `main` protegido por GitHub |
| `bolsa-it-gamma-privado` | Privado | Trazas, borradores, registros de IA. **Nunca código** | Las tres barreras de la planilla (versión simplificada, INT-04) |

**Dónde va cada tarjeta:**
- **Las que implementan** (contratos, fichas, tests, código, CI, despliegue) son **issues** en `bolsa-it-gamma` con el formulario "Tarea o infraestructura" y el título `GAMMA-M1-NNN · ROL-NN · nombre`. Ejemplo: `GAMMA-M1-011 · LID-10 · genera login`. Cada tarjeta trae su número.
- **Las de documentación y diseño** (casos de uso, bocetos, actas, memoria) **también son issues** del mismo Project, con el título `GAMMA-DOC-NNN · ROL-NN · nombre` y la label `tipo:doc`. En las tarjetas figuran como `GAMMA-DOC`. Sus archivos van en `docs/gamma/` del repo público; las trazas y los borradores, en el privado.
- Columnas del tablero: `Backlog · Por hacer · En proceso · Bloqueado · En revisión · Hecho`.

**Puertas** (página 03 y punto 5 de la Constitución):

| Puerta | Qué se aprueba | Quién |
|---|---|---|
| P1 | Intención | Líder (Sebas) |
| P2 | Spec / ficha | Líder + auditora o DevSecOps |
| P3 | Plan | Un compañero |
| P4 | PR de código | Revisor de alfa |
| P5 | Producción | DevSecOps |

**Regla de oro:** una tarjeta pasa a *Hecho* solo cuando la aprueba quien figura en "Valida". Nunca quien la hizo y nunca un agente. Los bloqueos se escriben así: `Bloqueada: falta X (ID)`.

## 5. Fases

| Fase | Objetivo de referencia | Qué se logra | Puerta de salida |
|---|---|---|---|
| **F0 · Arranque** | 29/10 → 30/10 | Esqueleto Reflex con Auth simulada (INT-00), repos, issues cargados, documentos del kit en `docs/gamma/` | Tablero cargado; la app levanta en las 7 máquinas; contrato M1 v1.0 aprobado o con observaciones |
| **F1 · PoC base** | 29/10 → **3/11** | Login con tests en rojo, código y verde **contra la Auth simulada**. El 3/11 se conecta a Supabase real y se vuelven a correr los tests | **v0.1.0 mostrada el 3/11** con login en verde |
| **F2 · M1 completo** | 3/11 → ~10/11 | Tablas y RLS en Supabase real; registro, perfil con privacidad, habilitación por admin, recuperación, baja lógica | M1 con tests en verde, P4 del revisor de alfa |
| **F3 · M4 e integración** | Diseño desde ya (T61) · construcción ~5/11 → ~15/11 | Contrato y fichas del M4, tests en rojo, núcleo P40 y P42, integración con M2 y M3, correcciones de auditoría | M4 en verde e integrado, auditoría cerrada |
| **F4 · Cierre** | ~15/11 → **19/11** (docs hasta 1/12) | M1 y M4 en test con P5, documentación, ensayo | P5 de DevSecOps; T69 entregado el 24/11 |

**El diseño del M4 (F3) no espera a F2:** Thiago, Agustín y Vicente empiezan T61 apenas el PoC esté encaminado.

### Tarjetas por fase

| Fase | Sebas (LID) | Ivo (REV) | Thiago (ANA) | Facu (VA1) | Agustín (VA2) | Vicente (ANM) | Nico (INT) |
|---|---|---|---|---|---|---|---|
| F0 | 01 02 03 | 01 02 | 01 | 01 | 01 | 01 02 | 00 01 03 04 |
| F1 | 04 05 06 07 08 10 11 | 03 04 09 | 02 03 05 | 02 03 04 05 06 12 | 02 03 | 03 04 05 | 02 05 06 07 11 |
| F2 | 12 | 06 07 08 10 11 | 07 09 10 11 13 | 07 08 09 10 11 | 04 | 07 08 09 | 08 09 10 12 |
| F3 | 09 13 14 15 | 05 12 13 | 04 06 08 12 | 13 | 05 06 07 08 09 10 11 12 | 06 10 11 | 13 |
| F4 | 16 17 | 14 15 | 14 15 | 14 | 13 14 15 | 12 13 14 15 | 14 15 16 |
| **Total** | 17 | 15 | 15 | 14 | 15 | 15 | 17 |

**Total: 108 tarjetas.** Varias del kit de la semana 20 al 26/10 pueden estar ya hechas: se marcan *Hecho* con evidencia y no se rehacen.

## 6. Cadenas de traspasos

### 6.1 PoC (hasta el 3/11): lo más urgente

```
LID-04 contrato M1 (usuario_actual, tiene_rol, UsuarioPublico)
   ├─► LID-07 ficha P1 ◄─► REV-03 ficha P2   (revisión en el par)
   ├─► ANA-01 caso de uso Iniciar sesión + ficha P11
   └─► VA1-01 casos de aceptación ──► VA2-01 alineación con el contrato
                                          │
INT-00 esqueleto + Auth simulada ──► INT-05 CI ──► VA1-04 entorno ──► VA1-05 TESTS EN ROJO (login)
                                                        │
                                   LID-10 genera login ──► REV-09 revisa ──► revisor de alfa (P4)
                                                        │
                                   INT-11 integra el login en el recorrido común ──► v0.1.0 (3/11)
```

### 6.2 M1 completo

```
ANA-03 modelo de datos M1 ──(auditora)──► ANA-07 fichas de lógica ─┐
ANM-04 pantallas ──► ANM-05 fichas de interfaz ───────────────────┤
                                          REV-06 aprueba fichas ◄──┘
                                                   │
                      ANA-09 + ANM-08 casos ──► VA1-06 acepta ──► VA1-07/08/09 tests en rojo
                                                   │
                        LID-12 genera el resto del M1 ──► VA1-10 rojo→verde ──► REV-10 ──► P4 alfa
                                                   │
                        INT-12 integra con M2 y M3 ──► INT-14 despliegue en test ──► P5 DevSecOps
```

### 6.3 M4 (T61 desde ya)

```
LID-05 matriz ──► LID-13 contrato M4 ──► ANA-04 modelo de datos M4 ──► ANA-08 fichas M4
                                            ANM-06 fichas de interfaz M4 ──┘
                                                   │
                           REV-06 aprueba ──► VA2-05 acepta casos ──► VA2-07/08/09/10 tests en rojo
                           VA2-06 casos y pruebas para T58 (DevSecOps lo construye)
                                                   │
                     LID-14 genera núcleo P40 y P42 ──► VA2-12 rojo→verde ──► REV-12
                                                   │
                     INT-13 integra con T6, M2 y M3 ──► LID-15 auditoría ──► INT-15 despliegue en test ──► P5
```

## 7. Ruta crítica interna

- **PoC:** `LID-04 → LID-07/REV-03 → VA1-05 → LID-10 → REV-09 → INT-11` (contra la Auth simulada; el 3/11 se pasa a Supabase real).
- **M1:** `ANA-03 (auditora) → ANA-07 → REV-06 → VA1-07/08/09 → LID-12 → REV-10 → INT-12 → INT-14`.
- **M4:** `LID-13 → ANA-04 → ANA-08 → REV-06 → VA2-07/08 → LID-14 → REV-12 → INT-13 → LID-15 → INT-15`.
- **Infraestructura de pruebas:** `INT-03 → INT-00 → INT-05 → VA1-04`. Bloquea a los dos validadores.

**Los cuellos más probables:**
1. Ivo aprobando fichas (REV-06).
2. Los tests en rojo: sin ellos Sebas no genera código.
3. Sebas como único que genera código. Para aliviarlo, Ivo y Nico conocen el flujo y pueden generar lotes chicos si hace falta, siempre con otra persona revisando.
4. El ritmo de alfa y beta para la integración. Mientras tanto se usan simulados (INT-08).

## 8. Quién valida (control de carga)

| Validador | Cantidad aprox. | Nota |
|---|---|---|
| Sebas | ~24 | El más cargado: que no tenga más de 4 tarjetas *En revisión* a la vez |
| Ivo | ~17 | Fichas y PRs |
| Thiago | ~10 | Contratos (interno), documentación, informes |
| Facu / Agustín | ~10 cada uno | Se validan entre sí |
| Nico | ~5 | Entorno, simulados, guía de despliegue |
| Vicente | ~5 | Aportes a la documentación |
| Externos | — | Docente, auditora, DevSecOps, revisor de alfa y líderes de beta: **pedirles con anticipación** |

## 9. Ritmo de trabajo

- Un PR por tarjeta, con el ID del ticket en el título.
- Máximo **2 tarjetas *En proceso*** por persona.
- Quien termina avisa por el canal del equipo, y el validador responde antes de agarrar algo nuevo.
- Código solo de fichas aprobadas y con tests en rojo. Sin secretos, sin datos reales, solo correos `test-…@ejemplo.com`.
- Todos somos developers: cuando a alguien se le vacía la columna, ayuda en la ruta crítica.

## 10. Dependencias externas

| Quién | Qué necesitamos | Tarjetas |
|---|---|---|
| Hugo | Confirmar habilitación por admin y recuperación por admin en el PoC; validar ADR, PoC y documentación final | LID-01, LID-06, LID-11, ANM-14 |
| Revisor de alfa | Aprobar el contrato M1 (C6) y los PRs (P4) | LID-04, LID-10, LID-12 |
| Auditora | Revisar ANA-03 antes del registro; auditoría de fichas; P2 | ANA-03, LID-07, REV-03, LID-15 |
| DevSecOps | **Proyecto Supabase (3/11)**, CI base y base efímera (T10, T65), moderador automático T6, componente T58, P5 | INT-05, VA2-06, VA2-10, INT-14, INT-15 |
| Community manager | Catálogo y datos ficticios consolidados | INT-01, ANA-10 |
| Alfa / beta | `publicar_oferta`, `listar_ofertas_publicadas`, funciones de baja y restauración para el admin, revisiones cruzadas | INT-07, INT-12, INT-13, REV-07, REV-08, REV-11 |
| Consejo | Definir quién revisa el núcleo del M4 antes de la C10 | REV-12, LID-14 |

## 11. Dudas que quedan abiertas

| # | Duda | Supuesto mientras tanto | Tarjetas |
|---|---|---|---|
| 1 | ¿Hugo acepta que la recuperación de cuenta en el PoC sea "el admin restablece la contraseña"? | Sí | ANA-07, VA1-07 |
| 2 | ¿Se confirma la habilitación de alumnos por el administrador? (C6) | Sí | ANA-03, LID-12 |
| 3 | Preguntas del contrato: ¿`sesion_id` es el token de Supabase? ¿rol = tipo? ¿admin pasa cualquier `tiene_rol`? ¿correo con mayúsculas entra? | Token de Supabase; rol ≠ tipo; admin no pasa roles ajenos; el correo se normaliza a minúsculas | LID-04, VA1-05 |
| 4 | ¿Quién revisa el núcleo del M4? | Ivo, propuesto al Consejo | REV-12 |
| 5 | El modelo de dominio v0.1 deja el M4 afuera: ¿cómo se suma? | ANA-04 propone una extensión por PR a los líderes | ANA-04 |
| 6 | ¿Qué del kit 20 al 26/10 quedó hecho? | Revisarlo hoy; lo hecho pasa a *Hecho* | ver cada archivo |

## 12. Riesgos

| Riesgo | Prevención | Responsable |
|---|---|---|
| Supabase llega después del 3/11 | Todo se construye contra la Auth simulada; conectar el real es cambiar el interruptor | Nico |
| El login no llega a la demo del 3/11 | Solo login en el PoC; lo extra va en ramas propias y no bloquea | Sebas |
| Registro con datos personales sin revisar | ANA-03 pasa por la auditora antes de VA1-07 y LID-12 | Thiago |
| Fichas aprobadas tarde | Ivo reserva tiempo; las fichas salen en lotes chicos | Ivo |
| M4 apurado al final | T61 desde ya; simulados de T6, M2 y M3 | Thiago, Agustín |
| Sebas cuello de botella | Generación en lotes y apoyo de Ivo y Nico | Sebas |
| Documentación al final | Registro continuo desde F0 | Vicente |

## 13. Cambios respecto de v1.0

| Cambio | Motivo |
|---|---|
| Plan reiniciado el 27/10 con F1 = PoC base | Fecha real y prioridad del PoC del 29/10 |
| Nombres en cada rol | Asignación definitiva |
| Dos repos (público y privado); INT-02 a INT-04 simplificados | Punto de encaje 2 |
| Formato de ticket `GAMMA-M1/M4-NNN · ROL-NN` | Punto de encaje 3 |
| Máquina de estados con *en revisión*; el M4 consume T6 | Punto de encaje 4 |
| Moderador = rol global que solo modera; el nivel 2 reporta | Respuesta 6 |
| T31 y T61 son de gamma; T58 lo construye DevSecOps | Respuestas 1 y 3 |
| Fichas P1 (Sebas) y P2 (Ivo) del kit | Kit de la semana |
| Puertas P1 a P5 asignadas a cada tarjeta | Respuesta 15 |
| Datos semilla → integrador con el community manager | Respuesta 16 y kit |
| Cobertura: cada REQ con al menos una prueba que lo cita | Respuesta 12 |
| Votación: 7 aprobaciones y Consejo de 9 (5 de 9) | Punto de encaje 6 |

## 14. Cambios respecto de v1.1 (29/10)

| Cambio | Motivo |
|---|---|
| Nextcloud eliminado: las tarjetas de documentación pasan a ser issues `GAMMA-DOC-NNN` con label `tipo:doc`, y los archivos van a `docs/gamma/` | Hugo descartó Nextcloud |
| El ticket-check acepta también `GAMMA-DOC-NNN` (regex: `^GAMMA-(M1\|M4\|DOC)-[0-9]{3} · `) | Las tarjetas de documentación ahora pasan por PR |
| Tarjeta nueva **INT-00**: esqueleto Reflex con Auth simulada | No hay código ni Supabase todavía |
| PoC: el 29/10 se entrega diseño y tests en rojo; el login en verde se muestra en la demo del **3/11** | El proyecto Supabase de la organización llega el martes 3/11 |
| F1 y F2 corridas: todo se construye contra la Auth simulada y se conecta a Supabase real el 3/11 | Ídem |
| La plantilla F3 y la página 19 se toman de Classroom | Nextcloud descartado |
