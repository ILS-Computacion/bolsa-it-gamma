# Constitución del equipo gamma · v1.0

> Fecha: 05/11/2026 · Reemplaza al borrador v0.1 · Aprobada en PR: [#]
> Puede agregar reglas a la Constitución General, pero no contradecirla. La valida Hugo.

## 1. Misión

- **Área a cargo:** M1 (usuarios) y M4 (panel y moderación) de la Bolsa de Trabajo IT.
- **En una frase:** "El equipo gamma existe para desarrollar el M1 (usuarios) y el M4 (panel y moderación) de la Bolsa de Trabajo IT".
- **Tickets:** `GAMMA-M1-NNN · …`, `GAMMA-M4-NNN · …` y `GAMMA-DOC-NNN · …` (label `tipo:doc`).

## 2. Integrantes

| Rol | Nombre | GitHub | Prefijo de tareas |
|---|---|---|---|
| Líder | Sebastián López | @accurateend143 | LID |
| Revisor | Ivo Albacete | @IvoAlbacete | REV |
| Analista mayor | Thiago Fajin | @thiago846 | ANA |
| Validador 1 (tests M1) | Facundo Coca | @Facu-Coca | VA1 |
| Validador 2 (tests M4 e integración) | Agustín Porcelli | @AgusPorce | VA2 |
| Analista menor + documentador | Vicente Cánobas | @vicente592 | ANM |
| Integrador | Nicolás Ferreyra | @NicoFerreyra07 | INT |

- **Suplente del líder:** Ivo.
- **Suplente del revisor:** [a definir].
- **Revisión cruzada (P4):** a gamma la revisa el revisor de alfa; el revisor de gamma (Ivo) revisa a beta.
- **Consejo:** líderes y revisores de los equipos; decide por mayoría de 5 de 9.

## 3. Cómo trabajamos

- **Sin reuniones fijas.** Cada integrante tiene sus tareas individuales en el GitHub Project. No tienen horario, pero algunas dependen de tareas de otros: la tarjeta indica de quién depende y a quién bloquea.
- **Bloqueos:** si una tarea depende de otra que no está lista, pasa a *Bloqueado* con "Bloqueada: falta X (ID)" y se avisa en el grupo a la persona y al líder.
- **Canal del equipo:** grupo de WhatsApp. Las decisiones se registran en GitHub (issue o PR), no solo en el chat.
- **Tiempo máximo para responder una revisión:** 24 h.

### Método de trabajo

1. Se escribe la ficha en lenguaje natural.
2. Ivo la aprueba.
3. Los validadores escriben los tests, que deben fallar (en rojo).
4. El líder genera el código hasta que los tests pasan (en verde).
5. Ivo revisa el PR y luego el revisor de alfa da la aprobación (P4).
6. Nico lo une a `main`.

**Reglas:**
- Sin ficha aprobada no hay tests, y sin tests en rojo no hay código.
- Si un test falla, se corrige el código o la ficha, nunca el test.
- Nadie aprueba su propio trabajo y la IA no aprueba nada.
- Un cambio por PR. El título del PR lleva el formato del ticket.

### Puertas de control

Una puerta es el punto donde alguien distinto del autor tiene que aprobar para seguir.

| Puerta | Qué se aprueba | Quién aprueba |
|---|---|---|
| P1 | La intención de la tarea | Líder |
| P2 | La ficha | Líder + auditora o DevSecOps |
| P3 | El plan de una tarea | Un compañero distinto del autor |
| P4 | El PR | Revisor de alfa |
| P5 | El pase a producción | DevSecOps |

## 4. Herramientas y repositorios

- **Stack:** Reflex + Supabase (Supabase Auth) + Reflex Cloud. Descartados: Railway, FastAPI, Nextcloud y los agentes de Paca.
- **IA:**
  - El código del producto lo genera solo el líder, con Claude Code.
  - El resto usa Cursor (versión gratuita) para tests, fichas, bocetos, configuración y revisiones asistidas.
  - Si el líder se satura, Ivo o Nico pueden generar lotes chicos con Cursor, siempre con otra persona revisando.
- **Usos libres de la IA:** explicar conceptos, generar ideas, revisar redacción, sugerir estructura y buscar errores.
- **Revisión extra obligatoria:** código que toca datos, decisiones de arquitectura, textos de esta constitución y todo lo que se entregue como terminado.
- **Repositorios:**
  - `bolsa-it-gamma` (público): código, contratos, fichas y tests. La documentación va en `docs/gamma/`.
  - `bolsa-it-gamma-privado`: trazas, prompts y borradores.

## 5. Datos y seguridad

- El sistema nunca pide ni usa **edad, género, origen ni domicilio**.
- Ningún secreto (contraseñas, claves, tokens) va al repo ni al chat: las credenciales se guardan en Bitwarden.
- En pruebas se usan solo datos ficticios (correos `test-…@ejemplo.com`).

## 6. Decisiones y desacuerdos

- Las decisiones del equipo se toman por mayoría simple: 4 de 7.
- Si no hay mayoría, desempatan Sebas y Facu.

## 7. Acuerdos de convivencia

1. Avisar con anticipación si no se puede cumplir algo, para que alguien pueda cubrir.
2. Respetar las opiniones de todos y decidir en equipo cuando haya desacuerdo.
3. Cumplir los plazos acordados o avisar a tiempo en el grupo.

## 8. Cambios a esta constitución

Cualquier cambio se hace por PR y necesita otra vez las 7 aprobaciones y la validación de Hugo.

## 9. Firma

Cada integrante aprueba el PR de este archivo.

| Integrante | Aprobó |
|---|---|
| Sebastián | X |
| Ivo | ☐ |
| Thiago | ☐ |
| Facundo | ☐ |
| Agustín | ☐ |
| Vicente | ☐ |
| Nicolás | ☐ |

## Cambios

| Versión | Fecha | Cambio |
|---|---|---|
| 0.1 | — | Borrador inicial |
| 1.0 | 05/11/2026 | Roles actualizados (líder Sebas, revisor Ivo), método, puertas, herramientas, datos y desempate |
