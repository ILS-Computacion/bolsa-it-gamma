# Revisor · Ivo · v1.3

## Tu trabajo en una frase
**Sos el control de calidad: nada pasa al siguiente paso sin tu OK.** Aprobás las fichas antes de que se escriban los tests y revisás el código antes de que entre al repo.

Pensalo así: sos el que firma "revisado" en cada pieza. Si dejás pasar una ficha confusa, la IA programa algo confuso. Si dejás pasar un PR con una clave escrita o un permiso mal puesto, queda en el sistema.

## Cómo leer este archivo
- Cada tarea tiene **qué es**, **pasos**, **terminaste cuando** y **a quién le avisás**.
- Hacé las tareas **en el orden de "Tu orden"**.
- Muchas tareas tuyas no son "hacer algo nuevo", sino **revisar lo de otro**: dejás comentarios en su PR y, si está bien, tocás **Approve**.
- Si te trabás: tarjeta a **Bloqueado**, escribís `Bloqueada: falta X (ID)` y le avisás a Sebas.

## Palabras que vas a ver mucho
| Palabra | Qué significa |
|---|---|
| **Ficha** | Descripción exacta en castellano de una función: qué recibe, qué hace, qué devuelve, errores y ejemplos |
| **PR** | Pull request: el pedido de "sumen mi cambio". Lo revisás en GitHub, en la pestaña *Files changed* |
| **Approve / Request changes** | Los dos botones de GitHub para aprobar un PR o devolverlo con pedidos de cambio |
| **Contrato** | Lo que el M1 promete al resto (nombres de funciones y datos). Lo escribe Sebas |
| **Matriz de permisos** | La tabla de quién puede hacer qué (rol × acción) |
| **RLS** | Reglas dentro de la base de datos que impiden que alguien lea o cambie datos que no son suyos |
| **REQ / PRD** | El número del requisito que cumple cada cosa. Cada test y cada ficha tienen que citarlo |
| **Puerta P2 / P4** | Los controles oficiales: P2 es la aprobación de una ficha y P4 la de un PR de código (esta última la da el revisor de alfa, después de vos) |
| **Revisión cruzada** | El revisor de alfa revisa lo nuestro, y vos revisás lo de beta (M3) |

## Las dos listas que usás siempre
**Al revisar una ficha:**
- [ ] Sigue la plantilla (B5, o B13 si guarda o busca datos).
- [ ] Tiene al menos 5 ejemplos: normal, raros y errores.
- [ ] Dice qué pasa en cada error.
- [ ] No pide ni usa edad, género, origen ni domicilio.
- [ ] Cita su REQ.
- [ ] Alguien podría programarla **sin preguntarle nada al autor**.

**Al revisar un PR:**
- [ ] El CI está en verde (tests y ticket-check).
- [ ] Cada test cita su REQ.
- [ ] El código hace lo que dice la ficha, **ni más ni menos**.
- [ ] Hace un solo cambio.
- [ ] No hay contraseñas, claves ni datos reales.
- [ ] Los permisos coinciden con la matriz.

## Tu orden
1. **REV-02** (tus listas) → 2. **REV-03** (tu ficha, urgente) → 3. **REV-04** → 4. **REV-09** → 5. **REV-06** (va todo el proyecto, de a tandas) → 6. **REV-10** → 7. **REV-05** → 8. **REV-12** → 9. **REV-13** → 10. **REV-14** → 11. **REV-15**. Cuando beta tenga material, sumás **REV-07, REV-08 y REV-11**. REV-01 es solo votar.

