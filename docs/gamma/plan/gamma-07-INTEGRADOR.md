# Integrador · Nico · v1.3

## Tu trabajo en una frase
**Te ocupás de que el código tenga dónde vivir, que se pruebe solo y que encaje con el de los demás**: el repo, la app base, las pruebas automáticas, los "de mentira" de alfa y beta, y subir la app al ambiente de test.

Pensalo así: los demás fabrican las piezas y vos armás la máquina, controlás que cada pieza entre y la enchufás.

## Cómo leer este archivo
- Cada tarea tiene **qué es**, **pasos**, **terminaste cuando** y **a quién le avisás**.
- Hacé las tareas **en el orden de "Tu orden"**. INT-03, INT-00 e INT-05 frenan a todo el equipo: van primero.
- Al terminar: PR con el título del ticket, tarjeta a **En revisión** y aviso a quien valida.
- Si te trabás: tarjeta a **Bloqueado**, escribís `Bloqueada: falta X (ID)` y le avisás a Sebas.
- Guías que te sirven: `guia-repos-e-integracion.md`, `guia-ticket-check.md`, `guia-supabase-auth.md` y `guia-reflex-cloud.md`.

## Palabras que vas a ver mucho
| Palabra | Qué significa |
|---|---|
| **Repo** | La carpeta del proyecto en GitHub. Gamma tiene dos: `bolsa-it-gamma` (público, el código) y `bolsa-it-gamma-privado` (notas, prompts y borradores; nunca código) |
| **`main`** | La rama principal. Solo entra código revisado, nunca se sube directo |
| **PR** | Pull request: el pedido de "sumen mi cambio a `main`". Lo revisa otro |
| **CI** | GitHub Actions: cada vez que alguien abre un PR, corre los tests solo y avisa si algo falla |
| **Ticket-check** | Un control del CI que exige que el título del PR tenga el número de tarjeta (`GAMMA-M1-011 · …`) |
| **Simulado** | Una versión de mentira de algo que no existe todavía (alfa, beta, T6 o Supabase), con la misma forma que el real |
| **Interruptor** | Una variable que elige si se usa el simulado o el real: `GAMMA_SIMULADOS=1` usa los de mentira y `0` usa los reales |
| **Contrato** | Lo que un módulo promete a los otros: nombres de funciones, qué reciben y qué devuelven |
| **Ambiente de test** | La app subida a Reflex Cloud para probarla y mostrarla. La versión final (producción) la sube DevSecOps |

## Cómo está armado gamma (tu mapa)
```
bolsa-it-gamma/
├── gamma/m1/          ← código del M1 (lo genera Sebas)
├── gamma/m4/          ← código del M4
├── simulados/         ← LO TUYO: alfa, beta, T6 y Auth de mentira
├── app_gamma/         ← la app Reflex para probar lo nuestro
├── tests/             ← lo de Facu y Agustín
├── docs/gamma/        ← documentos
└── .github/workflows/ ← LO TUYO: el CI y el ticket-check
```
**La idea clave:** gamma **no espera** a alfa y beta. Mientras ellos no tengan código, usamos los simulados. Cuando lo tengan, cambiás el interruptor y listo.

## Tu orden
1. **INT-03** → 2. **INT-00** → 3. **INT-01** → 4. **INT-05** → 5. **INT-06** → 6. **INT-04** → 7. **INT-07** → 8. **INT-08** → 9. **INT-11** → después INT-02, INT-09, INT-10 (siempre), INT-12, INT-13, INT-14, INT-15 e INT-16.

## Tabla de tareas
| ID | Tarea | Ticket | Necesitás antes | Valida |
|---|---|---|---|---|
| INT-00 | App base de gamma con login de mentira | GAMMA-M1-024 | INT-03 | Sebas |
| INT-01 | Lista de usuarios de mentira | GAMMA-DOC | — | Auditora |
| INT-02 | Práctica de integración (Cap. 24) | GAMMA-DOC | — | Facu |
| INT-03 | Preparar los repos | GAMMA-M1-007 | Repos creados por Hugo/DevSecOps | DevSecOps |
| INT-04 | Proteger el repo privado | GAMMA-M1-023 | INT-03 | Ivo |
| INT-05 | Pruebas automáticas en cada PR | GAMMA-M1-008 | INT-00 | DevSecOps |
| INT-06 | Cargar las tarjetas en el tablero | GAMMA-DOC | INT-03 | Sebas |
| INT-07 | Acuerdos con alfa, beta y DevSecOps | GAMMA-DOC | Contrato M1 | Sebas |
| INT-08 | Simulados de alfa, beta y T6 | GAMMA-M4-016 | INT-07 | Agustín |
| INT-09 | Guía para usar el historial (T58) | GAMMA-DOC | T58 de DevSecOps | Sebas |
| INT-10 | Cuidar `main` (siempre) | — | — | Ivo |
| INT-11 | Login dentro del recorrido común | GAMMA-M1-012 | Login generado (LID-10) | Sebas |
| INT-12 | M1 completo con alfa y beta | GAMMA-M1-019 | M1 generado | Sebas |
| INT-13 | M4 completo con todos | GAMMA-M4-011 | M4 generado + INT-08 | Sebas |
| INT-14 | Subir el M1 al ambiente de test | GAMMA-M1-020 | INT-12 | DevSecOps |
| INT-15 | Subir el M4 al ambiente de test | GAMMA-M4-012 | INT-13 | DevSecOps |
| INT-16 | Ayudar con la guía de despliegue | GAMMA-DOC | README de Vicente | Vicente |

