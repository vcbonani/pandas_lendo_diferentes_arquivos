# Pandas I/O: lendo e escrevendo diferentes formatos de arquivo

Projeto prático do curso **Pandas I/O: Trabalhando com diferentes formatos de arquivos** (Alura). O notebook percorre o ciclo completo de entrada e saída de dados com Pandas: ler, tratar e gravar em CSV, Excel, Google Planilhas, JSON, HTML, XML e banco de dados SQL.

## O que o projeto mostra

| Formato | Leitura | Escrita | Destaques |
|---|---|---|---|
| **CSV** | `read_csv` | `to_csv` | `sep`, `nrows`, `usecols`, `encoding`, `header`, `skipfooter`; detecção de codificação com `chardet` |
| **Excel** | `read_excel` | `to_excel` | `sheet_name`, `usecols` por intervalo (`'A:D'`), `nrows`, `ExcelFile().sheet_names` |
| **Google Planilhas** | `read_csv` via endpoint `gviz/tq` | n/a | extração do ID da planilha com regex e leitura de abas específicas |
| **JSON** | `read_json`, `json_normalize`, módulo `json` | `to_json` | normalização de JSON aninhado (`record_path`) e consumo de API pública com `requests` |
| **HTML** | `read_html` | `to_html` | extração de tabelas de páginas da Wikipédia e limpeza com regex |
| **XML** | `read_xml` | `to_xml` | seleção de colunas com `iloc` e exportação sem índice |
| **Banco de dados** | `read_sql`, `read_sql_table` | `to_sql` | SQLite em memória com SQLAlchemy, `INSERT`, `UPDATE` e `DELETE` com `text()` |

## Desafios resolvidos

- **CSV com vários parâmetros:** leitura do `dados_sus` com separador `;`, encoding `ISO-8859-1`, cabeçalho na 4ª linha e descarte de rodapé.
- **Google Planilhas de outro link:** ID extraído da URL com regex e dados exportados para CSV.
- **JSON da API:** normalização da resposta de usuários da API JSONPlaceholder.
- **Tabela de página web:** lista de países por população, com remoção de notas `[nota 1]` e conversão da coluna de população para inteiro.
- **Manipulação de banco:** `UPDATE`, `DELETE` e `INSERT` na tabela `clientes_banco`, conferindo os dados antes e depois.

## Estrutura do repositório

```
pandas_lendo_diferentes_arquivos/
├── README.md
├── requirements.txt
├── notebook/
│   └── Pandas_IO.ipynb
└── dados/
    ├── entrada/    # arquivos lidos pelo notebook
    └── saida/      # arquivos gerados pelo notebook
```

## Bases de dados

Arquivos locais em `dados/entrada/`: `superstore_data.csv`, `pacientes.json`, `pacientes_2.json`, `filmes_wikipedia.html`, `imdb_top_1000.xml` e `Lista de países por população.html`.

Bases lidas direto de URL (não ficam no repositório):

- Emissões de CO₂ (Excel com 3 abas) e clientes de banco (CSV), no repositório de materiais do curso na Alura
- `dados_sus.csv` e `superstore_data_ponto_virgula.csv`, no mesmo repositório do curso
- Planilha pública no Google Planilhas
- API pública [JSONPlaceholder](https://jsonplaceholder.typicode.com/users)

## Tecnologias

Python, Pandas, SQLAlchemy (SQLite), Requests, Chardet, OpenPyXL, lxml e Jupyter Notebook.

## Como executar

```bash
git clone https://github.com/vcbonani/pandas_lendo_diferentes_arquivos.git
cd pandas_lendo_diferentes_arquivos

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

cd notebook
jupyter notebook Pandas_IO.ipynb
```

Abra o notebook a partir da pasta `notebook/`, porque os caminhos são relativos (`../dados/entrada/` e `../dados/saida/`). Algumas células leem dados da internet, então é preciso estar conectado.

## Observações

- Na leitura via Google Planilhas, números com ponto de milhar chegam como texto. Para convertê-los, use `thousands='.'` no `read_csv`.
- No Google Colab, os caminhos relativos não funcionam. Faça upload dos arquivos de `dados/` e ajuste os caminhos.

## Autor

**Vinícius Cunha**: [GitHub](https://github.com/vcbonani)
