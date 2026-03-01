# 📄 Planeación del Sistema – Bankify

## Desglose de trabajo: Épicas, Historias de Usuario y Tareas

La implementación de los requerimientos identificados de Bankify se desglosa de la siguiente manera:

---

### 1. Épica:

| Campo | Descripción |
|------|-------------|
| **ID** | EP-01 |
| **Título** | Gestión de cuentas bancarias |
| **Descripción** | Desarrollar el módulo que permita crear, activar, inactivar y actualizar cuentas bancarias, cumpliendo con las reglas de negocio definidas por Bankify (validación de número de cuenta, banco registrado, roles autorizados) y permitiendo a los clientes consultar su saldo y realizar depósitos de forma segura. |
| **Stakeholder** | Gerente de operaciones de Bankify, clientes finales y asesores bancarios. |

---

### 2. Historias de usuario:

| Campo | Descripción |
|------|-------------|
| **ID** | HU-01 |
| **Título** | Crear cuenta bancaria |
| **Descripción** | Como asesor, quiero crear una cuenta bancaria para un cliente validando el número de cuenta y el banco registrado, para garantizar que solo se registren cuentas válidas en el sistema. |
| **Prioridad** | Alta — Es la funcionalidad base del sistema; sin ella no es posible ninguna otra operación sobre cuentas. |
| **Estimación** | |

| Campo | Descripción |
|------|-------------|
| **ID** | HU-02 |
| **Título** | Activar e inactivar cuenta bancaria |
| **Descripción** | Como asesor o cliente, quiero activar o inactivar una cuenta bancaria, para tener control sobre el estado de las cuentas y restringir operaciones sobre cuentas no habilitadas. |
| **Prioridad** | Alta — El control de estado de las cuentas es un requisito de negocio crítico para la seguridad operativa. |
| **Estimación** | |

| Campo | Descripción |
|------|-------------|
| **ID** | HU-03 |
| **Título** | Consultar saldo de cuenta |
| **Descripción** | Como cliente, quiero consultar el saldo de mi cuenta bancaria en cualquier momento, para conocer mi disponibilidad financiera de forma rápida y segura. |
| **Prioridad** | Alta — Es una de las funcionalidades esenciales para validar el modelo de negocio en la primera versión del producto. |
| **Estimación** | |

| Campo | Descripción |
|------|-------------|
| **ID** | HU-04 |
| **Título** | Realizar depósito a una cuenta |
| **Descripción** | Como cliente propietario u otro usuario, quiero realizar un depósito a una cuenta bancaria a través de PSE, para incrementar el saldo disponible de forma segura y controlada. |
| **Prioridad** | Media — Depende de que las cuentas estén creadas y activas (HU-01, HU-02), y representa la primera operación transaccional del sistema. |
| **Estimación** | |

---

### 3. Tareas:

| Campo | Descripción |
|------|-------------|
| **ID** | TR-01 |
| **Título** | Diseñar modelo de datos de cuenta bancaria |
| **ID de la Historia de Uso asociada** | HU-01 |
| **Descripción** | Definir la entidad `CuentaBancaria` con sus atributos: número de cuenta (10 dígitos), banco (2 primeros dígitos), titular, saldo, estado y fecha de creación. |
| **Tareas requisito** | — |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-02 |
| **Título** | Implementar validaciones del número de cuenta |
| **ID de la Historia de Uso asociada** | HU-01 |
| **Descripción** | Desarrollar la lógica de negocio que valide que el número de cuenta tenga exactamente 10 dígitos, contenga solo números, no incluya caracteres especiales y que el banco indicado (primeros 2 dígitos) esté registrado en el sistema. |
| **Tareas requisito** | TR-01 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-03 |
| **Título** | Implementar endpoint REST para creación de cuenta |
| **ID de la Historia de Uso asociada** | HU-01 |
| **Descripción** | Crear el endpoint `POST /cuentas` que reciba los datos de la nueva cuenta, ejecute las validaciones y persista la cuenta en base de datos, retornando la respuesta con el ID generado. |
| **Tareas requisito** | TR-01, TR-02 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-04 |
| **Título** | Implementar lógica de cambio de estado de cuenta |
| **ID de la Historia de Uso asociada** | HU-02 |
| **Descripción** | Desarrollar el servicio que permita cambiar el estado de una cuenta (ACTIVA / INACTIVA), validando que el usuario tenga el rol autorizado (asesor para ambas acciones; cliente solo para inactivar). |
| **Tareas requisito** | TR-01 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-05 |
| **Título** | Implementar endpoint REST para activar/inactivar cuenta |
| **ID de la Historia de Uso asociada** | HU-02 |
| **Descripción** | Crear el endpoint `PATCH /cuentas/{id}/estado` que reciba el nuevo estado y aplique el cambio correspondiente según el rol del usuario autenticado. |
| **Tareas requisito** | TR-04 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-06 |
| **Título** | Agregar pruebas unitarias para cambio de estado |
| **ID de la Historia de Uso asociada** | HU-02 |
| **Descripción** | Escribir pruebas unitarias que validen los flujos de activación e inactivación, incluyendo los casos donde el rol no tiene permiso para la operación. |
| **Tareas requisito** | TR-04, TR-05 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-07 |
| **Título** | Implementar servicio de consulta de saldo |
| **ID de la Historia de Uso asociada** | HU-03 |
| **Descripción** | Desarrollar la lógica de negocio que recupere el saldo actualizado de una cuenta dado su número, verificando que el cliente autenticado sea el titular de la cuenta. |
| **Tareas requisito** | TR-01 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-08 |
| **Título** | Implementar endpoint REST para consulta de saldo |
| **ID de la Historia de Uso asociada** | HU-03 |
| **Descripción** | Crear el endpoint `GET /cuentas/{id}/saldo` que retorne el saldo actual de la cuenta junto con el nombre del titular y el número de cuenta. |
| **Tareas requisito** | TR-07 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-09 |
| **Título** | Agregar pruebas unitarias para consulta de saldo |
| **ID de la Historia de Uso asociada** | HU-03 |
| **Descripción** | Escribir pruebas unitarias que validen la consulta exitosa del saldo y los casos de error: cuenta inexistente, cuenta inactiva y acceso por usuario no titular. |
| **Tareas requisito** | TR-07, TR-08 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-10 |
| **Título** | Integrar pasarela de pago PSE |
| **ID de la Historia de Uso asociada** | HU-04 |
| **Descripción** | Configurar e integrar el cliente HTTP para comunicarse con la API de PSE, gestionando la creación de la transacción, la redirección del usuario y la confirmación del pago. |
| **Tareas requisito** | — |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-11 |
| **Título** | Implementar servicio de depósito a cuenta |
| **ID de la Historia de Uso asociada** | HU-04 |
| **Descripción** | Desarrollar la lógica que, tras confirmar el pago exitoso desde PSE, actualice el saldo de la cuenta destino y registre la transacción en el histórico de movimientos. |
| **Tareas requisito** | TR-01, TR-10 |

