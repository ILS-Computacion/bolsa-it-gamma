# Analista menor + Documentador · Vicente · v1.3

## Tu trabajo en una frase
Tenés **dos trabajos**:
1. **Diseñás las pantallas:** cómo se ven y qué hace cada una.
2. **Sos la memoria del equipo:** anotás las decisiones, cómo usamos la IA, y armás la documentación final y la memoria técnica.

Pensalo así: Thiago escribe qué hace el sistema por dentro y vos, qué ve la persona. Y además sos el que lleva el diario del proyecto, para que al final no haya que acordarse de todo de golpe.

## Cómo leer este archivo
- Cada tarea tiene **qué es**, **pasos**, **terminaste cuando** y **a quién le avisás**.
- Hacé las tareas **en el orden de "Tu orden"**.
- Todo lo que escribís va al repo, en `docs/gamma/` (Nextcloud quedó descartado). Las notas internas y los borradores van al **repo privado**.
- Al terminar: PR con el título del ticket, tarjeta a **En revisión** y aviso a quien valida.
- Si te trabás: tarjeta a **Bloqueado**, escribís `Bloqueada: falta X (ID)` y le avisás a Sebas.
- **Ojo:** seguís trabajando después del 19/11. La documentación final se entrega el 24/11 y la memoria técnica el 1/12.

## Palabras que vas a ver mucho
| Palabra | Qué significa |
|---|---|
| **Pantalla P00, P11, P40…** | Cada pantalla tiene un código. P11 = iniciar sesión, P10 = registrarse, P40 = panel, P42 = cola de moderación |
| **Mapa de pantallas** | El dibujo de todas las pantallas y de cómo se pasa de una a otra |
| **Boceto** | Un dibujo a mano o simple de la pantalla. No tiene que ser lindo: tiene que ser claro |
| **Ficha de interfaz** | La descripción escrita de una pantalla: qué muestra, qué campos y botones tiene, qué mensajes y qué cambia según quién la mira |
| **Caso de uso** | Lo que un usuario quiere lograr ("iniciar sesión"). Los escribe Thiago; tus pantallas los cumplen |
| **Rol** | Tipo de usuario: talento, empresa, particular, moderador, admin nivel 1 o admin nivel 2 |
| **Campo privado** | Un dato del perfil que solo ve su dueño. La pantalla lo tiene que ocultar a los demás |
| **Memoria técnica (F3)** | El documento final que cuenta cómo se hizo el proyecto. Se entrega el 1/12 |
| **T69** | La documentación final del prototipo. Se entrega el 24/11 |

## Plantillas
Las fichas de interfaz usan la plantilla **B5** del Kit de la semana 20-26/10. La guía de la documentación final es la **página 19, sección 3**, y la de la memoria técnica es la **plantilla F3**. Las tres están en Classroom.

## Tu orden
1. **ANM-01** → 2. **ANM-02** → 3. **ANM-09** (empezalo ya y seguí todo el proyecto) → 4. **ANM-03** → 5. **ANM-04** → 6. **ANM-05** (primero P11) → 7. **ANM-07** → 8. **ANM-08** → 9. **ANM-06** → 10. **ANM-10** (se va sumando en cada fase) → 11. **ANM-11** → 12. **ANM-12** → 13. **ANM-13** → 14. **ANM-14** → 15. **ANM-15**.

## Tabla de tareas
| ID | Tarea | Ticket | Necesitás antes | Valida |
|---|---|---|---|---|
| ANM-01 | Acta de la C5, bitácora e índice | GAMMA-DOC | — | Sebas |
| ANM-02 | Ordenar los documentos en el repo | GAMMA-DOC | ANM-01 | Sebas |
| ANM-03 | Glosario | GAMMA-DOC | — | Thiago |
| ANM-04 | Mapa de pantallas | GAMMA-DOC | Lista de casos de uso (ANA-02) | Thiago |
| ANM-05 | Fichas y bocetos de las pantallas del M1 | GAMMA-M1-014 | ANM-04 + contrato M1 | Ivo |
| ANM-06 | Fichas y bocetos de las pantallas del M4 | GAMMA-M4-004 | ANM-04 + contrato M4 | Ivo |
| ANM-07 | Mensajes y validaciones de los formularios | GAMMA-DOC | ANM-05 | Thiago |
| ANM-08 | Casos de prueba de las pantallas | GAMMA-DOC | ANM-05, ANM-06 | Facu / Agustín |
| ANM-09 | Registro de decisiones y de uso de IA | repo privado | — | Sebas |
| ANM-10 | Memoria técnica, parte de gamma | GAMMA-DOC | ANM-09 | Sebas |
| ANM-11 | Documentación del M1 | GAMMA-DOC | Pruebas del M1 terminadas | Thiago |
| ANM-12 | Documentación del M4 | GAMMA-DOC | Pruebas del M4 terminadas | Thiago |
| ANM-13 | README: cómo instalar y desplegar | GAMMA-M1-022 | M1 en test (INT-14) | Nico |
| ANM-14 | Documentación final del prototipo | GAMMA-DOC | ANM-11, ANM-12 | Hugo |
| ANM-15 | Material de la presentación | GAMMA-DOC | ANM-14 | Sebas |

