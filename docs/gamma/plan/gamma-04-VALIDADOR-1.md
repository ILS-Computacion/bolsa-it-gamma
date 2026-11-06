# Validador 1 · Facu · v1.3

## Tu trabajo en una frase
**Escribís las pruebas automáticas del M1 (login, registro, perfil y permisos) antes de que exista el código.** Sebas no puede generar nada hasta que tus pruebas existen y fallan.

Pensalo así: vos armás el examen antes de que la IA estudie. Sebas genera código hasta que la IA "aprueba" tu examen. Si el examen es flojo, aprueba con código malo. **Vos marcás el ritmo del equipo.**

## Cómo leer este archivo
- Cada tarea tiene **qué es**, **pasos**, **terminaste cuando** y **a quién le avisás**.
- Hacé las tareas **en el orden de "Tu orden"**.
- Al terminar: PR con el título del ticket, tarjeta a **En revisión** y aviso a quien valida (casi siempre Agustín: ustedes dos se revisan entre sí).
- Si te trabás: tarjeta a **Bloqueado**, escribís `Bloqueada: falta X (ID)` y le avisás a Sebas.

## Palabras que vas a ver mucho
| Palabra | Qué significa |
|---|---|
| **Test / prueba** | Un pedacito de código que usa una función y comprueba que el resultado sea el esperado |
| **pytest** | La herramienta con la que escribimos y corremos los tests (`pytest` en la terminal) |
| **Test en rojo** | Un test que falla. Al principio **tiene** que fallar, porque el código todavía no existe |
| **Rojo → verde** | Sebas genera código hasta que tus tests pasan |
| **Fixture** | Datos de mentira que se preparan antes de cada test (un talento, una empresa, un admin…) |
| **Contrato** | Lo que el M1 promete: `usuario_actual`, `tiene_rol` y las demás funciones. Tus tests salen de ahí |
| **Ficha** | La descripción exacta de cada función, con ejemplos. La otra fuente de tus tests |
| **REQ** | El número del requisito. Cada test lo cita, para saber qué requisito prueba |
| **RLS** | Reglas dentro de la base de datos que impiden leer datos ajenos |
| **Auth simulada** | Un login de mentira que armó Nico, para trabajar hasta que esté Supabase |
| **Dado / cuando / entonces** | Forma de escribir un caso: *dado* un usuario dado de baja, *cuando* inicia sesión, *entonces* no entra |

## Cómo se ve un test
```python
# tests/m1/test_login.py
def test_contrasena_incorrecta_no_dice_que_fallo():
    """REQ-M1-001 · El mensaje no revela si el correo existe."""
    resultado = iniciar_sesion("test-talento1@ejemplo.com", "mal")
    assert resultado.error == "Correo o contraseña incorrectos"
```
Las reglas son tres:
- El nombre dice qué prueba.
- El docstring cita el REQ.
- Prueba **una sola cosa**.

## Tu orden
1. **VA1-01** → 2. **VA1-02** → 3. **VA1-03** → 4. **VA1-04** → 5. **VA1-05** (⚠️ el más importante) → 6. **VA1-12** → 7. **VA1-06** → 8. **VA1-07**, **VA1-08** y **VA1-09** → 9. **VA1-10** (cada vez que Sebas sube código) → 10. **VA1-11** → 11. **VA1-13** → 12. **VA1-14**.

