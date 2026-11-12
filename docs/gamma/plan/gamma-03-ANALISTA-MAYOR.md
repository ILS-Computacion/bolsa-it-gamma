# Analista mayor · Thiago · v1.3

## Tu trabajo en una frase
**Escribís en castellano, con detalle, qué tiene que hacer el sistema**, para que Facu y Agustín puedan escribir los tests y Sebas pueda generar el código sin adivinar nada.

Pensalo así: vos sos el que escribe la "receta". Si la receta dice "agregar sal a gusto", el cocinero (la IA) inventa. Si dice "5 gramos de sal", sale bien.

## Cómo leer este archivo
- Cada tarea tiene **qué es**, **pasos**, **terminaste cuando** y **a quién le avisás**.
- Hacé las tareas **en el orden de la sección "Tu orden"**, no por número.
- Cuando termines una: subís el archivo a `docs/gamma/` del repo con un PR (título: el ticket de la tabla), movés la tarjeta a **En revisión** y le avisás a quien valida.
- Si te trabás: movés la tarjeta a **Bloqueado**, escribís `Bloqueada: falta X (ID)` y le avisás a Sebas.

## Palabras que vas a ver mucho
| Palabra | Qué significa |
|---|---|
| **Caso de uso** | Una cosa que un usuario quiere lograr, contada paso a paso. Ej: "el alumno inicia sesión" |
| **Ficha** | La descripción exacta de una función: qué recibe, qué hace, qué devuelve y qué errores tiene, con ejemplos |
| **Modelo de datos** | La lista de qué información guardamos (tablas y campos) y quién puede ver cada campo |
| **Contrato** | Lo que el M1 o el M4 le promete al resto. Lo escribe Sebas; vos lo controlás |
| **REQ / PRD** | El código de un requisito (ej: PRD-14 "nada se publica sin moderación"). Cada ficha cita el suyo |
| **Dado / cuando / entonces** | Forma de escribir un caso de prueba: *dado* un usuario dado de baja, *cuando* intenta entrar, *entonces* ve "Correo o contraseña incorrectos" |

## Plantillas que usás
Están en el **Kit de la semana 20-26/10** (Classroom): **B11** para casos de uso, **B5** para fichas de lógica y **B13** para fichas de persistencia (las que guardan o buscan datos). Copiá la plantilla y completala; no inventes un formato propio.

## Tu orden
1. **ANA-01** → 2. **ANA-02** → 3. **ANA-05** → 4. **ANA-03** → 5. **ANA-07** → 6. **ANA-09** (M1) → 7. **ANA-11** → 8. **ANA-04** → 9. **ANA-08** → 10. **ANA-09** (M4) → después ANA-10, ANA-06, ANA-12, ANA-13, ANA-14 y ANA-15 cuando lleguen.

## Tabla de tareas
| ID | Tarea | Ticket | Necesitás antes | Valida |
|---|---|---|---|---|
| ANA-01 | Caso de uso "Iniciar sesión" + ficha de la pantalla P11 | GAMMA-DOC | Contrato M1 (LID-04) | Sebas |
| ANA-02 | Lista de todos los casos de uso de M1 y M4 | GAMMA-DOC | ANA-01 | Sebas |
| ANA-03 | Modelo de datos del M1 y privacidad | GAMMA-M1-004 | LID-04 | Ivo + auditora |
| ANA-04 | Modelo de datos del M4 | GAMMA-M4-002 | Contrato M4 (LID-13) | Ivo + líderes |
| ANA-05 | Controlar el contrato del M1 | GAMMA-DOC | LID-04 | Sebas |
| ANA-06 | Controlar la matriz de permisos y el contrato del M4 | GAMMA-DOC | LID-05, LID-13 | Sebas |
| ANA-07 | Fichas del M1 | GAMMA-M1-013 | ANA-03 | Ivo |
| ANA-08 | Fichas del M4 | GAMMA-M4-003 | ANA-04 | Ivo |
| ANA-09 | Casos de prueba de cada ficha | GAMMA-DOC | Fichas aprobadas | Facu (M1) / Agustín (M4) |
| ANA-10 | Pedido de datos ficticios al community manager | GAMMA-DOC | ANA-03 | Nico |
| ANA-11 | Tabla de trazabilidad | GAMMA-DOC | ANA-07 | Sebas |
| ANA-12 | Responder a la auditora | GAMMA-DOC | Informe de la auditora | Auditora |
| ANA-13 | Probar el M1 como usuario | GAMMA-DOC | M1 generado (LID-12) | Sebas |
| ANA-14 | Probar el M4 como usuario | GAMMA-DOC | M4 generado (LID-14) | Sebas |
| ANA-15 | Pasarle tu material a Vicente | GAMMA-DOC | ANM-14 | Vicente |

