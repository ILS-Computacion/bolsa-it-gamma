# Casos de prueba de pantallas (dado / cuando / entonces)
## P11 · Iniciar sesión
1. Normal: dado un usuario habilitado, cuando ingresa correo y contraseña correctos, entonces llega a P01.
2. Raro: dado un correo sin @, cuando toca Ingresar, entonces ve "Ingresá un correo válido".
3. Sin permiso: dado un usuario no habilitado, cuando ingresa bien sus datos, entonces ve "Tu cuenta está pendiente de habilitación" y no entra.
4. Privacidad: dado un correo inexistente, cuando ingresa, entonces el mensaje es igual al de contraseña incorrecta.
## P10 · Registrarse
1. Normal: dados datos válidos, cuando crea la cuenta, entonces ve el aviso de pendiente de habilitación.
2. Raro: dada una descripción de más de 300 palabras, cuando envía, entonces ve el error de longitud.
3. Sin permiso: dado un usuario con sesión, cuando abre P10, entonces va a P01.
4. Campo privado: dado un teléfono marcado privado, cuando una empresa mira el perfil, entonces no lo ve.
## Mi perfil
1. Normal: el dueño edita su descripción y ve "Perfil actualizado".
2. Raro: borra un campo obligatorio y ve el error.
3. Sin permiso: un usuario intenta editar el perfil de otro y se le niega.
4. Campo privado: dado un perfil con teléfono privado, cuando lo mira una empresa, entonces no ve el teléfono.
## Habilitar cuentas
1. Normal: admin habilita una cuenta y ve "Cuenta habilitada".
2. Raro: no hay cuentas pendientes y se muestra lista vacía.
3. Sin permiso: un talento abre la URL y ve "No tenés permiso".
4. Privacidad: la lista no muestra campos privados ni contraseñas.
## P40 · Panel
1. Normal: el moderador ve los números del panel.
2. Raro: sin datos, los números muestran 0.
3. Sin permiso: una empresa abre P40 y se le niega.
4. Privacidad: el panel no muestra datos privados de autores.
## P42 · Cola de moderación
1. Normal: aprueba una publicación y sale de la cola.
2. Raro: rechaza sin motivo y ve "Escribí el motivo del rechazo".
3. Sin permiso: un particular abre P42 y se le niega.
4. Privacidad: la cola no muestra campos privados del autor.
## Historial y Reportes
1. Normal: tras rechazar con motivo, el historial muestra quién, qué y cuándo.
2. Raro: reporte sin motivo muestra el error.
3. Sin permiso: un moderador (no admin 2) no puede reportar.
4. Privacidad: el historial no expone datos privados.
