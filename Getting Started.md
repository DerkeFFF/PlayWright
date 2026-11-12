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

# 6. Справочник по плагину pytest

# Использование
Для запуска тестов используйте Pytest CLI.

pytest --browser webkit --headed

Если вы хотите автоматически добавлять аргументы командной строки без их указания, вы можете использовать файл pytest.ini :

# content of pytest.ini
[pytest]
# Run firefox with UI
addopts = --headed --browser firefox

# Аргументы командной строки
Обратите внимание, что аргументы командной строки применяются только к значениям по умолчанию browserи фикстурам.

--headed: Запуск тестов в режиме с графическим интерфейсом (по умолчанию: без графического интерфейса).
--browser: Запуск тестов в другом браузере chromium, firefox, или webkit. Его можно указать несколько раз (по умолчанию: chromium).
--browser-channel Канал браузера , который будет использоваться.
--slowmoЗамедляет работу программы Playwright на указанное количество миллисекунд. Полезно для того, чтобы вы могли видеть, что происходит (по умолчанию: 0).
--device Устройство, которое необходимо эмулировать.
--outputКаталог для артефактов, созданных тестами (по умолчанию: test-results).
--tracingСледует ли записывать трассировку для каждого теста. on, off, или retain-on-failure(по умолчанию: off).
--videoСледует ли записывать видео для каждого теста. on, off, или retain-on-failure(по умолчанию: off).
--screenshotАвтоматически ли делать снимок экрана после каждого теста. on, off, или only-on-failure(по умолчанию: off).
--full-page-screenshotСледует ли делать снимок экрана всей страницы в случае сбоя. По умолчанию делается снимок только области просмотра. Требуется --screenshotвключить эту функцию (по умолчанию: off).

# Оборудовани
Этот плагин настраивает специфические для Playwright тестовые фикстуры для pytest 

def test_my_app_is_working(fixture_name):
    pass
    # Test using fixture_name
    # ...

Область видимости функций : Эти тестовые объекты создаются по запросу в тестовой функции и уничтожаются по завершении теста.

context: Новый контекст браузера для теста.
page: Новая страница браузера для теста.
new_contextПозволяет создавать различные контексты браузера для теста. Полезно для многопользовательских сценариев. Принимает те же параметры, что и browser.new_context() .

Область видимости сессии : Эти тестовые данные создаются по запросу в тестовой функции и уничтожаются после завершения всех тестов.

playwrightПример драматурга .
browser_type: Тип браузера : экземпляр текущего браузера.
browser: Экземпляр браузера , запущенный Playwright.
browser_name: Название браузера в виде строки.
browser_channel: Канал браузера в виде строки.
is_chromium, is_webkit, is_firefox: Логические значения для соответствующих типов браузеров.
Настройка параметров запуска : Для элементов browserуправления contextиспользуйте следующие элементы управления, чтобы определить пользовательские параметры запуска.

browser_type_launch_args: Переопределите аргументы запуска для browser_type.launch() . Он должен возвращать словарь.
browser_context_args: Переопределите параметры для browser.new_context() . Он должен возвращать словарь.
connect_options: Подключиться к существующему браузеру через конечную точку WebSocket. Должен вернуться словарь с параметрами browser_type.connect() .

Также можно переопределить параметры контекста

import pytest

@pytest.mark.browser_context_args(timezone_id="Europe/Berlin", locale="en-GB")
def test_browser_context_args(page):
    assert page.evaluate("window.navigator.userAgent") == "Europe/Berlin"
    assert page.evaluate("window.navigator.languages") == ["de-DE"]

# Параллелизм: выполнение нескольких тестов одновременно.
Если ваши тесты выполняются на машине с большим количеством процессоров, вы можете ускорить общее время выполнения набора тестов, используя pytest-xdistфункцию одновременного запуска нескольких тестов:

# install dependency
pip install pytest-xdist
# use the --numprocesses flag
pytest --numprocesses auto

В зависимости от аппаратного обеспечения и характера ваших тестов, вы можете установить numprocessesзначение, равное 2количеству процессоров на машине. \

Общую информацию о доступных параметрах см. в разделе «Запуск тестов»pytest .
