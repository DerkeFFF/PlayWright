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