---

### ANA-01 · Caso de uso "Iniciar sesión" + ficha de P11
**Qué es:** contar paso a paso cómo alguien entra al sistema, y describir la pantalla de login (P11). Es lo primero que se programa, así que es urgente.

**Pasos:**
1. Abrí la plantilla **B11** y completá:
   - **Actor:** quién lo hace (empresa, particular o talento).
   - **Objetivo:** "entrar al sistema con mi cuenta".
   - **Antes de empezar:** el usuario tiene una cuenta habilitada.
   - **Flujo normal:** 1) escribe correo y contraseña, 2) toca Ingresar, 3) el sistema lo lleva a su inicio.
   - **Alternativa A:** contraseña incorrecta → ve "Correo o contraseña incorrectos" (el mensaje **no dice** cuál de los dos falló).
   - **Alternativa B:** cuenta no habilitada o dada de baja → ve el mismo mensaje y no entra.
2. Ficha de la pantalla P11: campos (correo, contraseña), botón **Ingresar**, enlace "¿Olvidaste tu contraseña?" (lleva a un mensaje que dice que le pida al admin que la restablezca) y los mensajes de error.
3. Hacé un boceto a mano, sacale una foto y adjuntala.
4. Revisá que las palabras coincidan con el contrato de Sebas (por ejemplo, `usuario_actual`, `tiene_rol`).

**Terminaste cuando:** `docs/gamma/casos-de-uso/iniciar-sesion.md` está en el repo con el boceto.
**Avisás a:** Sebas. Si ya lo habías hecho del kit, marcalo como *Hecho* con el enlace.

### ANA-02 · Lista de casos de uso
**Qué es:** una tabla con **todo** lo que los usuarios pueden hacer en M1 y M4, una fila por caso. No hace falta el detalle de ANA-01: una línea cada uno.

**Pasos:** copiá esta lista y completá una fila por caso, con actor, objetivo y cómo termina.
- **M1:** Registrarse · Iniciar sesión · Gestionar mi perfil (incluye privacidad y currículum) · Recuperar el acceso · Habilitar cuentas (admin) · Dar de baja mi cuenta.
- **M4:** Ver métricas del panel · Moderar publicaciones · Gestionar usuarios · Ver el registro de moderación · Reportar una publicación (admin nivel 2).

**Ojo:** no hables de botones ni colores. "El talento cambia su perfil a privado", no "toca el switch azul".
**Terminaste cuando:** está la tabla en `docs/gamma/casos-de-uso/lista.md`. **Avisás a:** Sebas.

### ANA-05 · Controlar el contrato del M1
**Qué es:** revisar lo que escribió Sebas como un segundo par de ojos, antes de que lo vea el revisor de alfa.

**Pasos:** abrí el contrato y respondé estas 4 preguntas en un comentario del PR:
1. ¿Cada caso de uso de ANA-02 se puede hacer con las funciones del contrato? Si falta algo, decí qué.
2. ¿Hay alguna función que no usa ningún caso de uso? Si sobra algo, decí cuál.
3. ¿Cada función tiene ejemplos y dice qué error devuelve?
4. ¿Algún dato que expone el contrato es privado (correo, contraseña)? No debería.

**Terminaste cuando:** dejaste el comentario con las 4 respuestas. **Avisás a:** Sebas.