---

### INT-03 · Preparar los repos ⚠️ primero
**Qué es:** dejar los dos repos listos para que el equipo trabaje.
**Pasos:**
1. Confirmá que existen `bolsa-it-gamma` y `bolsa-it-gamma-privado` en ILS-Computación y que el team gamma tiene permiso de escritura. Si no existen, pedíselos a Sebas, que los tramita con Hugo. Probablemente se crean desde la plantilla `bolsa-it-practica`.
2. Clonalos en tu máquina.
3. Creá las **labels**: `modulo:m1`, `modulo:m4`, `tipo:doc`, `bloqueado`, `requiere-docente` y una `rol:` por rol (`rol:lider`, `rol:revisor`…).
4. Escribí la regla de nombres de ramas en `docs/gamma/README.md`: `gamma/M1-011-login`.
5. Confirmá que `main` del repo público está **protegido**: no se puede subir directo y hace falta un PR aprobado. Si no tenés permisos para eso, pedíselo a DevSecOps.
**Terminaste cuando:** los 7 pueden clonar, crear una rama y abrir un PR. **Avisás a:** Sebas y DevSecOps.

### INT-00 · App base con login de mentira ⚠️ frena a todos
**Qué es:** sin una app que arranque, nadie puede probar nada. La armás vos, sin esperar a nadie.
**Pasos:**
1. En `bolsa-it-gamma`, corré `reflex init` y armá las carpetas del mapa de arriba.
2. Creá `simulados/auth_simulada.py` con tres funciones que imitan a Supabase:
   - `iniciar_sesion(correo, contrasena)`: si coincide con un usuario de INT-01, devuelve un token.
   - `quien_es(token)`: devuelve el usuario.
   - `cerrar_sesion(token)`.
3. Agregá el interruptor `GAMMA_AUTH_SIMULADA=1`. Cuando esté Supabase, se carga el `.env` con las claves de Bitwarden (**nunca en el repo**), se pone el interruptor en `0` y se usa el Supabase real.
4. Configurá `pytest` y escribí un test que pase (por ejemplo, `assert 1 + 1 == 2`) para comprobar que funciona.
5. Escribí en el README cómo instalar y arrancar: `uv sync` y después `reflex run`.
**Terminaste cuando:** los 7 lograron correr `reflex run` y `pytest` en su máquina. **Avisás a:** todo el equipo, porque los destraba.

### INT-01 · Lista de usuarios de mentira
**Qué es:** los usuarios que se usan en todas las pruebas.
**Pasos:** armá una tabla con al menos: una empresa, un particular, un talento activo, un talento sin habilitar, un talento dado de baja, un moderador, un admin nivel 1 y un admin nivel 2. Solo correos `test-…@ejemplo.com`, **sin contraseñas escritas** en el documento.
**Terminaste cuando:** está en `docs/gamma/datos-ficticios.md` y lo vio la auditora. **Avisás a:** la auditora, Facu y Agustín.

### INT-05 · Pruebas automáticas en cada PR ⚠️ frena a los validadores
**Qué es:** que GitHub corra los tests solo, cada vez que alguien abre un PR.
**Pasos:**
1. Creá `.github/workflows/tests.yml`, que instala el proyecto y corre `pytest`.
2. Creá `.github/workflows/ticket-check.yml` copiando el de `guia-ticket-check.md`, pero con esta regex, que también acepta los tickets de documentación: `^GAMMA-(M1|M4|DOC)-[0-9]{3} · `.
3. Abrí un PR de prueba con un título mal escrito y comprobá que el check falle. Después corregí el título y comprobá que pase.
4. Pedile a quien administre el repo que marque los dos checks como **obligatorios** para unir a `main`.
**Terminaste cuando:** un PR sin tests en verde o sin el ticket en el título no se puede unir. **Avisás a:** Facu, Agustín y DevSecOps.

### INT-06 · Cargar las tarjetas en el tablero
**Qué es:** pasar las tarjetas de los 7 archivos al GitHub Project, junto con Sebas.
**Pasos:** un issue por tarjeta con el título del ticket, quién la hace (assignee), labels y la columna *Por hacer*. Copiá en el issue el "Terminaste cuando" de la tarjeta.
**Avisás a:** Sebas.