## Tabla de tareas
| ID | Tarea | Ticket | Necesitás antes | Valida |
|---|---|---|---|---|
| VA1-01 | Casos del login en castellano | GAMMA-DOC | — | Agustín |
| VA1-02 | Práctica de pruebas (Cap. 23) | GAMMA-DOC | — | Agustín |
| VA1-03 | Cómo vamos a probar (estrategia) | GAMMA-DOC | VA1-02 | Ivo |
| VA1-04 | Preparar el entorno y los datos de prueba | GAMMA-M1-009 | App base (INT-00) + usuarios de mentira (INT-01) | Nico |
| VA1-05 | Tests en rojo del login | GAMMA-M1-010 | Contrato M1 + VA1-04 | Agustín |
| VA1-06 | Aceptar los casos de Thiago | GAMMA-DOC | Casos de Thiago (ANA-09) | Sebas |
| VA1-07 | Tests en rojo: registro, habilitación y contraseña | GAMMA-M1-015 | Fichas de Thiago + VA1-06 | Agustín |
| VA1-08 | Tests en rojo: perfil y privacidad | GAMMA-M1-016 | Modelo de datos (ANA-03) | Agustín |
| VA1-09 | Tests en rojo: permisos | GAMMA-M1-017 | Matriz de permisos (LID-05) | Ivo |
| VA1-10 | Correr tus tests contra el código de Sebas | en los PRs | Código de Sebas | Agustín |
| VA1-11 | Pedirle a la IA que encuentre huecos | GAMMA-DOC | VA1-05 a VA1-09 | Agustín |
| VA1-12 | Recorrido del login para la demo | GAMMA-M1-021 | Login generado (LID-10) | Sebas |
| VA1-13 | Volver a probar después de la auditoría | en los PRs | Correcciones (LID-15) | Auditora |
| VA1-14 | Prueba final e informe del M1 | GAMMA-DOC | M1 desplegado en test | Thiago |

---

### VA1-01 · Casos del login en castellano
**Qué es:** antes de escribir código de test, escribís en palabras qué hay que probar del login.
**Pasos:** 5 casos *dado / cuando / entonces*, con correos `test-…@ejemplo.com`:
1. **Normal:** usuario habilitado con datos correctos → entra.
2. **Borde:** correo con mayúsculas (`Test-Talento1@…`) → entra igual.
3. **Borde:** cuenta sin habilitar → no entra.
4. **Error:** contraseña incorrecta → "Correo o contraseña incorrectos".
5. **Error:** cuenta dada de baja → el mismo mensaje.
**Terminaste cuando:** están en `docs/gamma/casos-login.md`. Si ya lo hiciste con el kit, marcalo *Hecho*. **Avisás a:** Agustín.

### VA1-02 · Práctica de pruebas
**Qué es:** leer el Cap. 23 (Classroom) y hacer los ejercicios de los niveles 1 y 2. Es práctica para entender `pytest`; no es parte del producto.
**Avisás a:** Agustín.

### VA1-03 · Cómo vamos a probar
**Qué es:** una página corta con las reglas de los tests, para que vos y Agustín escriban igual.
**Pasos:** en `docs/gamma/estrategia-pruebas.md`, escribí:
1. Herramienta: `pytest`.
2. Carpetas: `tests/m1/` y `tests/m4/`.
3. Tipos de test:
   - De una función sola.
   - De contrato: lo que prometemos a otros.
   - De permisos: quién puede qué.
   - De punta a punta: un recorrido completo.
4. Cada test cita su REQ en el docstring.
5. **Regla de oro:** un test nunca se cambia para que pase, salvo con el OK de otra persona.
**Avisás a:** Ivo.

### VA1-04 · Preparar el entorno y los datos de prueba
**Qué es:** que cualquiera corra `pytest` y tenga los datos de prueba listos.
**Pasos:**
1. Cuando Nico tenga la app base (INT-00), cloná el repo y corré `pytest`. Tiene que pasar su test de ejemplo.
2. En `tests/conftest.py`, creá un fixture por rol, con los usuarios de mentira de Nico (INT-01): talento, empresa, particular, moderador, admin nivel 1 y admin nivel 2. Sumá también un talento sin habilitar y uno dado de baja.
3. Nada de contraseñas reales ni claves en el código.
**Terminaste cuando:** `pytest` corre en tu máquina y en GitHub (el CI de Nico). **Avisás a:** Nico y Agustín.

### VA1-05 · Tests en rojo del login ⚠️ lo más importante
**Qué es:** los tests que Sebas necesita para generar el login. **Sin esto, el equipo no arranca.**
**Pasos:** a partir del contrato de Sebas, escribí en `tests/m1/test_login.py` y `tests/m1/test_usuario_actual.py`:
| Función | Tests mínimos |
|---|---|
| Iniciar sesión (P11) | Datos correctos; contraseña incorrecta (mismo mensaje que si el correo no existe); correo con mayúsculas |
| `usuario_actual` | Sesión válida devuelve el usuario; sesión vencida da `SesionInvalida`; sesión inventada da `SesionInvalida`; usuario dado de baja da error |
| `tiene_rol` | Un caso por fila de la tabla de la sección 5 del contrato |
**Terminaste cuando:** los tests existen, **todos fallan** porque el código no existe y cada uno cita su REQ. **Avisás a:** Agustín (que los revisa) y a Sebas (que espera esto para arrancar).