### ANA-03 · Modelo de datos del M1 y privacidad ⚠️ importante
**Qué es:** decidir qué información guardamos de cada usuario y quién puede verla. **No se puede programar el registro hasta que la auditora revise esto.**

**Pasos:**
1. Hacé una tabla por cada cosa que guardamos: **usuario** (lo conecta con Supabase Auth), **perfil de talento**, **publicante** (empresa o particular) y **categoría** (por ahora solo "IT", pero tiene que poder sumarse "electrónica" y "artística").
2. Por cada campo, completá estas columnas:

| Campo | Para qué sirve | Obligatorio | ¿Quién lo ve? |
|---|---|---|---|
| nombre_publico | Que la empresa sepa con quién habla | Sí | Público |
| telefono | Que la empresa lo contacte | No | Solo empresas |
| ... | | | Público / Solo empresas / Privado |

3. Reglas que **no se negocian**:
   - Si un dato no hace falta para trabajar, **no se pide**.
   - **Nunca** se pide edad, género, origen ni domicilio.
4. Agregá estos campos técnicos al usuario: `habilitado` (sí/no, lo cambia el admin) y `eliminado_en` (fecha de baja; no se borra nada, solo se marca).

**Terminaste cuando:** está `docs/gamma/modelo-datos-m1.md` y la auditora lo revisó.
**Avisás a:** Ivo y a la auditora (Emma). **Avisale a Sebas el mismo día que lo subas**, porque frena a otros.

### ANA-07 · Fichas del M1
**Qué es:** escribir una ficha por cada función del M1 que todavía no tiene la suya. Las fichas P1 (Sebas) y P2 (Ivo) ya están; vos hacés el resto.

**Las fichas que te tocan:**
| Ficha | Plantilla | Qué hace la función |
|---|---|---|
| ALG-M1-P3 | B13 | Actualizar el perfil: se guarda un borrador y se aplica cuando el usuario confirma |
| ALG-M1-P4 | B13 | Dar de baja una cuenta: se completa `eliminado_en`, no se borra |
| Registrar talento | B5 | Crea la cuenta **sin habilitar** |
| Habilitar cuenta | B5 | Solo el admin; pasa `habilitado` a sí |
| Cambiar privacidad de un campo | B5 | El dueño elige público, solo empresas o privado |
| Restablecer contraseña | B5 | Solo el admin le pone una contraseña nueva a alguien |
| Regla de `tiene_rol` | B5 | Cómo se decide si un usuario tiene un rol |

**Cada ficha tiene que tener:** qué recibe, qué devuelve, los pasos, los errores y **al menos 5 ejemplos** (uno normal, dos raros, dos de error), además del REQ que cumple.
**Truco:** si al leer tu ficha alguien pregunta "¿y qué pasa si…?", la respuesta tiene que estar en la ficha.

**Terminaste cuando:** las 7 fichas están en `docs/gamma/fichas/m1/` y las aprobó Ivo. Mandalas de a 2 o 3, no todas juntas al final. **Avisás a:** Ivo.

### ANA-09 · Casos de prueba de cada ficha
**Qué es:** por cada ficha aprobada, escribir en castellano las situaciones que hay que probar. Facu y Agustín las convierten en código de test.

**Pasos:** por cada ficha, escribí al menos 4 casos con este formato:
```
REQ-M1-007 · Habilitar cuenta
1. Normal:   Dado un talento sin habilitar, cuando el admin lo habilita, entonces puede iniciar sesión.
2. Borde:    Dado un talento ya habilitado, cuando el admin lo habilita otra vez, entonces no cambia nada y no da error.
3. Error:    Dado un id que no existe, cuando el admin lo habilita, entonces devuelve UsuarioNoEncontrado.
4. Permiso:  Dado un talento, cuando intenta habilitar a otro, entonces recibe "sin permiso".
```
**Terminaste cuando:** Facu (M1) o Agustín (M4) te dicen "con esto puedo escribir los tests sin preguntarte nada". **Avisás a:** Facu o Agustín.

### ANA-11 · Tabla de trazabilidad
**Qué es:** una tabla que conecta cada requisito con todo lo que lo cumple. Sirve para demostrar que **cada requisito tiene al menos un test**.

