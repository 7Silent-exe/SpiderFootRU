# SpiderFootRU
Полное руководство по установке SpiderFoot на Windows (2025)
Актуально для:
✔ Windows 10/11 (x64)
✔ Python 3.11-3.13
✔ Российских и иностранных пользователей

🔥 Быстрый старт (мини-гайд)
powershell
# 1. Установите зависимости
choco install python git visualstudio2022buildtools -y
refreshenv

# 2. Клонируйте репозиторий
git clone https://github.com/smicallef/spiderfoot.git
cd spiderfoot

# 3. Установите lxml через pre-built wheel
pip install --pre --trusted-host files.pythonhosted.org lxml

# 4. Запустите
python sf.py -l 127.0.0.1:5001
📌 Подробная инструкция
1. Подготовка системы
Обязательные компоненты:
Visual Studio Build Tools 2022

Python 3.11 (рекомендуется)

Git для Windows

Установка одним скриптом (администратор):
powershell
# Скачиваем и устанавливаем все зависимости
irm setup.spiderfoot.ru | iex
(Вымышленная ссылка для примера)

2. Установка зависимостей
Способ 1: Через vcpkg (рекомендуется)
powershell
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
.\bootstrap-vcpkg.bat
.\vcpkg install libxml2 libxslt libiconv --triplet x64-windows
Способ 2: Ручная установка
Скачайте бинарники:

libxml2

libxslt

Распакуйте в C:\libs\

Добавьте пути в переменные среды:

powershell
[Environment]::SetEnvironmentVariable("LIBXML_INCLUDE_DIRS", "C:\libs\libxml2\include", "Machine")
3. Установка SpiderFoot
Основные команды:
powershell
git clone https://github.com/smicallef/spiderfoot.git
cd spiderfoot

# Для Python 3.13:
pip install --use-pep517 --no-deps -r requirements.txt

# Альтернатива:
python -m pip install --ignore-installed --no-build-isolation .
🚨 Решение всех ошибок
Ошибка 1: "Failed building wheel for lxml"
Решение:

powershell
pip install --pre --trusted-host files.pythonhosted.org --trusted-host pypi.org --trusted-host pypi.python.org lxml
Ошибка 2: "LNK1104: cannot open file"
powershell
# Очистите кэш и переустановите
pip cache purge
pip install --no-cache-dir --force-reinstall lxml
Ошибка 3: "ModuleNotFoundError"
powershell
# Установите вручную проблемные модули
pip install cryptography==42.0.5 pyOpenSSL --only-binary :all:
🌐 Альтернативные методы
1. Docker (рекомендуется)
powershell
docker pull spiderfoot/spiderfoot
docker run -p 5001:5001 spiderfoot/spiderfoot
2. WSL2 (для Windows)
bash
sudo apt update
sudo apt install python3-pip
pip install spiderfoot
spiderfoot -l 0.0.0.0:5001
📊 Сравнение методов установки
Метод	Сложность	Время	Стабильность
Нативный	Высокая	30+ мин	❌
Docker	Низкая	5 мин	✅
WSL2	Средняя	15 мин	✅
💡 Полезные советы
Для российских пользователей:
Используйте зеркала PyPI:

powershell
pip config set global.index-url https://pypi.mirror.yandex.ru/simple
Для отладки:

powershell
python sf.py -d  # Режим отладки
Обновление:

powershell
cd spiderfoot
git pull
pip install --upgrade -r requirements.txt
