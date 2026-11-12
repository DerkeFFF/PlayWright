# 1. Установка
Устанавливатся коммандой: playwright install
Но перед этим нужно устаночить необходмые браузеры:

    uv add paytest-playwright

# Пример теста:

    import re
    from playwright.sync_api import Page, expect


    def test_has_title(page: Page):
    page.goto(" ")

    # Expect a title "to contain" a substring.
    expect(page).to_have_title(re.compile("Playwright"))


    def test_get_started_link(page: Page):
    page.goto(" ")

    # Click the get started link.
    page.get_by_role("link", name="Get started").click()

    # Expects page to have a heading with the name of Installation.
    expect(page.get_by_role("heading", name="Installation")).to_be_visible()

   
    
# Системные требования:
Python 3.8 или выше.
Windows 11+, Windows Server 2019+ или подсистема Windows для Linux (WSL).
macOS 14 (Sonoma) или более поздняя версия.
Debian 12 / 13, Ubuntu 22.04 / 24.04 / 26.04 (x86-64 или arm64).

# 2. Навигация:

большинство тестов начинаются с пререхоа на страницу по указанному URL
PlayWright будет ждать, пока страница польность не загрузится.

# Взаимодейстаия 

Выполнение действий начинается с определения местоположения элементов.
Для этого Playwright используеn API локаторов.


```bash
Create a locator.
get_started = page.get_by_role("link", name="Get started")

 Click it.
get_started.click()

В большинстве случаев это будет написано в одну строку:

page.get_by_role("link", name="Get started").click()
```

# Основные действия:

Действие	                 Описание
-```locator.check()```	          Установите флажок ввода.
-```locator.click()```	          Нажмите на элемент
-```locator.uncheck()```	        Снимите флажок с поля ввода.
-```locator.hover()```	          Наведите курсор мыши на элемент.
-```locator.fill()```	            Заполните поле формы, введите текст.
-```locator.focus()```	          Сфокусируйте элемент
-```locator.press()```	          Нажмите одну клавишу
-```locator.set_input_files()```	Выберите файлы для загрузки
-```locator.select_option()```	  Выберите вариант в выпадающем списке.

# Использование Приспособлений:

Вы можете использовать различные фикстуры для выполнения кода до или после тестов, а также для обмена объектами между ними.

```bash
import pytest
from playwright.sync_api import Page, expect

@pytest.fixture(scope="function", autouse=True)
def before_each_after_each(page: Page):
    
    print("before the test runs")

    # Go to the starting url before each test.
    page.goto("https://playwright.dev/")
    yield
    
    print("after the test runs")

def test_main_navigation(page: Page):
     Assertions use the expect API.
    expect(page).to_have_url(" ")
```

# 3. Генерация тестов

Используйте codegen команду для запуска генератора тестов, за которой следует URL-адрес веб-сайта, для которого вы хотите сгенерировать тесты. URL-адрес необязателен.

```playwright codegen demo.playwright.dev/todomvc```

# Запись теста

Запускайте codegenи выполняйте действия в браузере.

С помощью генератора тестов вы можете записать:

Действия, такие как клик или заполнение, осуществляются посредством взаимодействия со страницей.
Для проверки необходимо щелкнуть значок на панели инструментов, а затем щелкнуть элемент страницы, для которого нужно выполнить проверку. Вы можете выбрать:
- ```assert visibility``` утверждать, что элемент видим
- ```assert text``` утверждать, что элемент содержит определенный текст.
- ```assert value``` утверждать, что элемент имеет определенное значение
- 
- После завершения работы со страницей нажмите ```record``` кнопку, чтобы остановить запись, и используйте эту ```copy``` кнопку, чтобы скопировать сгенерированный код в свой редактор.
- Используйте ```clear``` кнопку, чтобы очистить код и начать запись заново.

# Эмуляция

Вы можете создавать тесты, используя эмуляцию для определенных областей просмотра, устройств, цветовых схем, геолокации, языка или часового пояса.

# 4. Запуск и отладка тестов

# Командная строка
Для запуска тестов используйте pytestкоманду.

```bash
pytest
```

# Запускайте тесты в режиме с заголовком
Для запуска тестов в режиме просмотра с заголовком используйте ```--headed```

```bash
pytest --headed
```
# Проведите тесты в разных браузерах
Чтобы указать, в каком браузере вы хотите запускать тесты, используйте ```--browser``` 

```bash
pytest --headed webkit
```
чтобы указать несколько браузеров для запуска тестов, используйте -```-browser``` флаг несколько раз, а затем укажите название каждого браузера.


```bash
pytest --browser webkit --browser firefox
```
# Выполните определенные тесты
Для запуска отдельного тестового файла укажите имя тестового файла, который вы хотите запустить.

```bash
pytest test_login.py
```

Чтобы запустить набор тестовых файлов, передайте имена файлов, которые вы хотите запустить.

```bash
pytest tests/test_todo_page.py tests/test_landing_page.py
```

Для запуска конкретного теста передайте имя функции, которую вы хотите запустить.

```bash
pytest -k test_add_a_todo_item
```
# Запуск тестов параллельно
Для параллельного запуска тестов используйте ```--numprocesses``` флаг, за которым следует количество процессов, на которых вы хотите запустить тесты.

```bash
pytest --numprocesses 2
```

(Предполагается, что программа ```pytest-xdist``` установлена.)

# 5. Просмотр трассировки

# Запись трассы

Трассировку можно записать, запустив тесты с соответствующим ```--tracing``` флагом.

```bash
pytest --tracing on
```

Варианты отслеживания:

```on``` Запись трассировки для каждого теста
```off:``` Не записывать трассировку. (по умолчанию)
```retain-on-failure``` Записывайте трассировку для каждого теста, но удаляйте все трассировки из успешных запусков тестов.

# 5. Настройка GitHub Actions

# Настройка GitHub Actions
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

После настройки рабочего процесса GitHub Actions вам останется только создать репозиторий на GitHub или отправить свой код в существующий репозиторий.

# Открытие рабочих процессов
Перейдите на вкладку ```«Действия»``` , чтобы просмотреть рабочие процессы. Здесь вы можете увидеть, прошли ли ваши тесты или нет

# Просмотр журналов тестирования
При нажатии на кнопку запуска рабочего процесса отображаются все действия, выполненные GitHub, а при нажатии на кнопку ```«Запустить тесты Playwright»``` отображаются сообщения об ошибках.

# Просмотр следа
```trace.playwright.dev``` — это статически размещенный вариант Trace Viewer. Вы можете загружать файлы трассировки с помощью перетаскивания.

# Правильное обращение с секретами
Артефакты тестирования (трассировки и логи) могут содержать конфиденциальные данные, поэтому храните их в CI и передавайте команде только через доверенные сервисы или в зашифрованном виде.
