---
sidebar_position: 2
title: Ejecutar Pruebas
---

# Ejecutar Pruebas

IntelliKeep usa `pytest` para las pruebas de backend.

## Ejecutar mediante Docker (recomendado)

No se requiere instalación local de Python.

```bash
# Todas las pruebas
./run-tests.sh

# Archivo específico
./run-tests.sh tests/test_task_manager.py

# Con filtro
./run-tests.sh -k test_complete_recurring
```

## Ejecutar localmente

```bash
pip install -r requirements_test.txt
pytest tests/ -v
```

## Estructura de pruebas

Las pruebas están ubicadas en el directorio `tests/` del repositorio IntelliKeep. La suite de pruebas cubre:
- Creación, actualización, finalización y eliminación de tareas
- Lógica de programación de tareas recurrentes
- Condiciones de disparo de notificaciones
- Validación de acciones de servicio
