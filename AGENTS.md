# AGENTS.md — Agente Hotel (Persistência)

## Stack Principal
- Linguagem: Python
- Frameworks: Agno, Openai, Flask, Flask-Cors, Supabase
- Front-End: HTML, CSS e JS (arquivo único em `static/index.html`)

## Como rodar
- Ambiente virtual local: `.venv\Scripts\python.exe` (Python 3.14). `python` NÃO está no PATH do sistema — use o executável do venv.
- Subir o servidor: `.venv\Scripts\python.exe app.py`
- O app roda na porta **8000** (`app.run(port=8000, host="0.0.0.0", debug=True)`) — não na porta padrão 5000 do Flask.
- Acessar o front-end em `http://localhost:8000/` (servido via `send_static_file("index.html")`).

## Arquitetura (backend em `app.py`)
- `supabase` client criado no topo usando `SUPABASE_URL` / `SUPABASE_KEY` do `.env` via `load_dotenv()`.
- Rotas:
  - `POST /perguntar` e `POST /agente` → resposta do Agno (chave JSON `resposta`)
  - `POST /reserva` e `POST /reservas` → insere no Supabase na tabela `reservas`
  - `GET /reservas` → lista registros da tabela `reservas`
- Não há `requirements.txt`, testes, linter ou CI configurados. Dependências instaladas no `.venv`.

## Railguards (não quebrar)
- Não alterar a lógica do projeto.
- Não alterar nem criar arquivos sem pedir permissão.
- Não instalar bibliotecas desnecessárias.
- Não expor nem ler arquivos `.env` e `.gitignore`.
- Não alterar a `description` do agente do hotel (contém preços/serviços que a IA usa).
- Não alterar a estrutura de rotas do Flask nem as chaves dos JSON de retorno (o JS de `static/index.html` depende delas).

## Preferências
- Responder sempre em PT-BR.
- Colocar comentários no código, facilitando a leitura para um programador iniciante (e para releitura futura).
