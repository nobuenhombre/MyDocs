# Как начать тестировать REST API используя Codeception

## 1). Установим codeception и flow/jsonpath (второй компонент для работы с json ответами)

```
composer require "codeception/codeception" --dev
composer require flow/jsonpath
```

## 2). Сделаем каталог для тестов зайдем в него и выполним следующие команды

### 2.1).
```
codecept bootstrap
```

Создаст файловую струтуру тестов - появится конфиг codeception.yml и папочка tests

вот примерное содержимое файла codeception.yml
```
paths:
    tests: tests
    output: tests/_output
    data: tests/_data
    support: tests/_support
    envs: tests/_envs
actor_suffix: Tester
extensions:
    enabled:
        - Codeception\Extension\RunFailed
settings:
    bootstrap: _bootstrap.php
```
если надо - доводим до кондиции - 
_bootstrap.php - это наш файлик в котором можно подключить свои модули

### 2.2).
```
codecept generate:suite api
```

Создаст внутри папочки tests файл api.suite.yml
вот примерное содержимое файла api.suite.yml
```
actor: ApiTester
modules:
    enabled:
        - REST:
            url: https://api.service.ru/
            depends: PhpBrowser
        - \Helper\Api
```

### 2.3).
```
codecept build
```

сгенерирует файлики в каталог 
/tests/_support/_generated

## 3). Собственно осталось только создать тест
```
codecept generate:cest api TestName
```