## Tabla de tareas
| ID | Tarea | Ticket | Necesitás antes | Valida |
|---|---|---|---|---|
| REV-01 | Votar la Constitución General | GAMMA-DOC | — | Hugo |
| REV-02 | Armar tus listas de revisión | GAMMA-DOC | — | Sebas |
| REV-03 | Escribir la ficha P2 (buscar usuario) | GAMMA-M1-006 | Contrato M1 | Sebas → auditora |
| REV-04 | Revisar el contrato M1 y la ficha P1 de Sebas | GAMMA-DOC | LID-04, LID-07 | Thiago |
| REV-05 | Revisar la matriz y el contrato del M4 | GAMMA-DOC | LID-05, LID-13 | Thiago |
| REV-06 | Aprobar las fichas de M1 y M4 | GAMMA-DOC | Fichas escritas | Auditora |
| REV-07 | Revisar las fichas de beta (M3) | GAMMA-DOC | Fichas de beta | Líder de beta |
| REV-08 | Revisar el primer PR de beta | GAMMA-DOC | PR de beta | Líder de beta |
| REV-09 | Revisar el PR del login | en el PR de GAMMA-M1-011 | LID-10 | Sebas |
| REV-10 | Revisar los PRs del resto del M1, con seguridad | en los PRs | LID-12 | DevSecOps |
| REV-11 | Revisar el código de beta (M3) | GAMMA-DOC | Código de beta | Líder de beta |
| REV-12 | Revisar los PRs del M4 | en los PRs | LID-14 | Sebas |
| REV-13 | Revisar las correcciones de la auditoría | en los PRs | LID-15 | Auditora |
| REV-14 | Revisar la lista de despliegue | GAMMA-DOC | LID-16 | DevSecOps |
| REV-15 | Revisar la documentación final | GAMMA-DOC | ANM-14 | Sebas |

---

### REV-01 · Votar la Constitución General
**Qué es:** sos parte del Consejo (9 integrantes, ganan 5 de 9). Votás aprobando el PR de la Constitución.
**Terminaste cuando:** votaste. Si ya lo hiciste, marcalo *Hecho* con el enlace. **Avisás a:** Sebas.

### REV-02 · Armar tus listas de revisión
**Qué es:** dejar por escrito las dos listas de arriba, así todos saben qué vas a mirar antes de mandarte algo.
**Pasos:** copiá las dos listas a `docs/gamma/checklist-revision.md`. Si la lista B1 del Cap. 27 (Classroom) trae algo que falte, sumalo.
**Terminaste cuando:** está en el repo. **Avisás a:** Sebas y a todo el equipo.

### REV-03 · Ficha P2: buscar un usuario ⚠️ urgente
**Qué es:** la ficha de la función que busca un usuario. La necesita el login, así que va antes que casi todo.
**Pasos:** usá la plantilla **B13** del kit (sección 4, "ALG-M1-P2") y completá:
1. **Dos búsquedas:**
   - **Por correo:** solo se usa adentro del M1, para el login.
   - **Por id:** la usan los otros módulos y devuelve el usuario **sin** correo ni contraseña (`UsuarioPublico`).
2. **Reglas:**
   - El correo se pasa a minúsculas antes de buscar (`Ana@x.com` = `ana@x.com`).
   - No devuelve usuarios dados de baja ni sin habilitar.
   - Si no existe, devuelve el error `UsuarioNoEncontrado`.
3. **Ejemplos:** al menos 5 (por ejemplo: encontrado, correo con mayúsculas, dado de baja, no existe, id inválido).
4. **Eficiencia:** la búsqueda tiene que ser rápida, así que lleva un índice sobre el correo y el id.
**Terminaste cuando:** la ficha está en `docs/gamma/fichas/m1/` y Sebas la revisó. **Avisás a:** Sebas.

### REV-04 · Revisar el contrato M1 y la ficha P1
**Qué es:** el primer control de lo que escribió Sebas, antes de que lo vea el revisor de alfa.
**Pasos:** en el PR del contrato, controlá:
1. Que cada función tenga ejemplos y diga qué errores devuelve.
2. Que los nombres coincidan con el modelo de dominio.
3. Que no se expongan datos privados.
Después hacé lo mismo con la ficha P1 de Sebas, usando tu lista de fichas.
**Terminaste cuando:** dejaste comentarios o aprobaste. **Avisás a:** Sebas y Thiago.

### REV-09 · Revisar el PR del login
**Qué es:** el primer código real del proyecto. Lo revisás vos y después el revisor de alfa.
**Pasos:** pasá tu lista de PR y prestá atención a tres cosas en especial:
1. Si la contraseña o el correo están mal, el mensaje es el mismo ("Correo o contraseña incorrectos"), sin decir cuál de los dos falló.
2. Una sesión vencida da el error `SesionInvalida`.
3. `tiene_rol` responde lo que dice la tabla del contrato.
**Terminaste cuando:** tocaste Approve o pediste cambios concretos. **Avisás a:** Sebas.