### INT-04 · Proteger el repo privado
**Qué es:** el repo privado no tiene las protecciones de GitHub del público, así que le ponés una simple.
**Pasos:** un *hook* local (`pre-push`) que no deje subir directo a `main`, y un texto corto de "cómo deshacer un error" (`git revert`). Probalo una vez.
**Avisás a:** Ivo.

### INT-07 · Acuerdos con alfa, beta y DevSecOps
**Qué es:** dejar por escrito qué le damos a los otros equipos y qué necesitamos de ellos, para que nadie cambie nombres sin avisar.
**Pasos:** en `docs/gamma/acuerdos-interfaces.md`, escribí:
1. **Lo que damos (M1):** `usuario_actual`, `tiene_rol`, `UsuarioPublico` y `obtener_usuario_publico`.
2. **Lo que necesitamos de alfa y beta:** listar las publicaciones en revisión, dar de baja y restaurar. La lista exacta te la pasa Thiago (ANA-04).
3. **Lo que necesitamos de DevSecOps:** el resultado de T6, el historial T58 y Supabase.
4. Hacé que un líder de alfa y uno de beta escriban "de acuerdo" en el PR.
**Si alfa o beta todavía no tienen contrato:** lo proponés vos con nombres y tipos, y se lo pasás.
**Avisás a:** Sebas.

### INT-08 · Simulados de alfa, beta y T6
**Qué es:** versiones de mentira para que el M4 se pueda programar y probar **sin esperar** a nadie.
**Pasos:**
1. `simulados/m2_ofertas.py` y `simulados/m3_busquedas.py`: las mismas funciones que acordaste en INT-07, devolviendo publicaciones de ejemplo.
2. `simulados/t6_moderador.py`: recibe un texto y devuelve "OK" o "problema: motivo". Por ejemplo, si el texto contiene una palabra de una lista corta de malas palabras, devuelve "problema".
3. El interruptor `GAMMA_SIMULADOS` elige simulado o real (el código de ejemplo está en `guia-repos-e-integracion.md`).
4. Marcá cada archivo con un comentario arriba: `# SIMULADO: reemplazar cuando exista el real`.
**Terminaste cuando:** Agustín puede escribir sus tests del M4 usando estos simulados. **Avisás a:** Agustín.

### INT-11 · Login dentro del recorrido común
**Qué es:** cuando Sebas termina el login, lo integrás al recorrido de la demo: "una empresa publica una oferta y un talento la encuentra".
**Pasos:** uní el PR aprobado a `main`, creá la etiqueta `v0.1.0` (`git tag v0.1.0` y después `git push --tags`) y comprobá que el login funcione dentro del recorrido, usando los simulados donde falte alfa o beta.
**Avisás a:** Sebas.

### INT-10 · Cuidar `main` (todo el proyecto)
**Qué es:** sos el que une los PRs.
**Reglas:** solo unís PRs con los checks en verde y aprobados por quien corresponde. Si dos PRs chocan, lo resolvés con sus autores. Si algo rompe `main`, avisás enseguida.

### INT-02 · Práctica de integración
**Qué es:** Cap. 24 (contratos, simulados e integración continua), niveles 1 y 2. Es práctica.
**Avisás a:** Facu.

### INT-09 · Guía para usar el historial (T58)
**Qué es:** cuando DevSecOps entregue T58, escribís una guía corta de cómo se usa desde M1 y M4, con un ejemplo que funcione.
**Avisás a:** Sebas y Agustín.

### INT-12 e INT-13 · Juntar con alfa y beta
**Qué es:** cuando alfa y beta tengan código real, cambiás el simulado por el real.
**Pasos:**
1. Poné el interruptor en `0`.
2. Corré todos los tests.
3. Si algo falla porque ellos hicieron algo distinto de lo acordado, lo resolvés con su integrador.
4. Para el M4, probá que una oferta de alfa y una búsqueda de beta recorran todo el flujo de moderación.
**Avisás a:** Sebas.

### INT-14 e INT-15 · Subir al ambiente de test ⚠️ antes del 19/11
**Qué es:** poner la app en internet, en el ambiente de test de Reflex Cloud.
**Pasos:**
1. Pedile a DevSecOps acceso a la app de test.
2. Cargá las variables (claves de Supabase) **en el panel de Reflex Cloud**, nunca en el repo.
3. Corré `reflex deploy`.
4. Comprobá que se pueda iniciar sesión con un usuario de mentira.
5. Ivo revisa la lista de despliegue y después le pedís a DevSecOps la **P5**: él sube a producción.
**Terminaste cuando:** el M1 (INT-14) y el M4 (INT-15) andan en test y DevSecOps dio la P5. **Avisás a:** Sebas y DevSecOps.

### INT-16 · Ayudar con la guía de despliegue
**Qué es:** comprobar con Vicente que la guía coincida con lo que hiciste de verdad, y estar en el ensayo.
**Avisás a:** Vicente.
