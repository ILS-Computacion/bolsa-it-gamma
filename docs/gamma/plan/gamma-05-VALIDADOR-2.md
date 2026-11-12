# Validador 2 · Agustín · v1.3

## Tu trabajo en una frase
**Escribís pruebas automáticas que dicen si el M4 funciona**, y las escribís **antes** de que exista el código. Mientras tanto, revisás las pruebas de Facu.

Pensalo así: vos armás el examen antes de que la IA estudie. Sebas genera código hasta que la IA "aprueba" tu examen. Si tu examen es flojo, aprueba con código malo.

## Cómo leer este archivo
- Cada tarea tiene **qué es**, **pasos**, **terminaste cuando** y **a quién le avisás**.
- Hacé las tareas **en el orden de "Tu orden"**.
- Al terminar: PR con el título del ticket, tarjeta a **En revisión** y aviso a quien valida.
- Si te trabás: tarjeta a **Bloqueado**, escribís `Bloqueada: falta X (ID)` y le avisás a Sebas.

## Palabras que vas a ver mucho
| Palabra | Qué significa |
|---|---|
| **Test / prueba** | Un pedacito de código que usa una función y comprueba que el resultado sea el esperado |
| **pytest** | La herramienta con la que escribimos y corremos los tests (`pytest` en la terminal) |
| **Test en rojo** | Un test que falla. Al principio **tiene** que fallar, porque todavía no hay código |
| **Rojo → verde** | Sebas genera código hasta que los tests pasan |
| **Fixture** | Datos de mentira que se preparan antes de cada test (un moderador, una oferta en revisión…) |
| **Simulado** | Una versión de mentira de algo que todavía no existe (alfa, beta o el moderador automático T6) |
| **Máquina de estados** | Las etapas por las que pasa una publicación y por cuáles puede pasar a cuáles |
| **T6** | El moderador automático (lo hace DevSecOps). Mira la publicación y dice "OK" o "problema: motivo" |
| **T58** | El historial (lo hace DevSecOps). Guarda quién cambió qué, cuándo y por qué |

## Cómo se ve un test
```python
# tests/m4/test_estados.py
def test_rechazar_sin_motivo_da_error():
    """REQ-M4-004 · No se puede rechazar sin motivo."""
    pub = crear_publicacion(estado="en_revision")          # fixture
    with pytest.raises(MotivoObligatorio):
        rechazar(pub, moderador=moderador_de_prueba, motivo="")
```
Las reglas son tres:
- El nombre dice qué prueba.
- El docstring cita el REQ.
- Prueba **una sola cosa**.

## Las etapas de una publicación (lo vas a usar todo el tiempo)
```
borrador ──► enviada ──► T6 dice OK ─────────────────► publicada
                    └──► T6 dice "problema" ──► en revisión ──► el moderador aprueba ──► publicada
                                                           └──► el moderador rechaza (con motivo) ──► rechazada
```
**Quién puede moderar:** el moderador y el admin nivel 1. El admin nivel 2 **solo reporta**. Empresa, particular y talento **no entran al panel**.

## Tu orden
1. **VA2-01** → 2. **VA2-02** → 3. **VA2-03** (lo más urgente: revisar los tests del login de Facu) → 4. **VA2-04** → 5. **VA2-05** → 6. **VA2-07**, **VA2-08**, **VA2-09** y **VA2-10** → 7. **VA2-06** → 8. **VA2-12** → 9. **VA2-11** → 10. **VA2-13** → 11. **VA2-14** → 12. **VA2-15**.

