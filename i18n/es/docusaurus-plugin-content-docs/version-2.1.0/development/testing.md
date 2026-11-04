---
sidebar_position: 2
title: Ejecutar pruebas
---

# Ejecutar pruebas

IntelliKeep usa `pytest` para las pruebas del backend.

## Ejecutar con Docker (recomendado)

No hace falta tener Python instalado en local.

```bash
# All tests
./run-tests.sh

# Specific file
./run-tests.sh tests/test_task_manager.py

# With filter
./run-tests.sh -k test_complete_recurring
```

De forma predeterminada, las pruebas se ejecutan con la versión actual de Home Assistant. Para probar con la línea compatible más antigua (2026.2.x), usa la imagen de Python 3.13:

```bash
PYTHON_IMAGE=python:3.13-slim ./run-tests.sh
```

## Ejecutar en local

La versión actual de Home Assistant necesita Python 3.14 o posterior.

```bash
pip install -r requirements_test.txt
pytest tests/ -v
```

## Estructura de las pruebas

Las pruebas están en el directorio `tests/` del repositorio de IntelliKeep. La batería de pruebas cubre:
- La creación, actualización, finalización, reapertura y eliminación de tareas
- La programación de tareas recurrentes: intervalos de repetición, el ancla de programación, días de la semana, finales de mes y cambios de horario de verano
- Las entidades de lista de tareas pendientes y de calendario
- Las condiciones que activan las notificaciones
- La validación de las acciones

## Integración continua

GitHub Actions ejecuta las pruebas con Python 3.14 (Home Assistant actual) y Python 3.13 (Home Assistant 2026.2.x) en cada push y pull request, y una vez por semana para detectar fallos provocados por nuevas versiones de Home Assistant. La validación de HACS, `hassfest` y una compilación del frontend también se ejecutan en los push y pull requests a `main`.
