# Flask-ton-miniapp
Telegram mini App Flask. с офлайн майнингом, бустами и TON- кошелекем
# Flask TON Mini App

**Telegram Mini App** на Flask: оффлайн-майнинг с бустами, задания-подписки, реферальная система и привязка TON-кошелька (TON Connect).

##  Фичи
-    Telegram WebApp авторизация
-    Привязка TON-кошелька
-    Оффлайн-майнинг: множество скоростей ×2, ×5, ×10, ×100
-    Задания-подписки за вознаграждение TON
-    Двухуровневая реферальная структура (7% / 3%)
-    Вывод: минимум 1 TON + ≥ 5 рефералов + подписка на `@crypto_vsem_b_o_t`

##  Установка и запуск

```bash
git clone https://github.com/LeshiyCrypto/Flask-ton-miniapp.git
cd Flask-ton-miniapp
python -m venv venv
source venv/bin/activate  # или venv\Scripts\activate на Windows
pip install -r requirements.txt
flask run
backend/
├─ app.py
├─ models.py
├─ config.py
frontend/
├─ webapp.html
└─ ton_connect_stub.js
README.md
# Используем официальный Python
FROM python:3.11

# Задаём рабочую директорию
WORKDIR /app

# Копируем зависимости
COPY requirements.txt .

# Устанавливаем зависимости
RUN pip install --no-cache-dir -r requirements.txt

# Копируем всё приложение
COPY . .

# Открываем порт
EXPOSE 5000

# Запускаем Flask
CMD ["flask", "--app", "backend/app.py", "run", "--host=0.0.0.0", "--port=5000"]
services:
  - type: web
    name: flask-ton-miniapp
    env: python
    plan: free
    buildCommand: ""
    startCommand: flask --app backend/app.py run --host=0.0.0.0 --port=5000
    envVars:
      - key: BOT_TOKEN
        sync: false
      - key: SECRET_KEY
        sync: false
