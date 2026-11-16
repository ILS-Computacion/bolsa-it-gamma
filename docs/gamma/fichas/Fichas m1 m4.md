Lista y reparto de fichas · M1 y M4

Ticket: GAMMA-DOC-NNN · LID-08 · Lista y reparto de fichas de M1 y M4 (label tipo:doc) Autor: Sebas · Fecha: 16/11/2026 · Valida: Ivo · Puerta: P1 Ubicación: docs/gamma/fichas/README.md Cada ficha va en docs/gamma/fichas/ y la aprueba Ivo (REV-06) antes de que se escriban sus tests.

Cómo se lee
Estado: Pendiente (sin empezar) · Redactada (PR abierto) · Aprobada (Ivo la aprobó) · Bloqueada.
Requisito: de dónde sale la ficha: función del contrato (F1…), fila de la matriz (M1-07…), regla del dominio (D-…) o requisito del producto (PRD-…).
Los autores actualizan su fila al abrir el PR y al aprobarse.
1. Persistencia (cómo se guarda y se lee de la base)
ID	Ficha	Autor	Estado	Requisito
ALG-M1-P1	Guardar un usuario nuevo	Sebas	Redactada	Contrato M1 §3; matriz M1-07; ADR 0004
ALG-M1-P2	[nombre según REV-03]	Ivo	[a completar]	Contrato M1 F1, F2
ALG-M1-P3	Actualizar el perfil	Thiago	Pendiente	Matriz M1-02; PRD-02 (privacidad por campo)
ALG-M1-P4	Dar de baja un usuario (baja lógica)	Thiago	Pendiente	Contrato M1 F4; matriz M1-05, M1-10
ALG-M4-P1	Guardar una decisión de moderación	Thiago	Pendiente	Matriz M4-01, M4-02; PRD-14
ALG-M4-P2	Guardar un reporte del nivel 2	Thiago	Pendiente	Matriz M4-06
2. Lógica (reglas y decisiones)
M1
ID	Ficha	Autor	Estado	Requisito
ALG-M1-L1	Obtener el usuario de la sesión	Thiago	Pendiente	Contrato M1 F1
ALG-M1-L2	Verificar un rol	Thiago	Pendiente	Contrato M1 F2; decisión 9.3
ALG-M1-L3	Obtener datos públicos de un usuario	Thiago	Pendiente	Contrato M1 F3; matriz M1-03
ALG-M1-L4	Habilitar un talento	Thiago	Pendiente	Matriz M1-07, M1-12
ALG-M1-L5	Asignar y quitar roles	Thiago	Pendiente	Matriz M1-08
ALG-M1-L6	Restablecer la contraseña (por el admin)	Thiago	Pendiente	Matriz M1-09; MASTER §11.1
ALG-M1-L7	Filtrar el perfil según quién lo mira	Thiago	Pendiente	Matriz M1-01, M1-03, M1-04; PRD-02
M4
ID	Ficha	Autor	Estado	Requisito
ALG-M4-L1	Cambiar el estado de una publicación (máquina de estados)	Thiago	Pendiente	Contrato M4 (LID-13); PRD-14
ALG-M4-L2	Recibir el resultado del moderador automático (T6)	Thiago	Pendiente	Contrato M4; matriz M4-09
ALG-M4-L3	Aprobar o rechazar con motivo	Thiago	Pendiente	Matriz M4-02, M4-03; supuesto S6 de la matriz
ALG-M4-L4	Calcular las métricas del panel	Thiago	Pendiente	Matriz M4-04, M4-05
ALG-M4-L5	Registrar un reporte del nivel 2	Thiago	Pendiente	Matriz M4-06, M4-07
3. Interfaz (pantallas)
ID	Pantalla	Autor	Estado	Requisito
ALG-M1-I-P00	Inicio	Vicente	Pendiente	Recorrido del PoC
ALG-M1-I-P01	Menú según el rol	Vicente	Pendiente	Contrato M1 F2
ALG-M1-I-P10	Registro	Vicente	Pendiente	ALG-M1-P1
ALG-M1-I-P11	Iniciar sesión	Vicente	Pendiente	Contrato M1 F1; ADR 0004
ALG-M1-I-PER	Perfil (ver y editar, con privacidad por campo)	Vicente	Pendiente	ALG-M1-P3, ALG-M1-L7; PRD-02, PRD-NF9
ALG-M4-I-P40	Panel con métricas	Vicente	Pendiente	ALG-M4-L4
ALG-M4-I-P42	Cola de moderación	Vicente	Pendiente	ALG-M4-L3
4. Resumen de carga
Autor	Fichas
Sebas	1
Ivo	1
Thiago	16
Vicente	7

Thiago queda con 16 fichas y es un cuello de botella. Propuesta: que Ivo o Nico tomen algunas de lógica del M1 (L5 y L6) si Thiago se atrasa.

5. Supuestos
#	Supuesto	A confirmar con
S1	P00 es la pantalla de inicio y P01 el menú según el rol	Vicente
S2	Las fichas de persistencia del M4 (ALG-M4-P1 y P2) son de Thiago, igual que las de lógica	Thiago
S3	El historial (T58) no lleva ficha de gamma: lo construye DevSecOps	DevSecOps
