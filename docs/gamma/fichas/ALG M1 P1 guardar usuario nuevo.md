Ficha ALG-M1-P1 · Guardar un usuario nuevo

Tipo: persistencia (B13) · Módulo: M1 · Autor: Sebas · Fecha: 14/11/2026 Ticket: GAMMA-M1-005 · LID-07 · Ficha ALG-M1-P1 · Guardar un usuario nuevo Valida: Ivo (revisión en el par con P2) → revisor de alfa (C2) → auditora (C3) · Puerta: P2 Se apoya en: contrato del M1 v1.0, matriz de permisos v1.0 (M1-07, M1-12), ADR 0004. Ubicación: docs/gamma/fichas/ALG-M1-P1-guardar-usuario-nuevo.md

1. Qué hace

Guarda en el sistema una cuenta nueva que llega desde el registro (P10): crea la identidad en Supabase Auth y sus datos propios en el M1 (usuario, rol inicial y perfil vacío). O se guarda todo, o no se guarda nada.

2. Entrada
Dato	Tipo	Regla
correo	texto	Formato de correo válido. Se normaliza: sin espacios al principio y al final, todo en minúsculas
contrasena	texto	Mínimo 8 caracteres. Se pasa directo a Supabase Auth; el M1 no la guarda ni la registra en ningún log
nombre_visible	texto	2 a 60 caracteres, sin espacios al principio ni al final
tipo	TipoCuenta	Solo talento, empresa o particular

Nadie puede registrarse con rol moderador, admin_n1 ni admin_n2: esos roles los asigna el admin nivel 1 después (matriz M1-08).

3. Salida
Éxito: el UsuarioPublico recién creado (contrato M1, §3).
Error: DatosInvalidos (con qué campo falló) o RegistroNoDisponible (mensaje genérico, ver paso 4).
4. Pasos
Normalizar el correo: quitar espacios y pasar a minúsculas.
Validar los cuatro datos de la entrada. Si alguno falla → DatosInvalidos, sin tocar nada.
Crear la identidad en Supabase Auth con el correo normalizado y la contraseña. Supabase guarda la contraseña cifrada.
Si Supabase responde que el correo ya existe → RegistroNoDisponible con el mensaje genérico "No pudimos completar el registro. Si ya tenés una cuenta, iniciá sesión." El mensaje es el mismo que para cualquier otro error de Supabase: no revela que el correo existe.
En una sola transacción de la base, guardar:
una fila en usuarios: id (el de Supabase), nombre_visible, tipo, correo_normalizado, habilitado, creado_en, eliminado_en = null;
una fila en usuario_roles con el rol igual al tipo (talento, empresa o particular);
una fila en perfiles, vacía, con todos los campos opcionales en privado por defecto.
habilitado vale False si el tipo es talento (lo habilita un admin, matriz M1-07 y M1-12) y True para empresa y particular.
Si la transacción del paso 5 falla → se borra la identidad creada en el paso 3 (compensación) y se devuelve RegistroNoDisponible. Así no queda una cuenta de Supabase sin usuario del M1.
Devolver el UsuarioPublico.
5. Casos de ejemplo
#	Entrada	Resultado esperado
P1-01	Ana@Ejemplo.com , contraseña válida, "Ana", talento	Se crea con correo_normalizado = ana@ejemplo.com, rol talento, habilitado = False
P1-02	test-empresa@ejemplo.com, válida, "Acme SA", empresa	Se crea con rol empresa, habilitado = True
P1-03	test-ana@ejemplo.com cuando ya existe TEST-ANA@ejemplo.com	RegistroNoDisponible con el mensaje genérico; no se crea nada
P1-04	Correo ana@ (sin dominio)	DatosInvalidos (correo); no se llama a Supabase
P1-05	Contraseña de 5 caracteres	DatosInvalidos (contraseña); no se llama a Supabase
P1-06	tipo = "moderador"	DatosInvalidos (tipo); no se crea nada
P1-07	Datos válidos, pero falla el guardado en perfiles	Se borra la identidad de Supabase; no queda fila en usuarios ni usuario_roles; RegistroNoDisponible
P1-08	Cualquier registro exitoso	La contraseña no aparece en ninguna tabla del M1 ni en los logs
P1-09	Cualquier registro exitoso	El UsuarioPublico devuelto no contiene el correo
6. Datos que no usa
Nunca se pide ni se guarda: edad, fecha de nacimiento, género, origen, nacionalidad, domicilio, teléfono, documento.
La contraseña no se guarda en el M1 (solo en Supabase Auth, cifrada).
No se pide el currículum ni datos del perfil en el registro: se completan después, de forma opcional.
7. Eficiencia
Índice único sobre usuarios.correo_normalizado: evita duplicados aunque falle el control de Supabase, y hace la búsqueda por correo inmediata.
Índice sobre usuarios.eliminado_en para filtrar rápido las cuentas activas.
Una sola llamada a Supabase Auth y una sola transacción en la base por registro.
8. Riesgos para la auditoría
#	Riesgo	Cómo se cubre
R1	Enumeración de cuentas: saber si un correo está registrado	Mensaje genérico igual para todos los errores (paso 4, P1-03)
R2	Contraseña expuesta en logs o tablas	Pasa directo a Supabase; prohibido registrarla (P1-08)
R3	Cuenta a medias (en Supabase pero no en el M1)	Transacción + compensación (paso 7, P1-07)
R4	Autoasignarse un rol privilegiado	El tipo solo admite los 3 roles básicos (P1-06)
R5	Datos personales innecesarios	Solo 4 datos de entrada; ninguno de la lista prohibida (§6)
R6	Sesgo en la habilitación	La habilitación la decide una persona con los mismos datos para todos; esta ficha no filtra ni ordena por ningún dato personal
R7	Correo duplicado con distinta mayúscula	Normalización + índice único (P1-03, §7)
9. Supuestos
#	Supuesto	A confirmar con
S1	Empresa y particular quedan habilitados al registrarse; solo el talento espera al admin	Hugo
S2	Contraseña de mínimo 8 caracteres	DevSecOps
S3	El correo se guarda también en usuarios.correo_normalizado (además de Supabase) para el índice único y la búsqueda del admin; nunca sale del M1	Auditora [Privacidad]