| Campo | Descripción |
|------|-------------|
| **ID** | TR-12 |
| **Título** | Implementar endpoint REST para depósito |
| **ID de la Historia de Uso asociada** | HU-04 |
| **Descripción** | Crear el endpoint `POST /cuentas/{id}/depositos` que inicie el flujo de depósito vía PSE, valide el monto (mayor a cero) y retorne la URL de redirección al usuario para completar el pago. |
| **Tareas requisito** | TR-10, TR-11 |



# video del planning poker 

historia de usuario 1 comprendida por las tareas de:
-crear la base de datos 
-implementar validaciones del numero de la cuenta
-implementar creacion de cuentas

https://teams.microsoft.com/l/meetingrecap?driveId=b%21-Mgoy6LOnU2lyoan7rg8taTgiuwSdJlOtGTnFUqAIE-up3tgmOB0RoUIFXvrMVZs&driveItemId=016HQMUJGHQM2PW7NQSBBYJQ3MSZLWXCYK&sitePath=https%3A%2F%2Fpruebacorreoescuelaingeduco-my.sharepoint.com%2F%3Av%3A%2Fg%2Fpersonal%2Fjuan_neira-z_mail_escuelaing_edu_co%2FIQDHgzT7fbCQQ4TDbJZXa4sKAaE2_y8gjcOZ_sLpNxCrIIY&fileUrl=https%3A%2F%2Fpruebacorreoescuelaingeduco-my.sharepoint.com%2F%3Av%3A%2Fg%2Fpersonal%2Fjuan_neira-z_mail_escuelaing_edu_co%2FIQDHgzT7fbCQQ4TDbJZXa4sKAaE2_y8gjcOZ_sLpNxCrIIY&threadId=19%3A10bc4f5609094d9b86c7da8ff85f9eef%40thread.v2&organizerId=ce1f903c-9c2c-4ee7-b716-c56b640bd94d&tenantId=50640584-2a40-4216-a84b-9b3ee0f3f6cf&callId=57e1e7e5-2887-4f56-9b9e-f5f36ef78c26&threadType=GroupChat&meetingType=Adhoc&subType=RecapSharingLink_RecapChiclet


5. En el archivo README.md contesten las siguientes preguntas:
a. ¿Cuál fue la mayor dificultad a la hora de estimar?

a la hora de estimar los puntos de historia de usuario es muy importante el tener diferentes perspectivas pues una persona puede pensar que una tarea es muy facil o muy complicado lo cual depende de persona a persona entonces estimar los puntos seria muy complpicado haciendolo solo y sin hablar para llegar a acuerdos

b. ¿Fue fácil llegar a un consenso?

si pues en nuestro grupo no se tienen personalidades que choquen entres si por o cual es facil llegar a ver las cosas con la perspectiva de los otros lo cual permite facimente llegar a consensos

c. ¿Cómo resolvieron los escenarios donde las estimaciones para la misma historia de usuario no fueron cercanas?

como se menciono en el punto anterior nuestro grupo tienen una buena comunicacion y comprension lo cual hace que podamos llegar a consensos facilmente cada quien exponiendo su razonaiento y sus opiniones donde despues de analizarlo se pudo llegar a solucionar las estimaciones incluso cuando se varia demasiado las estimaciones de cada persona
