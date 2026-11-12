# 1. Настройка GitHub Actions

# 1.1 Настройка GitHub Actions
Чтобы добавить файл ```GitHub Actions``` , сначала создайте ```.github/workflows``` папку, а внутри неё добавьте ```playwright.yml``` файл, содержащий пример кода, приведённый ниже, чтобы ваши тесты запускались при каждом ```push-``` и ```pull-``` запросе для основной/ветки ```master```.

```bash
name: Playwright Tests
on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v6
    - name: Set up Python
      uses: actions/setup-python@v6
      with:
        python-version: '3.13'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Ensure browsers are installed
      run: python -m playwright install --with-deps
    - name: Run your tests
      run: pytest --tracing=retain-on-failure
    - uses: actions/upload-artifact@v5
      if: ${{ !cancelled() }}
      with:
        name: playwright-traces
        path: test-results/
```

# 2. Создайте репозиторий и отправьте изменения в GitHub.

После настройки рабочего процесса GitHub Actions вам останется только создать репозиторий на GitHub или отправить свой код в существующий репозиторий.

# 3. Открытие рабочих процессов

Перейдите на вкладку ```«Действия»``` , чтобы просмотреть рабочие процессы. Здесь вы можете увидеть, прошли ли ваши тесты или нет

# 4. Просмотр журналов тестирования

При нажатии на кнопку запуска рабочего процесса отображаются все действия, выполненные GitHub, а при нажатии на кнопку «Запустить тесты Playwright» отображаются сообщения об ошибках.

# 5. Просмотр следа

```trace.playwright.dev``` — это статически размещенный вариант Trace Viewer. Вы можете загружать файлы трассировки с помощью перетаскивания.

# 6. Правильное обращение с секретами

Артефакты тестирования (трассировки и логи) могут содержать конфиденциальные данные, поэтому храните их в CI и передавайте команде только через доверенные сервисы или в зашифрованном виде.