---

### ANM-01 · Acta, bitácora e índice
**Qué es:** la tarea del kit de la semana. Si ya la hiciste, marcala *Hecho* con el enlace.
**Pasos:**
1. **Acta de la C5:** qué decidieron los líderes (modelo de dominio, Supabase Auth, PRD v1.0) y cómo salió la votación de la Constitución.
2. **Bitácora:** una lista con fecha y qué pasó en cada clase.
3. **Índice:** la lista de todos los documentos de gamma, con su enlace.
**Avisás a:** Sebas.

### ANM-02 · Ordenar los documentos en el repo
**Qué es:** que cualquiera encuentre cualquier documento en 10 segundos.
**Pasos:**
1. En el repo público, creá `docs/gamma/README.md`, que es la página de inicio, con el índice de ANM-01.
2. Armá estas carpetas: `docs/gamma/casos-de-uso/`, `docs/gamma/fichas/m1/`, `docs/gamma/fichas/m4/`, `docs/gamma/pantallas/` y `docs/gamma/plan/` (los archivos de rol).
3. Subí lo que ya existe: la constitución, el contrato, las fichas y las tareas de la semana.
4. Las notas, los borradores y los prompts van al **repo privado**.
**Avisás a:** Sebas y a todo el equipo, con el enlace al README.

### ANM-09 · Registro de decisiones y de uso de IA ⚠️ empezalo ya
**Qué es:** el diario del proyecto. Hugo lo pide como parte de la entrega ("las trazas"). Si lo hacés de a poco son 5 minutos por clase; si lo dejás para el final, es imposible.
**Pasos:** en el **repo privado**, dos archivos:
1. `decisiones.md`: una fila por decisión.
   | Fecha | Quién | Qué se decidió | Por qué |
   |---|---|---|---|
   | 29/10 | Hugo | Nextcloud descartado | … |
2. `registro-ia.md`: qué se le pidió a la IA y qué se hizo con la respuesta (aceptada, corregida o descartada). Lo sacás de los prompts que guarda Sebas y de las revisiones con IA de Facu y Agustín.
**Cuándo:** al final de cada clase, o cuando pase algo importante.
**Avisás a:** Sebas, una vez por semana.

### ANM-03 · Glosario
**Qué es:** una lista de palabras con su significado, para que todos usen las mismas.
**Pasos:** en `docs/gamma/glosario.md`:
1. Partí del "lenguaje del dominio" del `modelo-dominio.md` (oferta, búsqueda, publicante, talento IT…).
2. Sumá las palabras de gamma: rol, moderador, admin nivel 1 y 2, habilitar, campo privado, "en revisión", reporte y baja lógica.
3. Para cada una: **una oración** que la explique y la columna "no confundir con".
**Avisás a:** Thiago.

### ANM-04 · Mapa de pantallas
**Qué es:** el dibujo de todas las pantallas de gamma y de cómo se pasa de una a otra.
**Pasos:**
1. Listá las pantallas:
   - **M1:** P00 inicio, P01 inicio con sesión, P10 registrarse, P11 iniciar sesión, mi perfil y habilitar cuentas (solo admin).
   - **M4:** P40 panel, P42 cola de moderación, historial y reportes.
2. Al lado de cada una, escribí qué rol la usa y qué caso de uso de Thiago cumple.
3. Dibujá un recorrido por rol con flechas (por ejemplo, para el talento: P00 → P11 → P01 → mi perfil). Puede ser a mano, en una foto.
**Terminaste cuando:** está en `docs/gamma/pantallas/mapa.md`. **Avisás a:** Thiago.

### ANM-05 · Fichas y bocetos de las pantallas del M1
**Qué es:** por cada pantalla del M1, una ficha que explique exactamente qué muestra y hace, más un boceto.
**Pasos:** usá la plantilla **B5** y, por cada pantalla, respondé:
1. **Qué muestra:** títulos, textos y datos.
2. **Qué campos tiene:** por ejemplo, correo y contraseña.
3. **Qué botones y enlaces tiene, y a dónde llevan.**
4. **Qué mensajes aparecen:** errores y avisos.
5. **Qué cambia según quién la mira:** por ejemplo, la empresa no ve los campos privados.
6. **Boceto:** un dibujo a mano y su foto.
**Empezá por P11 (iniciar sesión)**, que es la primera que se programa. Si Thiago ya la hizo en ANA-01, solo la completás.
**Terminaste cuando:** las fichas están en `docs/gamma/pantallas/m1/` y las aprobó Ivo. Mandalas de a 2 o 3. **Avisás a:** Ivo.