### VA1-12 · Recorrido del login para la demo
**Qué es:** un test largo que recorre el login como en la demo: entra un usuario, el sistema sabe quién es y qué rol tiene.
**Pasos:** cuando el login esté en verde, escribilo en `tests/m1/test_recorrido_login.py`. Si registro y perfil ya funcionan, sumalos.
**Avisás a:** Sebas.

### VA1-06 · Aceptar los casos de Thiago
**Qué es:** Thiago te pasa casos en castellano por cada ficha (ANA-09). Vos decidís si te alcanzan.
**Pasos:** por cada caso, preguntate: "¿puedo escribir el test sin preguntarle nada a Thiago?". Si no, devolvé ese caso diciendo qué falta.
**Avisás a:** Thiago y Sebas.

### VA1-07 · Tests en rojo: registro, habilitación y contraseña
**Tests mínimos:**
| Situación | Resultado esperado |
|---|---|
| Un talento se registra bien | Queda creado **sin habilitar** |
| Se registra con un correo que ya existe | Error que **no dice** que el correo existe |
| Manda un dato prohibido (edad, género…) | Se rechaza |
| El admin habilita una cuenta | Ahora puede entrar |
| Un talento intenta habilitar a otro | "Sin permiso" |
| El admin restablece una contraseña | La nueva funciona |
| Alguien que no es admin intenta restablecer | "Sin permiso" |
**Avisás a:** Agustín.

### VA1-08 · Tests en rojo: perfil y privacidad
**Tests mínimos:**
| Situación | Resultado esperado |
|---|---|
| Talento sin currículum | Puede usar el sistema igual |
| Edita su perfil | El cambio queda como borrador hasta que confirma |
| Campo público | Lo ve cualquiera |
| Campo "solo empresas" | Lo ve una empresa, pero no otro talento |
| Campo privado | Solo lo ve el dueño |
| Se da de baja | No aparece, pero sus datos no se borran |
| Categoría | Hoy es "IT", pero el sistema acepta otra |
**Avisás a:** Agustín.

### VA1-09 · Tests en rojo: permisos
**Qué es:** comprobar que la base de datos misma impida ver lo ajeno, no solo la pantalla.
**Pasos:** por cada fila de la matriz de permisos de Sebas, un test de "puede" y otro de "no puede". **Clave:** corré estos tests como usuario común, nunca como administrador, porque el administrador se saltea las reglas y el test pasaría siempre.
**Ejemplos:** una empresa no lee campos privados; un talento no lee el perfil privado de otro.
**Avisás a:** Ivo.

### VA1-10 · Correr tus tests contra el código
**Qué es:** cada vez que Sebas sube código del M1, corrés tus tests y le decís qué pasa.
**Pasos:** en su PR, comentá cuáles pasan y cuáles fallan, con el error.
**Regla de oro:** si un test falla, se arregla el **código** (o la ficha), no el test. Si el test estaba mal, lo cambiás con el OK de Agustín y lo dejás anotado.
**Avisás a:** Sebas.

### VA1-11 · Pedirle a la IA que encuentre huecos
**Qué es:** le pasás tus tests a Cursor y le preguntás "¿qué caso no estoy probando?" o "¿hay algún test que pasaría aunque el código esté mal?". Vos decidís qué sugerencias tomar.
**Pasos:** anotá en el repo privado qué te sugirió y qué aceptaste o descartaste, con el motivo.
**Avisás a:** Agustín.

### VA1-13 · Volver a probar después de la auditoría
**Qué es:** cuando se corrige algo que marcó la auditora, corrés todos los tests y agregás uno nuevo por cada problema corregido, para que no vuelva a pasar.
**Avisás a:** la auditora y Sebas.

### VA1-14 · Prueba final e informe del M1
**Qué es:** con el M1 en el ambiente de test, comprobás que lo básico funcione y escribís un resumen.
**Pasos:** `docs/gamma/informe-pruebas-m1.md` con qué se probó, qué pasó y qué quedó pendiente. Ese informe va a la documentación final.
**Avisás a:** Thiago y Vicente.
