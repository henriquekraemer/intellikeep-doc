---
sidebar_position: 2
title: Executando Testes
---

# Executando Testes

O IntelliKeep usa `pytest` para os testes do backend.

## Rodando via Docker (recomendado)

Não é preciso ter Python instalado localmente.

```bash
# All tests
./run-tests.sh

# Specific file
./run-tests.sh tests/test_task_manager.py

# With filter
./run-tests.sh -k test_complete_recurring
```

Por padrão, os testes rodam com a versão atual do Home Assistant. Para testar com a versão mais antiga suportada (2026.2.x), use a imagem do Python 3.13:

```bash
PYTHON_IMAGE=python:3.13-slim ./run-tests.sh
```

## Rodando localmente

O Home Assistant atual precisa do Python 3.14 ou mais recente.

```bash
pip install -r requirements_test.txt
pytest tests/ -v
```

## Estrutura dos testes

Os testes ficam na pasta `tests/` do repositório do IntelliKeep. A suíte cobre:
- Criação, atualização, conclusão, reabertura e exclusão de tarefas
- Agendamento de tarefas recorrentes: intervalos de repetição, a âncora de agendamento, dias da semana, fins de mês e mudanças de horário de verão
- As entidades de lista de tarefas e de calendário
- Condições de disparo das notificações
- Validação das ações de serviço

## Integração contínua

O GitHub Actions roda os testes no Python 3.14 (Home Assistant atual) e no Python 3.13 (Home Assistant 2026.2.x) a cada push e pull request, e uma vez por semana para pegar quebras causadas por novas versões do Home Assistant. A validação do HACS, o `hassfest` e um build do frontend também rodam nos pushes e pull requests para a `main`.
