# Публикация пакета py2jupyter на PyPI

## Подготовка к публикации

1. **Создайте аккаунт на PyPI** (если ещё нет):
   - https://pypi.org/account/register/

2. **Создайте API токен**:
   - Зайдите в настройки аккаунта PyPI
   - Создайте новый API токен с scope "Entire account"

3. **Установите twine** (уже установлено):
   ```bash
   pip install twine
   ```

## Публикация

### Тестирование на Test PyPI (рекомендуется сначала)

```bash
# Создайте аккаунт на https://test.pypi.org/
# Создайте API токен для test.pypi.org

# Загрузите пакет на Test PyPI
python -m twine upload --repository testpypi dist/*

# Установите для тестирования
pip install --index-url https://test.pypi.org/simple/ py2jupyter
```

### Публикация на Production PyPI

```bash
# Загрузите пакет на основной PyPI
python -m twine upload dist/*

# Теперь можно устанавливать из основного репозитория
pip install py2jupyter
```

## Структура пакета

```
/home/antonov/Base/Libs/Py2Nb/
├── pyproject.toml          # Конфигурация пакета
├── MANIFEST.in            # Список включаемых файлов
├── py2jupyter/            # Основной пакет
│   ├── __init__.py
│   └── __main__.py        # Основной код конвертера
├── README.md              # Описание пакета
├── LICENSE                # Лицензия
├── VERSION                # Версия
├── ARTICLE.md             # Статья о библиотеке
├── AI_GUIDE.md            # Руководство для AI
├── PY_FORMAT_RULES.md     # Правила форматирования
├── example/               # Примеры использования
└── dist/                  # Собранные дистрибутивы (после build)
```

## Проверка перед публикацией

- [x] Пакет собирается без ошибок (`python -m build`)
- [x] Команда `py2jupyter` работает после установки
- [x] Конвертация работает в обе стороны
- [x] Документация включена в пакет
- [x] Лицензия указана корректно
- [x] Все тесты проходят

## Обновление версии

При выпуске новой версии:
1. Обновите версию в `VERSION` и `pyproject.toml`
2. Создайте git tag: `git tag v0.1.2`
3. Соберите пакет: `python -m build`
4. Опубликуйте: `python -m twine upload dist/*`
