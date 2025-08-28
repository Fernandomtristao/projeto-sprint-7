Projeto 7 — QA Automation (Python)

Visão geral

Projeto 7 é uma suíte de automação de testes em Python focada em qualidade de software. O objetivo é demonstrar práticas de testes automatizados (UI / API / E2E), organização de projeto, execução contínua e relatórios claros.

Funcionalidades

Testes automatizados para APIs e/ou interfaces web.

Estrutura modular de testes (fixtures, páginas/objetos, utils).

Suporte a execução local e em CI (GitHub Actions, GitLab CI, etc.).

Relatórios em HTML / JUnit.

Integração com ferramentas de linting e formatação (flake8, black).

Exemplos de dados de teste e geração de relatórios.

Stack Tecnológica

Python 3.10+

Frameworks de testes: pytest (ou unittest conforme preferência)

Requests/HTTP: requests (para API tests)

Automação de UI (opcional): playwright ou selenium

Gerador de relatórios: pytest-html, allure (opcional)

Lint/format: flake8, black

Use o que fizer mais sentido para o objetivo do seu projeto.

Estrutura sugerida do repositório
Projeto7/
├── README.md
├── requirements.txt
├── pyproject.toml
├── tests/
│   ├── api/
│   │   └── test_example_api.py
│   ├── ui/
│   │   └── test_example_ui.py
│   └── conftest.py
├── src/
│   └── app_helpers.py
├── pages/                # (se usar Page Object Model)
│   └── login_page.py
├── reports/
│   └── html_report.html
└── .github/workflows/    # (CI)
    └── python-tests.yml

Requisitos

Instale Python 3.10+ e crie um ambiente virtual:

python -m venv .venv
source .venv/bin/activate   # macOS / Linux
.venv\Scripts\activate      # Windows
pip install -r requirements.txt


Exemplo do requirements.txt:

pytest
requests
pytest-html
playwright  # opcional
flake8
black

Como rodar os testes (local)

Executar todos os testes:

pytest


Gerar relatório HTML:

pytest --html=reports/report.html --self-contained-html


Executar apenas testes de API:

pytest tests/api


Executar testes de UI com Playwright (exemplo de instalação + execução):

# instalar os navegadores (apenas na primeira vez)
playwright install

# rodar
pytest tests/ui

Boas práticas e recomendações

Use fixtures no conftest.py para configurar clientes, auth tokens e setup/teardown.

Separe dados de teste (fixtures/JSON) do código de teste.

Mantenha testes determinísticos; evite dependência em estado externo não controlado.

Versione relatórios importantes (ou armazene como artefatos no CI).

Integre linting e formatação no CI para manter qualidade do código.

Exemplo rápido (pytest)

tests/api/test_example_api.py

import requests

BASE_URL = "https://api.exemplo.com"

def test_get_health():
    resp = requests.get(f"{BASE_URL}/health")
    assert resp.status_code == 200
    assert resp.json().get("status") == "ok"

Integração CI (exemplo - GitHub Actions)

.github/workflows/python-tests.yml (resumo)

name: Python Tests

on: [push, pull_request]

jobs:
  tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Run tests
        run: pytest --junitxml=reports/junit.xml --html=reports/report.html --self-contained-html
      - name: Upload report
        uses: actions/upload-artifact@v4
        with:
          name: reports
          path: reports/

Como contribuir

Fork o repositório.

Crie uma branch feature/bugfix.

Adicione testes para qualquer funcionalidade nova/ajustada.

Abra um Pull Request descrevendo as mudanças.

Licença

Escolha uma licença (ex.: MIT). Adicione arquivo LICENSE com o conteúdo.

Contato / Referência do repositório

Repositório-base (seu fork/clone): 

Se quiser, eu posso:

Gerar um requirements.txt pronto com as versões.

Criar um conftest.py de exemplo com fixtures comuns.

Escrever um workflow de GitHub Actions completo com upload de artefatos.

Quer que eu gere algum desses arquivos agora?
