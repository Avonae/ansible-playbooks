# Ansible Playbook for Secure Server Setup
[![ansible-lint](https://github.com/Avonae/ansible-playbooks/actions/workflows/ansible-lint.yml/badge.svg?branch=main)](https://github.com/Avonae/ansible-playbooks/actions/workflows/ansible-lint.yml)
## Описание
Этот плейбук Ansible настраивает сервер с безопасными конфигурациями, включая:
- Настройка SSH на случайный порт
- Создание пользователя `alex` с правами sudo и доступом к Docker
- Уведомления в Telegram о каждом входе в систему

## Структура проекта
- `playbook.yml`: Основной плейбук
- `inventory.ini`: Файл инвентаря с IP-адресом сервера
- `group_vars/all.yml`: Переменные, используемые в плейбуке

## Установка и запуск
1. Клонируйте репозиторий.
2. Обновите файл `inventory.ini` с IP и пользователем для вашего сервера.
3. Запустите плейбук:
   ```bash
   ansible-playbook -i inventory.ini playbook.yml --ask-vault-pass