## Tabla de tareas
| ID | Tarea | Ticket | Necesitás antes | Valida |
|---|---|---|---|---|
| VA2-01 | Comparar los casos de Facu con el contrato | GAMMA-DOC | Casos de Facu y contrato M1 | Sebas |
| VA2-02 | Práctica de pruebas (Cap. 23) | GAMMA-DOC | — | Facu |
| VA2-03 | Revisar los tests del M1 de Facu | en los PRs de Facu | Tests de Facu | Ivo |
| VA2-04 | Datos de prueba del M4 | GAMMA-M4-014 | Fixtures de Facu | Facu |
| VA2-05 | Aceptar los casos de prueba del M4 | GAMMA-DOC | Casos de Thiago | Sebas |
| VA2-06 | Pruebas para el historial (T58) | GAMMA-M4-009 | Saber cómo es T58 | DevSecOps |
| VA2-07 | Tests en rojo: etapas de la publicación | GAMMA-M4-005 | Contrato M4 + VA2-05 | Facu |
| VA2-08 | Tests en rojo: quién puede hacer qué | GAMMA-M4-006 | Matriz de permisos | Facu |
| VA2-09 | Tests en rojo: panel y métricas | GAMMA-M4-007 | Modelo de datos M4 | Facu |
| VA2-10 | Tests del moderador automático (T6) | GAMMA-M4-008 | Simulado de T6 (Nico) | Nico |
| VA2-11 | Tests de que todo funciona junto | GAMMA-M4-015 | Simulados de alfa y beta | Nico |
| VA2-12 | Correr tus tests contra el código de Sebas | en los PRs | Código del M4 | Facu |
| VA2-13 | Recorrido completo de moderación | GAMMA-M4-013 | VA2-12 | Sebas |
| VA2-14 | Pedirle a la IA que encuentre huecos | GAMMA-DOC | VA2-07 a VA2-10 | Facu |
| VA2-15 | Prueba final e informe del M4 | GAMMA-DOC | M4 desplegado en test | Thiago |

---

### VA2-01 · Comparar los casos de Facu con el contrato
**Qué es:** Facu escribió casos del login ("dado… cuando… entonces…"). Vos controlás que digan lo mismo que el contrato de Sebas.
**Pasos:**
1. Abrí la sección 5 del contrato del M1 (la tabla de casos).
2. Por cada caso de Facu, buscá su fila en el contrato.
3. Si algo no coincide (por ejemplo, Facu dice que da error y el contrato dice que devuelve vacío), anotalo.
**Terminaste cuando:** dejaste un comentario con la lista de diferencias, o con "todo coincide". **Avisás a:** Sebas. Si ya lo hiciste con el kit, marcalo *Hecho*.

### VA2-02 · Práctica de pruebas
**Qué es:** leer el Cap. 23 y hacer los ejercicios de los niveles 1 y 2. Es práctica para que entiendas `pytest`, no es parte del producto.
**Terminaste cuando:** tenés los ejercicios hechos. **Avisás a:** Facu.

### VA2-03 · Revisar los tests de Facu ⚠️ urgente
**Qué es:** sos el segundo par de ojos de Facu. Sin tu OK, sus tests no se usan.
**Pasos:** por cada test de Facu (empezá por los del login), respondé:
1. ¿Prueba lo que dice la ficha?
2. ¿Falla **por la razón correcta**? (Que falle porque la función no existe está bien. Que falle porque el test tiene un error, no.)
3. ¿Podría pasar aunque el código esté mal? (Por ejemplo, un test que no comprueba nada siempre pasa.)
4. ¿Cita su REQ?
**Terminaste cuando:** aprobaste el PR de Facu o le dejaste comentarios concretos. **Avisás a:** Facu e Ivo.

### VA2-04 · Datos de prueba del M4
**Qué es:** preparar los datos de mentira que usan todos tus tests.
**Pasos:** en `tests/conftest.py`, sumá a lo que ya hizo Facu:
- Una publicación en cada etapa: borrador, enviada, en revisión, publicada y rechazada.
- Usuarios: un moderador, un admin nivel 1, un admin nivel 2, una empresa y un talento.
- Un reporte de ejemplo.
**Ojo:** no rompas los datos de Facu. Corré `pytest` entero antes de subir.
**Terminaste cuando:** los tests de Facu siguen funcionando y tus datos existen. **Avisás a:** Facu.

### VA2-05 · Aceptar los casos de prueba del M4
**Qué es:** Thiago te pasa casos en castellano (ANA-09). Vos decidís si te alcanzan para escribir los tests.
**Pasos:** leé cada caso y preguntate: "¿puedo escribir el test sin preguntarle nada a Thiago?". Si no, devolvé ese caso con lo que falta.
**Terminaste cuando:** todos los casos están aceptados. **Avisás a:** Thiago y Sebas.

### VA2-07 · Tests en rojo: etapas de la publicación
**Qué es:** un test por cada cambio de etapa del dibujo de arriba, los permitidos y los prohibidos.
**Tests que tenés que escribir (como mínimo):**
| # | Situación | Resultado esperado |
|---|---|---|
| 1 | Enviada + T6 dice OK | Pasa a publicada |
| 2 | Enviada + T6 dice problema | Pasa a en revisión |
| 3 | En revisión + el moderador aprueba | Pasa a publicada |
| 4 | En revisión + el moderador rechaza con motivo | Pasa a rechazada |
| 5 | En revisión + rechazar **sin** motivo | Error |
| 6 | Intentar publicar algo en revisión sin moderar | Error |
| 7 | Moderar algo ya publicado o rechazado | Error |
**Terminaste cuando:** los 7 tests existen y **todos fallan** porque el código no existe. **Avisás a:** Facu.

