# api-todo-list

Projeto de To-Do List em arquitetura de microsserviços desenvolvido em aula.

## Estrutura

```text
api-todo-list/
  frontend/
  api-laravel/
  api-express/
  api-fastapi/
```

## Responsabilidades

- `api-laravel`: cadastro e visualização de tarefas.
- `api-express`: registro de logs das ações.
- `api-fastapi`: estatísticas de tarefas consumindo banco do Laravel e do Express.
- `frontend`: interface web integrada aos três serviços.

## Instalação

### Git

```bash
https://git-scm.com/install/windows
```

### Laravel

- Laragon: [https://laragon.org/download](https://laragon.org/download)
- Composer: [https://getcomposer.org/download/](https://getcomposer.org/download/)

```bash
composer global require laravel/installer
laravel new project
```

ou

```bash
composer create-project laravel/laravel project
```

### Express

```bash
mkdir api-express
cd api-express
npm init -y
npm install express prisma @prisma/client cors
npm install nodemon --save-dev
npx prisma init
```

### FastAPI

```bash
python -m venv venv
source venv/bin/activate
pip install fastapi uvicorn sqlalchemy psycopg2-binary
```

Para este projeto (MySQL), use:

```bash
python -m venv venv
source venv/bin/activate
pip install fastapi uvicorn sqlalchemy python-dotenv pymysql
```

No Windows:

```bash
venv\Scripts\activate
```

## Fluxo de bootstrap (ordem)

1. Subir MySQL e criar os bancos `db-projeto-2026` e `projeto-log-2026`.
2. Rodar migrations do Laravel (`php artisan migrate`).
3. Rodar Prisma no Express (`npx prisma generate` e `npx prisma migrate dev` se necessário).
4. Subir as 3 APIs (`api-laravel`, `api-express`, `api-fastapi`).
5. Subir o `frontend`.

## Bootstrap por serviço

### api-laravel

```bash
cd api-laravel
copy .env.example .env
composer install
php artisan key:generate
php artisan migrate
php artisan serve --host=0.0.0.0 --port=8000
```

### api-express

```bash
cd api-express
copy .env.example .env
npm install
npx prisma generate
npm run dev
```

### api-fastapi

```bash
cd api-fastapi
copy .env.example .env
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8001
```

### frontend

```bash
cd frontend
python -m http.server 5500
```

Abrir: `http://127.0.0.1:5500`

## Contratos de API

- Laravel: `GET/POST /api/todos`, `PATCH /api/todos/{id}/toggle`, `DELETE /api/todos/{id}`
- Express: `POST /api/logs`, `GET /api/logs`
- FastAPI: `GET /api/stats`
