# ADR 0004 · Autenticación con Supabase Auth

- **Estado:** Aceptada
- **Fecha de la decisión:** 15/10/2026 (T68)
- **Redactado:** 14/11/2026 · Sebas (líder de gamma)
- **Ticket:** `GAMMA-M1-003 · LID-06 · ADR 0004 (Supabase Auth)`
- **Valida:** Hugo
- **Ubicación:** `docs/adr/0004-autenticacion.md`

## Contexto

La Bolsa de Trabajo IT necesita que los usuarios (talentos, empresas, particulares, moderadores y administradores) inicien sesión de forma segura. El M1 (usuarios), a cargo de gamma, es el módulo del que dependen todos los demás para saber quién está logueado y qué rol tiene.

Había dos opciones (T68):

- **A · Autenticación propia:** programar nosotros el registro, el guardado de contraseñas, las sesiones y la recuperación de cuenta.
- **B · Supabase Auth:** usar el servicio de autenticación de Supabase, que ya es la base de datos del proyecto.

Restricciones:

- Equipo de alumnos, con poco tiempo (entrega final 24/11).
- Manejar contraseñas a mano es un riesgo de seguridad alto.
- El proyecto ya usa Supabase como base de datos, con reglas RLS.
- No se guardan datos personales innecesarios (nunca edad, género, origen ni domicilio).

## Decisión

Usamos **Supabase Auth (opción B)** para toda la autenticación.

## Alternativa descartada

**Autenticación propia (A).** Se descartó porque:

- Guardar contraseñas, manejar sesiones y recuperar cuentas de forma segura es difícil y fácil de hacer mal.
- Consumiría tiempo que hace falta para M1 y M4.
- Supabase Auth se integra directo con las reglas RLS de la base (`auth.uid()`), cosa que con una solución propia habría que construir.

## Consecuencias

### Qué delega el M1 a Supabase Auth

| Tema | Detalle |
|---|---|
| Contraseñas | Supabase las guarda cifradas; el M1 **nunca** las ve ni las guarda |
| Sesiones | Supabase emite y valida el token de acceso; ese token es el `sesion_id` del contrato M1 |
| Identidad | El id del usuario de Supabase es el `id` de `UsuarioPublico` |
| Restablecer contraseña | Lo ejecuta Supabase; en pruebas lo dispara el admin, porque los correos son ficticios |
| Unicidad del correo | Supabase no permite dos cuentas con el mismo correo |

### Qué sigue siendo nuestro (M1)

| Tema | Detalle |
|---|---|
| Roles | Los 6 roles y su asignación (`tiene_rol`), en tablas propias |
| Tipo de cuenta | Talento, empresa o particular, separado de los roles |
| Perfil | Datos del perfil con privacidad por campo (público, visible para empresas, privado) y currículum opcional |
| Habilitación | El talento se registra sin habilitar; lo habilita un admin |
| Baja | Lógica, con `eliminado_en`; al darse de baja, sus sesiones dejan de servir |
| Permisos | Reglas RLS según la matriz de permisos (LID-05) |
| Normalización | El correo se pasa a minúsculas antes de guardarlo |
| Mensajes | Los errores no revelan si un correo existe |

### Otras consecuencias

- **Positivas:** menos código propio y menos riesgo de seguridad; las reglas RLS usan directamente la identidad de Supabase.
- **Negativas:** dependemos de un servicio externo; los tests no pueden usar Supabase real en cada corrida.
- **Mitigación:** una **Auth simulada** (`GAMMA_AUTH_SIMULADA=1`) cumple el mismo contrato del M1 y se usa en todos los tests. Conectar Supabase real es cambiar ese interruptor.
- **Cambio de stack del 14/11 (Reflex → Flask + Render):** no afecta esta decisión. Flask valida el token de Supabase en cada pedido; el contrato del M1 no cambia.

## Referencias

- Contrato del M1 v1.0: `docs/gamma/contratos/contrato-m1.md`
- Matriz de permisos: `docs/gamma/matriz-permisos.md`
- MASTER v1.4, sección 3