### VA2-08 · Tests en rojo: quién puede hacer qué
**Qué es:** comprobar que cada rol solo pueda hacer lo suyo.
**Tests que tenés que escribir (como mínimo):**
| Rol | Puede | No puede |
|---|---|---|
| Moderador | Aprobar y rechazar | Gestionar usuarios |
| Admin nivel 1 | Todo, incluido moderar | — |
| Admin nivel 2 | Reportar | Aprobar ni rechazar |
| Empresa / particular / talento | — | Entrar al panel |
Un test para cada "puede" y otro para cada "no puede".
**Terminaste cuando:** existen y fallan. **Avisás a:** Facu.

### VA2-09 · Tests en rojo: panel y métricas
**Qué es:** comprobar que el panel muestre los números correctos y solo a quien corresponde.
**Pasos:** con tus datos de VA2-04, escribí tests como "con 2 publicaciones en revisión, la métrica *en revisión* da 2", y "un talento que pide las métricas recibe *sin permiso*".
**Avisás a:** Facu.

### VA2-10 · Tests del moderador automático (T6)
**Qué es:** el M4 no hace la moderación automática; **recibe** el resultado de T6. Probás que lo reciba bien.
**Pasos:** usando el simulado de T6 de Nico:
1. Si T6 devuelve "OK", la publicación pasa.
2. Si T6 devuelve "problema: malas palabras", queda en revisión y el motivo se guarda.
3. Si T6 no responde, la publicación queda en revisión (mejor revisar de más que publicar algo malo).
Cuando DevSecOps entregue el T6 real, los mismos tests se corren contra él.
**Avisás a:** Nico.

### VA2-06 · Pruebas para el historial (T58)
**Qué es:** DevSecOps construye el historial; vos le pasás las pruebas que tiene que cumplir.
**Pasos:** escribí tests de que cada cambio de etapa guarda **quién, cuándo, qué y por qué**, de que nadie puede borrar ni editar el historial, y de que se puede restaurar una versión anterior con motivo. Primero preguntale a Nico cómo se usa T58.
**Avisás a:** DevSecOps (por medio de Nico o Sebas).

### VA2-12 · Correr tus tests contra el código
**Qué es:** cuando Sebas sube código del M4, corrés tus tests y reportás.
**Pasos:** en el PR de Sebas, comentá cuáles pasan y cuáles fallan, con el error. **Regla de oro:** si un test falla, se arregla el **código**, no el test. Si el test estaba mal, lo cambiás con el OK de Facu y lo dejás anotado.
**Avisás a:** Sebas y Facu.

### VA2-11 · Tests de que todo funciona junto
**Qué es:** comprobar que el M4 funciona con lo de los demás (o con sus simulados).
**Pasos:** probá que alfa y beta puedan usar `usuario_actual` y `tiene_rol`, y que el M4 pueda leer ofertas y búsquedas y darlas de baja. Anotá cuáles pruebas usan simulados, para correrlas otra vez cuando llegue el código real.
**Avisás a:** Nico.

### VA2-13 · Recorrido completo de moderación
**Qué es:** un solo test largo que cuenta la historia completa.
**Pasos:** una empresa envía una oferta → T6 dice problema → queda en revisión → el moderador la rechaza con motivo → queda en el historial. Y un segundo recorrido donde la oferta se publica.
**Avisás a:** Sebas.

### VA2-14 · Pedirle a la IA que encuentre huecos
**Qué es:** le pasás tus tests a Cursor y le preguntás "¿qué caso no estoy probando?". Vos decidís qué sugerencias tomar.
**Pasos:** anotá en el repo privado qué te sugirió y qué aceptaste o descartaste, con el motivo.
**Avisás a:** Facu.

### VA2-15 · Prueba final e informe del M4
**Qué es:** con el M4 en el ambiente de test, probás que lo básico funcione y escribís un resumen.
**Pasos:** `docs/gamma/informe-pruebas-m4.md` con qué se probó, qué pasó y qué quedó pendiente. Ese informe va a la documentación final.
**Avisás a:** Thiago y Vicente.