### REV-06 · Aprobar las fichas de M1 y M4 ⚠️ el cuello de botella
**Qué es:** **ninguna ficha pasa a tests ni a código sin tu OK.** Es tu tarea más importante y dura todo el proyecto.
**Pasos:**
1. Thiago y Vicente te mandan sus fichas de a 2 o 3.
2. Pasá tu lista de fichas por cada una.
3. Si está bien, comentá "Aprobada" y aprobá el PR. Si no, comentá **qué cambiar** (no solo "está mal") y tocá *Request changes*.
4. Primero van las del M1 y después las del M4.
**Truco:** intentá responder en el mismo día, porque mientras una ficha espera, Facu y Agustín no pueden avanzar.
**Terminaste cuando:** cada ficha dice "aprobada" o "devuelta con motivo". **Avisás a:** el autor y al validador que la va a usar.

### REV-10 · Revisar los PRs del resto del M1, con seguridad
**Qué es:** igual que REV-09, pero con todo lo que viene después del login.
**Además de tu lista, probá estas seis cosas:**
1. Un talento no ve los campos privados de otro.
2. Una empresa no ve campos privados.
3. Una cuenta sin habilitar no puede entrar.
4. Solo el admin puede restablecer contraseñas.
5. Dar de baja no borra nada: solo marca la fecha.
6. Los tests de permisos se corren como usuario común, no como administrador (si no, la regla nunca se pone a prueba).
**Terminaste cuando:** anotaste lo revisado en `docs/gamma/revision-seguridad-m1.md`. **Avisás a:** Sebas y DevSecOps.

### REV-05 · Revisar la matriz y el contrato del M4
**Qué es:** controlar que las reglas de moderación tengan sentido antes de programarlas.
**Pasos:** comprobá que:
1. Ninguna publicación pueda quedar trabada en una etapa sin salida.
2. El moderador solo pueda moderar, aunque sobre todas las publicaciones.
3. El admin nivel 2 solo pueda reportar.
4. Cada acción del panel tenga su fila en la matriz.
**Avisás a:** Sebas y Thiago.

### REV-12 · Revisar los PRs del M4
**Qué es:** igual que REV-10, pero para el M4.
**Además de tu lista, comprobá que:**
1. No se pueda publicar algo "en revisión" sin que lo apruebe un moderador.
2. Rechazar sin motivo dé error.
3. Cada decisión quede en el historial.
4. El admin nivel 2 no pueda aprobar ni rechazar.
**Avisás a:** Sebas. Si el Consejo pone a otra persona a revisar el M4, le pasás esta tarjeta.

### REV-13 · Revisar las correcciones de la auditoría
**Qué es:** la auditora encuentra problemas y Sebas los corrige. Vos comprobás que cada corrección arregle **ese** problema sin romper otra cosa (los tests siguen en verde).
**Avisás a:** la auditora.

### REV-14 · Revisar la lista de despliegue
**Qué es:** antes de subir la app, controlás que esté todo listo.
**Pasos:** comprobá que:
1. Las variables estén nombradas, pero **sin** sus valores, en el repo.
2. Las tablas se creen desde cero.
3. La app arranque en una máquina limpia siguiendo el README.
**Avisás a:** Nico y DevSecOps.

### REV-15 · Revisar la documentación final
**Qué es:** leer lo que armó Vicente y comprobar que describa lo que **realmente** existe. Además, estar en el ensayo.
**Avisás a:** Vicente y Sebas.

### REV-07, REV-08 y REV-11 · Trabajo cruzado con beta
**Qué es:** así como el revisor de alfa revisa lo nuestro, vos revisás lo de beta (M3, búsquedas), con las mismas dos listas.
- **REV-07:** sus fichas.
- **REV-08:** su primer PR.
- **REV-11:** el resto de su código.
**Extra:** anotá 2 o 3 cosas que hayas aprendido de ellos y que nos sirvan a nosotros.
**Avisás a:** el líder de beta.
