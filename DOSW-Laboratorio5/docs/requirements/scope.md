# 📄 Requerimientos del Sistema

## 1. Sistema

* **Nombre del sistema:** Sistema de Gestión de Cuentas Bankify  

* **Objetivo:** El sistema tiene como objetivo centralizar la gestión básica de cuentas bancarias de Bankify, permitiendo la administración de clientes y cuentas, la consulta de saldos, la realización de depósitos y la generación de reportes tributarios, garantizando el cumplimiento de las reglas de negocio establecidas.

---

## 2. Problema a resolver

Actualmente, Bankify no cuenta con un sistema centralizado que permita registrar y validar cuentas bancarias conforme a reglas específicas del negocio, consultar saldos, realizar depósitos de manera controlada y generar reportes tributarios tanto para los clientes como para la DIAN.

La ausencia de este sistema dificulta la gestión organizada de la información, el control de operaciones básicas y el cumplimiento de obligaciones tributarias en formatos requeridos (PDF y JSON).

---

## 3. Diagrama de Contexto

### 3.1 Diagrama

![diagramaDeContexto](./../uml/bankify.png)

### 3.2 Actores

| Actor / Rol            | Descripción                                                                 |
|------------------------|:---------------------------------------------------------------------------:|
| Usuario final          | Cliente del sistema de Bankify                                             |
| Cliente                | Puede autenticarse, consultar saldo, realizar depósitos, generar reportes e inactivar su cuenta |
| Asesor                 | Gestiona cuentas bancarias: crear, activar, inactivar y actualizar cuentas |
| Supervisor             | Gestiona clientes: crear, activar, inactivar y actualizar información      |
| Gerente financiero     | Genera reportes tributarios consolidados y los envía a la DIAN            |

---         

### 3.3 Sistemas externos

| Sistema                | Descripción                                                                 |
|------------------------|:---------------------------------------------------------------------------:|
| Reportes               | Sistema que genera los reportes tributarios de cada cliente del sistema de Bankify |
| DIAN                   | Sistema externo que recibe el reporte tributario consolidado en formato JSON |
| Bancos Externos        | Sistema de entidades financieras externas que realizan operaciones con nuestro Banco |

---

## 4. Alcance del sistema
   
### 4.1 Dentro del sistema

Funciones que el sistema sí realiza:

- Autenticación mediante usuario y contraseña.
- Creación, activación, inactivación y actualización de clientes.
- Creación, activación, inactivación y actualización de cuentas bancarias.
- Validación de reglas de negocio para números de cuenta (10 dígitos, solo números, banco válido).
- Consulta de saldo por parte del cliente.
- Realización de depósitos.
- Generación de reporte tributario individual en formato PDF.
- Generación de reporte tributario consolidado en formato JSON para la DIAN.

---
### 4.2 Fuera del sistema

Funciones que no realiza:

- Transferencias entre cuentas.
- Integración con sistemas reales de otros bancos.
- Gestión de créditos o productos financieros avanzados.
- Pagos electrónicos o pasarelas de pago.
- Desarrollo de aplicación móvil.