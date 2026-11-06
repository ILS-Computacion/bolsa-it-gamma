# Flujo general de gamma · De cero a M1 y M4 andando

> Para los 7. Muestra **en qué orden pasan las cosas, quién mueve cada paso y con qué herramienta**. El detalle de cada paso está en las tarjetas de su archivo de rol (`gamma-01` a `gamma-07`).

## Herramientas: quién usa qué

| Quién | Herramienta de IA | Para qué |
|---|---|---|
| **Sebas (líder)** | **Claude Teams + Claude Code** | Contratos, revisión de fichas y **generación del código** a partir de fichas aprobadas |
| Ivo, Thiago, Facu, Agustín, Vicente, Nico | **Cursor (versión gratuita)** | Escribir tests, fichas, bocetos y configuración; revisiones asistidas. Cursor **no genera el código del producto**: eso pasa por Sebas |
| Todos | GitHub (repo, issues y Project), Bitwarden | Código, documentación en `docs/gamma/`, tarjetas y credenciales. **Nextcloud quedó descartado** |

> Si Sebas se satura, Ivo o Nico pueden generar lotes chicos con Cursor, **siempre con otra persona revisando**.

## El flujo en una línea

```
Pedidos a Hugo/DevSecOps → Esqueleto Reflex de gamma → Diseño (contrato, casos, modelo, pantallas)
→ Fichas aprobadas → Tests en ROJO → Código generado → Tests en VERDE → Revisión (Ivo y luego alfa)
→ Versión etiquetada → Integración → Despliegue en test → P5 DevSecOps → Documentación → Entrega
```

## Paso a paso

### Paso 0 · Preparación (lo que nos tienen que dar)
| Qué | Quién lo da | Quién lo pide |
|---|---|---|
| Repos `bolsa-it-gamma` y `bolsa-it-gamma-privado` | DevSecOps / Hugo | Sebas |
| GitHub Project de gamma (o permiso para crearlo) | DevSecOps / Hugo | Sebas |
| Proyecto Supabase de la organización (**llega el martes 3/11**) | DevSecOps / Hugo | Sebas |
| App de test en Reflex Cloud | DevSecOps | Nico |

Las credenciales se reparten en clase y se guardan en Bitwarden. **Nunca por chat ni en el repo.**

### Paso 1 · Esqueleto propio de gamma (tarjeta nueva: INT-00, Nico + Sebas)
No esperamos el esqueleto de Hugo. Creamos el nuestro:
1. `reflex init` dentro de `bolsa-it-gamma`, con la estructura de `guia-repos-e-integracion.md`.
2. Simulados de alfa y beta en `simulados/`, para no depender de ellos.
3. `pytest` configurado y un test de ejemplo en verde.
4. CI: tests y ticket-check en cada PR (`guia-ticket-check.md`).
5. Auth **simulada** hasta el 3/11; ese día se conecta Supabase Auth real (`guia-supabase-auth.md`).

**Listo cuando:** la app levanta en local con `reflex run` en las 7 máquinas.

### Paso 2 · Diseño (en paralelo)
| Quién | Hace | Archivo |
|---|---|---|
| Sebas | Contrato M1 (`usuario_actual`, `tiene_rol`, `UsuarioPublico`), matriz de permisos y contrato M4 | LID-04, LID-05, LID-13 |
| Thiago | Casos de uso, modelo de datos (pasa por la auditora) y fichas de lógica | ANA-01 a ANA-08 |
| Vicente | Pantallas, bocetos y fichas de interfaz | ANM-04 a ANM-06 |
| Ivo | Ficha P2 y revisión en el par del contrato | REV-03, REV-04 |
| Facu / Agustín | Casos de aceptación *dado / cuando / entonces* | VA1-01, VA2-01 |
| Nico | Datos ficticios y acuerdos de interfaces | INT-01, INT-07 |

### Paso 3 · El ciclo de cada ficha (se repite para cada pieza del M1 y del M4)

```
 Thiago/Vicente escriben la ficha (Cursor)
        │
        ▼
 Ivo la APRUEBA (P2) ──── devuelta ──► se corrige
        │
        ▼
 Thiago/Vicente escriben los casos de prueba
        │
        ▼
 Facu (M1) / Agustín (M4) escriben los TESTS EN ROJO (Cursor)  ◄── el otro validador los revisa
        │
        ▼
 Sebas genera el código con Claude Code hasta que los tests pasan a VERDE
        │
        ▼
 PR con título GAMMA-M1-NNN · ... → CI corre tests + ticket-check
        │
        ▼
 Ivo revisa el PR → revisor de alfa aprueba (P4)
        │
        ▼
 Nico lo une a main → la tarjeta pasa a Hecho
```

**Reglas del ciclo:**
- Sin ficha aprobada, no hay tests.
- Sin tests en rojo, no hay código.
- Si un test falla, se corrige el código o la ficha, **no el test**.

### Paso 4 · Versión e integración
Nico etiqueta una versión (`v0.1.0`, `v0.2.0`…) y la lleva al repo de integración (ver `guia-repos-e-integracion.md`). Mientras alfa y beta no tengan código, gamma se prueba contra los simulados.

### Paso 5 · Despliegue
Nico levanta la app en el ambiente de test de Reflex Cloud (`guia-reflex-cloud.md`). Ivo revisa el checklist y DevSecOps valida y pasa a producción (P5).

### Paso 6 · Aceptación y documentación
- Thiago prueba como usuario (aceptación).
- Facu y Agustín hacen la prueba de humo.
- Vicente documenta lo que realmente quedó, con registro continuo desde el día 1.

## Línea de tiempo

```
29/10     PoC: se entrega diseño + contrato + fichas P1 y P2 + tests en rojo (Supabase no existe todavía)
30/10-2/11 Esqueleto con Auth simulada + login en verde contra el simulado
3/11      Llega Supabase → se conecta, tests otra vez en verde → demo del PoC
3/11 →    M1 ciclo por ficha: login → registro → perfil → habilitación → baja
~5/11 →   M4 (su diseño ya arrancó con T61): cola "en revisión", panel, historial
~15/11    Integración con lo que tengan alfa y beta (o simulados) + correcciones de auditoría
19/11     M1 y M4 en test con P5  ✅
24/11     Documentación final · 27/11 presentación · 1/12 memoria
```

## Si te trabás
- **Te falta algo de otro rol:** escribí tu supuesto en la tarjeta, seguí y mencioná a la persona.
- **Te falta algo de afuera** (repo, Supabase, alfa, beta): la tarjeta pasa a *Bloqueado* con "Bloqueada: falta X (ID)" y avisás a Sebas.
- **Te sobra tiempo:** ayudá en la ruta crítica, que son los tests en rojo y las fichas.
