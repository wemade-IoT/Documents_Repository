# Service Design and Planning Bounded Context

## 1. Descripción General

Este bounded context gestiona la entidad Order, encargada de la planificación y diseño de servicios solicitados por los usuarios. La entidad Order ha sido extraída del contexto de Subscriptions and Payments para centralizar la lógica de planeamiento y diseño de servicios.

## 2. Implementación de las interfaces de los Repositories

| Clase            | Interfaz Implementada | Descripción                                                                 |
|------------------|----------------------|-----------------------------------------------------------------------------|
| OrderRepository  | IOrderRepository     | Implementa los métodos de consulta y persistencia de las órdenes de servicio.|

## 3. Bounded Context Software Architecture Component Level Diagrams

Web App:

<img src="../component-diagrams/structurizr-101372-ServiceDesignPlanningWebApp.png" alt="Service Design Planning Component Diagram on Web App" width="350"/>

Backend:

<img src="../component-diagrams/structurizr-101372-ServiceDesignPlanningBackend.png" alt="Service Design Planning Component Diagram on API" width="350"/>

Mobile:

<img src="../component-diagrams/structurizr-101372-ServiceDesignPlanningMobileApp.png" alt="Service Design Planning Component Diagram on Mobile App" width="350"/>

## 4. Bounded Context Software Architecture Code Level Diagrams

### 4.1. Bounded Context Domain Layer Class Diagrams

Web App:

<img src="../class-diagrams/serviceDesignPlanningWeb.png" alt="Service Design Planning class diagram on Web App"/>

Mobile App:

<img src="../class-diagrams/serviceDesignPlanningMobile.png" alt="Service Design Planning class diagram on Mobile App"/>

Backend:

<img src="../class-diagrams/domain-layer-service-design-planning-order.png" alt="Service Design Planning class diagram on API"/>

### 4.2. Bounded Context Database Design Diagram

<img src="../tactical-level-ddd/db-diagrams/service-design-planning-orders-diagram.jpeg" alt="Service Design Planning Database Design Diagram"/>

---

## 5. Domain Layer

### Entities

**Order**

| Atributo              | Tipo     |
|-----------------------|----------|
| Id                    | int      |
| Action                | string   |
| UserId                | int      |
| SensorId              | int      |
| ActuatorId            | int      |
| CreatedAt             | DateTime |
| CompletedAt           | DateTime |
| StateId               | int      |
| SubscriptionId        | int      |

| Método                | Descripción                                               |
|-----------------------|-----------------------------------------------------------|
| UpdateOrderState      | Actualiza el estado de una orden.                         |

### Value Objects

**OrderStates**

| Atributo    | Descripción                                  |
|-------------|----------------------------------------------|
| ToComplete  | Representa el estado de una orden por completar|
| Completed   | Representa el estado de una orden completada  |

### Commands

| Clase                   | Descripción                                         |
|-------------------------|-----------------------------------------------------|
| CreateOrderCommand      | Comando para la creación de una nueva orden         |
| UpdateOrderStateCommand | Comando para la actualización de estado de una orden|
| SeedOrderStatesCommand  | Inicialización de datos para los estados de orden   |

### Queries

| Clase                  | Descripción                                         |
|------------------------|-----------------------------------------------------|
| GetOrdersByUserIdQuery | Consulta para obtener todas las órdenes de un usuario|

### Domain Services (Interfaces)

| Interface                | Descripción                                        |
|--------------------------|----------------------------------------------------|
| IOrderCommandService     | Operaciones que ejecutan cambios sobre Order        |
| IOrderStateCommandService| Operaciones sobre los estados de la orden          |

### Repositories (Interfaces)

| Interface           | Descripción                                            |
|---------------------|-------------------------------------------------------|
| IOrderRepository    | Contrato para persistencia y consultas sobre órdenes   |
| IOrderStateRepository| Contrato para persistencia y consultas sobre estados  |

---

## 6. Interface Layer

### Backend

#### Resources

| Clase                  | Descripción                                         |
|------------------------|-----------------------------------------------------|
| CreateOrderResource    | Solicitud de creación de una orden                  |
| OrderResource          | Datos de la entidad Order devueltos al cliente      |
| UpdateOrderStateResource| Solicitud de actualización de estado de una orden  |

#### Transforms/Assemblers

| Clase                                 | Descripción                                         |
|---------------------------------------|-----------------------------------------------------|
| CreateOrderCommandFromResourceAssembler| Transforma recurso en comando de creación de orden   |
| UpdateOrderStateCommandFromResourceAssembler| Transforma recurso en comando de actualización de estado |
| OrderResourceFromEntityAssembler      | Transforma entidad Order en recurso para el cliente  |

#### Controllers

**OrderController**

| Ruta especifica   | Descripción                                      |
|-------------------|--------------------------------------------------|
| /api/v1/orders    | Gestiona la creación y consulta de órdenes        |

---

## 7. Application Layer

### Backend

| Clase                | Interfaz Implementada   | Descripción                                 |
|----------------------|------------------------|---------------------------------------------|
| OrderCommandService  | IOrderCommandService   | Servicio que maneja los comandos de órdenes |

---

## 8. Infrastructure Layer

### Backend

| Clase            | Interfaz Implementada | Descripción                                         |
|------------------|----------------------|-----------------------------------------------------|
| OrderRepository  | IOrderRepository     | Implementa los métodos de consulta y persistencia    |

---

## 9. Diagramas

### Componentes
- Web App: ver sección 3
- Backend: ver sección 3
- Mobile: ver sección 3

### Clases
- Web App: ver sección 4
- Backend: ver sección 4
- Mobile: ver sección 4

### Base de datos
- Ver sección 4.2