### ANM-07 · Mensajes y validaciones
**Qué es:** la lista de todo lo que el sistema le dice al usuario cuando completa un formulario.
**Pasos:** una tabla por formulario:
| Campo | Regla | Mensaje si está mal |
|---|---|---|
| Correo | Tiene que tener @ | "Ingresá un correo válido" |
**Reglas:**
- Los mensajes **nunca** revelan si un correo existe.
- El límite de unas 300 palabras se aplica solo a textos que se escriben libremente, no a lo que sale de una lista.
- Incluí los avisos "Tu cuenta está pendiente de habilitación" y "Un moderador la va a revisar".
**Avisás a:** Thiago.

### ANM-08 · Casos de prueba de las pantallas
**Qué es:** escribir en palabras qué hay que probar de cada pantalla, para Facu y Agustín.
**Pasos:** por cada ficha, al menos 4 casos *dado / cuando / entonces*: uno normal, uno raro, uno de alguien sin permiso y uno con un campo privado. Ejemplo: "*Dado* un perfil con el teléfono privado, *cuando* lo mira una empresa, *entonces* no ve el teléfono".
**Avisás a:** Facu (M1) y Agustín (M4).

### ANM-06 · Fichas y bocetos de las pantallas del M4
**Qué es:** lo mismo que ANM-05, pero para el panel. Arrancás apenas Sebas tenga el contrato del M4.
**Pantallas:**
1. **P40, panel:** qué números muestra y qué ve cada rol.
2. **P42, cola de moderación:** la lista de publicaciones "en revisión", con el motivo que dio el moderador automático y los botones **Aprobar** y **Rechazar** (el motivo es obligatorio).
3. **Historial:** quién decidió qué y cuándo.
4. **Reportes:** cómo un admin nivel 2 reporta una publicación.
**Avisás a:** Ivo.

### ANM-10 · Memoria técnica, parte de gamma
**Qué es:** el documento grande que se entrega el 1/12. Se escribe de a poco: un pedazo al cerrar cada etapa.
**Pasos:**
1. Conseguí la **plantilla F3** en Classroom.
2. Escribí la parte de gamma en `docs/gamma/memoria-gamma.md`.
3. Al cerrar cada etapa (PoC, M1, M4), agregá qué se hizo, qué se decidió y qué problemas hubo. Sacalo de tu ANM-09.
4. El 17/11 tiene que haber un borrador completo.
5. Coordiná con los documentadores de alfa y beta para que las tres partes encajen.
**Avisás a:** Sebas.

### ANM-11 y ANM-12 · Documentación del M1 y del M4
**Qué es:** explicar cada módulo **tal como quedó**, no como se planeó.
**Pasos:** dos partes por módulo:
1. **Para usuarios:** qué puede hacer cada rol.
2. **Para técnicos:** qué datos se guardan, quién puede ver qué, cómo funciona el login con Supabase, las etapas de moderación (M4) y cómo correr los tests.
Sacá la información de las pruebas de Thiago (ANA-13 y ANA-14) y de los informes de Facu y Agustín. **Nunca** escribas claves ni contraseñas.
**Avisás a:** Thiago.

### ANM-13 · README: cómo instalar y desplegar
**Qué es:** las instrucciones para que alguien que nunca vio el proyecto lo pueda instalar.
**Pasos:** con ayuda de Nico, escribí: cómo instalar, qué variables hacen falta (solo los **nombres**, nunca los valores), cómo crear las tablas y cómo subirlo a Reflex Cloud.
**Terminaste cuando:** alguien que no lo escribió lo siguió paso a paso y funcionó. **Avisás a:** Nico.

### ANM-14 · Documentación final del prototipo (24/11)
**Qué es:** juntar todo en la entrega oficial.
**Pasos:** seguí la **página 19, sección 3** (Classroom). Incluí la documentación de M1 y M4, el README, el glosario y las trazas (tu registro de decisiones y de IA). Revisá que sea coherente con lo de alfa y beta.
**Avisás a:** Hugo, Sebas e Ivo (que lo revisa en REV-15).

### ANM-15 · Material de la presentación (27/11)
**Qué es:** las diapositivas o el material de la parte de gamma para la presentación, más el ensayo.
**Avisás a:** Sebas.