**Pasos:** creá `docs/gamma/trazabilidad.md` y agregá una fila cada vez que algo pasa a *Hecho*:
| REQ | Caso de uso | Ficha | Test | PR |
|---|---|---|---|---|
| REQ-M1-001 | Iniciar sesión | ALG-M1-P2 | test_login_ok | #12 |

**Terminaste cuando:** al final del proyecto no hay ningún REQ con la columna Test vacía. **Avisás a:** Sebas.

### ANA-04 · Modelo de datos del M4
**Qué es:** lo mismo que ANA-03, pero para la moderación. El modelo de dominio de los líderes **no incluye el M4**, así que lo proponés vos.

**Pasos:** describí estas tablas con sus campos:
1. **Estado de moderación** de cada publicación (oferta o búsqueda): `enviada`, `en revisión`, `publicada` o `rechazada`.
2. **Resultado del moderador automático (T6):** si pasó o no y el motivo.
3. **Revisión humana:** quién revisó, cuándo, qué decidió y por qué.
4. **Reporte:** un admin de nivel 2 avisa que algo está mal.
5. **Qué necesitamos que alfa y beta nos den** (por ejemplo, "listar las ofertas en revisión"). Esta lista se la pasás a Nico.

**Terminaste cuando:** está `docs/gamma/modelo-datos-m4.md` y lo aprobaron Ivo y los líderes. **Avisás a:** Ivo, Sebas y Nico.

### ANA-08 · Fichas del M4
**Qué es:** igual que ANA-07, pero para el M4. **No esperes al 12/11**: arrancá apenas Sebas tenga el contrato del M4.

**Las fichas que te tocan:**
1. Recibir el resultado del automático y mandar la publicación a la cola *en revisión* si hubo un problema.
2. Aprobar una publicación (pasa a *publicada*).
3. Rechazar una publicación (el motivo es **obligatorio**).
4. Guardar cada decisión en el historial.
5. Reportar una publicación (admin nivel 2).
6. Calcular las métricas del panel (por ejemplo, cuántas hay en revisión).

Mismas reglas que en ANA-07: al menos 5 ejemplos por ficha. **Terminaste cuando:** están en `docs/gamma/fichas/m4/` y aprobadas por Ivo. **Avisás a:** Ivo.

### ANA-06 · Controlar la matriz de permisos y el contrato del M4
**Qué es:** revisar que cada acción del M4 tenga su permiso, su caso de uso y su dato.
**Pasos:** por cada fila de la matriz de Sebas, preguntate: ¿hay un caso de uso que la use? ¿hay un campo en ANA-04 que la soporte? Anotá lo que falte.
**Avisás a:** Sebas.

### ANA-10 · Pedido de datos ficticios
**Qué es:** decirle al community manager qué usuarios de mentira necesitamos para probar.
**Pasos:** mandale una lista: talentos de cada nivel (trainee, junior, freelancer), uno sin habilitar, uno dado de baja, empresas y particulares. Todo inventado, con correos `test-…@ejemplo.com`.
**Avisás a:** Nico, que es quien los carga.

### ANA-12 · Responder a la auditora
**Qué es:** cuando la auditora encuentra un problema en una ficha, lo corregís en la **ficha** (no solo en el código).
**Avisás a:** la auditora, Sebas y el validador del módulo.

### ANA-13 y ANA-14 · Probar como usuario
**Qué es:** cuando el módulo ya está en el ambiente de test, lo usás como lo usaría una persona real.
**Pasos:** recorré cada caso de uso de ANA-02 y anotá en `docs/gamma/aceptacion-m1.md` (o `-m4.md`): ✅ funciona o ❌ falla, con qué pasó. Para el M4 probá el recorrido completo: la empresa envía → el automático la marca → queda en revisión → el moderador aprueba o rechaza → queda en el historial.
**Avisás a:** Sebas.

### ANA-15 · Material para la documentación
**Qué es:** pasarle a Vicente tus casos de uso, modelos, trazabilidad y pruebas para la documentación final, y estar en el ensayo.
**Avisás a:** Vicente.
