# API REST Menú Digital Restaurante

API REST desarrollada en Ruby on Rails para gestionar un menú digital de restaurante con funcionalidades completas de administración, inventario, asistencia y ventas.

## Características

- **Autenticación JWT**: Login seguro para administradores y empleados
- **Gestión de Productos**: CRUD de productos con imágenes y categorías
- **Inventario**: Control de ingredientes con fotografías y alertas de stock mínimo
- **Checador de Asistencia**: Control de entrada/salida con gestión de descansos
- **Gestión de Órdenes**: Sistema completo de pedidos (dine-in/pickup)
- **Sistema de Clientes**: Base de datos de clientes con historial
- **Promociones**: Gestión de ofertas y descuentos
- **Reportes de Ventas**: Análisis detallado de ventas y rendimiento

## Requisitos

- Ruby 3.1.0
- Rails 7.0.4
- SQLite3
- ImageMagick (para procesamiento de imágenes)

## Instalación

1. Clonar el repositorio
```bash
git clone <url-del-repositorio>
cd restaurant-api
```

2. Instalar dependencias
```bash
bundle install
```

3. Configurar la base de datos
```bash
rails db:create
rails db:migrate
rails db:seed
```

4. Iniciar el servidor
```bash
rails server
```

## Endpoints Principales

### Autenticación
```
POST /auth/login
```

### Gestión de Usuarios
```
GET /api/v1/users          # Listar usuarios (admin)
POST /api/v1/users         # Crear usuario
GET /api/v1/users/profile  # Perfil del usuario actual
```

### Productos
```
GET /api/v1/products                # Listar productos
POST /api/v1/products               # Crear producto (admin)
PUT /api/v1/products/:id            # Actualizar producto (admin)
GET /api/v1/products/:id            # Ver producto
```

### Inventario
```
GET /api/v1/ingredients                    # Listar ingredientes
POST /api/v1/ingredients                   # Agregar ingrediente
POST /api/v1/ingredients/:id/adjust_stock  # Ajustar inventario
```

### Asistencia
```
POST /api/v1/attendances/check_in          # Marcar entrada
POST /api/v1/attendances/:id/check_out     # Marcar salida
POST /api/v1/attendances/:id/start_break   # Iniciar descanso
POST /api/v1/attendances/:id/end_break     # Terminar descanso
GET /api/v1/attendances/summary            # Reporte de asistencias
```

### Órdenes
```
GET /api/v1/orders           # Listar órdenes
POST /api/v1/orders          # Crear orden
PUT /api/v1/orders/:id       # Actualizar estado
PUT /api/v1/orders/:id/cancel # Cancelar orden
```

### Reportes
```
GET /api/v1/sales/report               # Reporte de ventas
GET /api/v1/sales/product_performance  # Rendimiento por producto
```

## Autenticación

La API utiliza JWT para autenticación. Incluir el token en el header:
```
Authorization: Bearer <token>
```

## Roles

- **Admin**: Acceso completo a todas las funcionalidades
- **Employee**: Acceso a órdenes, asistencia y visualización de productos

## Credenciales de Prueba

- **Admin**: admin@restaurante.com / password123
- **Empleado**: empleado@restaurante.com / password123

## Estructura de Datos

### Producto
```json
{
  "id": 1,
  "name": "Quesadillas de Pollo",
  "description": "Quesadillas rellenas de pollo y queso",
  "price": 85.00,
  "active": true,
  "image_url": {
    "original": "/uploads/...",
    "thumb": "/uploads/...",
    "medium": "/uploads/..."
  },
  "categories": [...],
  "ingredients": [...]
}
```

### Orden
```json
{
  "id": 1,
  "order_type": "dine_in", // o "pickup"
  "status": "pending",     // pending, confirmed, preparing, ready, delivered, cancelled
  "total": 170.00,
  "special_instructions": "Sin cebolla",
  "order_items": [
    {
      "id": 1,
      "quantity": 2,
      "unit_price": 85.00,
      "product": {...}
    }
  ],
  "customer": {...}
}
```

## Consideraciones de Producción

1. Configurar variables de entorno para secretos
2. Usar un sistema de almacenamiento para imágenes (S3, Cloudinary)
3. Implementar rate limiting
4. Configurar CORS apropiadamente
5. Usar una base de datos más robusta (PostgreSQL)
6. Implementar respaldos automáticos
7. Configurar monitoreo y logging

## Contribuir

Las contribuciones son bienvenidas. Por favor, abre un issue primero para discutir los cambios que te gustaría realizar.

## Licencia

MIT License
