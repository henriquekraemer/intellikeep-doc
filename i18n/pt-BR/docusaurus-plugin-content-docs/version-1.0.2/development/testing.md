---
sidebar_position: 2
title: Executando Testes
---

# Executando Testes

O IntelliKeep usa `pytest` para testes de backend.

## Executar via Docker (recomendado)

Nenhuma instalação local de Python necessária.

```bash
# Todos os testes
./run-tests.sh

# Arquivo específico
./run-tests.sh tests/test_task_manager.py

# Com filtro
./run-tests.sh -k test_complete_recurring
```

## Executar localmente

```bash
pip install -r requirements_test.txt
pytest tests/ -v
```

## Estrutura de testes

Os testes estão localizados no diretório `tests/` do repositório IntelliKeep. A suíte de testes cobre:
- Criação, atualização, conclusão e exclusão de tarefas
- Lógica de agendamento de tarefas recorrentes
- Condições de disparo de notificações
- Validação de ações de serviço
