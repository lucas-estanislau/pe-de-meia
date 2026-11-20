# Pé-de-Meia e o Abandono Escolar no Brasil

Análise exploratória de dados sobre a relação entre os pagamentos do programa **Pé-de-Meia** e os indicadores de rendimento escolar (aprovação, reprovação e abandono) do ensino médio da rede pública nas unidades da federação do Brasil.

O estudo utiliza dados de pagamentos do **Portal da Transparência** (2024–2026, com 2026 parcial na base utilizada) e taxas de rendimento escolar do **INEP** (2007–2025). A comparação entre pagamentos e abandono concentra-se sobretudo em 2024 e 2025.

> **Importante:** esta é uma análise descritiva/exploratória. Correlação ou variações observadas não permitem, por si só, atribuir causalmente ao Pé-de-Meia mudanças nas taxas de abandono.

## 1. Arquivos do repositório

| Arquivo | Finalidade |
| --- | --- |
| [`01-coleta-pdm.ipynb`](01-coleta-pdm.ipynb) | Coleta, processamento e agregação mensal dos pagamentos do Pé-de-Meia por UF e tipo de incentivo. |
| [`01_coleta_inep.ipynb`](01_coleta_inep.ipynb) | Leitura e tratamento das planilhas de taxas de rendimento escolar do INEP. |
| [`02_agregação.ipynb`](02_agrega%C3%A7%C3%A3o.ipynb) | Consolidação dos dados por ano/UF e integração das duas fontes. |
| [`03_analise_graficos_atualizados.ipynb`](03_analise_graficos_atualizados.ipynb) | Análise exploratória, comparações e visualizações. |
| [`requirements.txt`](requirements.txt) | Bibliotecas Python para executar os notebooks. |

## 2. Requisitos

- Conta Google com acesso ao **Google Drive** e ao **Google Colab**;
- Navegador com acesso à internet;
- Dados organizados no Drive conforme a estrutura da seção 4.

Os notebooks foram elaborados para o ambiente Google Colab (Python 3). Não é necessário instalar Python no computador para executá-los no Colab.

## 3. Obter os dados

Para reproduzir os resultados **sem refazer a coleta e o tratamento**, obtenha a pasta de dados preparada para o projeto:

**[BAIXAR/COPIAR PASTA DE DADOS]([https://drive.google.com/drive/folders/1QZWUgnlCn_76y1HlOVkhl3thL-sLxd1R?usp=sharing])**

1. Abra o link e entre com a conta Google autorizada a acessar a pasta.
2. Baixe a pasta ou crie uma cópia dos dados na sua própria conta Google Drive. Se baixar um ZIP, descompacte-o.
3. No seu **Meu Drive**, coloque a pasta com o nome exato `pe-de-meia` (não apenas um atalho para o Drive de outra pessoa).
4. Confirme que as pastas e os nomes dos arquivos internos estão exatamente como descritos abaixo.

### Fontes originais

- **Pé-de-Meia:** [Portal da Transparência — downloads](https://portaldatransparencia.gov.br/download-de-dados/pe-de-meia). A coleta mensal e a agregação por UF estão no notebook `01-coleta-pdm.ipynb`.
- **INEP:** planilhas de **Taxas de Rendimento Escolar por UF**, de 2007 a 2025, conforme utilizadas em `01_coleta_inep.ipynb`. As planilhas originais são arquivos `.xls` por ano.

Os scripts de coleta estão disponíveis no próprio repositório. Como os dados são grandes e os notebooks usam caminhos no Google Drive, a opção mais simples para reproduzir apenas os resultados é usar a pasta disponibilizada acima.

## 4. Estrutura obrigatória no Google Drive

Coloque a pasta `pe-de-meia` diretamente na raiz de **Meu Drive**, de modo que o caminho no Colab seja `/content/drive/MyDrive/pe-de-meia/`.

```text
Meu Drive/
└── pe-de-meia/
    ├── inep/
    │   ├── TAXAS RENDIMENTO UF 2007.xls
    │   ├── TAXAS RENDIMENTO UF 2008.xls
    │   ├── ...
    │   ├── TAXAS RENDIMENTO UF 2025.xls
    │   └── inep-data/
    │       └── taxas_em_uf_2007_2025.csv
    ├── pe-de-meia-data/
    │   ├── 2024/
    │   │   └── [arquivos CSV mensais processados de 2024]
    │   ├── 2025/
    │   │   └── [arquivos CSV mensais processados de 2025]
    │   └── 2026/
    │       └── [arquivos CSV mensais disponíveis de 2026]
    └── agregados/
        ├── pe-de-meia-2024-2026.csv
        ├── pe-de-meia-2024-2026-total-UF.csv
        └── pdm-tx-rendimento-2024-2025.csv
```

Alguns arquivos de saída podem ser produzidos novamente ao executar os notebooks. **Não renomeie as pastas, os arquivos ou `pe-de-meia`**, pois os caminhos no código estão definidos explicitamente. Caso use um nome diferente, deverá alterar os caminhos correspondentes nos notebooks.

## 5. Abrir notebooks no Colab

Você pode abrir cada notebook pelo link correspondente:

- [Coleta — Pé-de-Meia](https://colab.research.google.com/github/lucas-estanislau/pe-de-meia/blob/main/01-coleta-pdm.ipynb)
- [Coleta — INEP](https://colab.research.google.com/github/lucas-estanislau/pe-de-meia/blob/main/01_coleta_inep.ipynb)
- [Agregação das bases](https://colab.research.google.com/github/lucas-estanislau/pe-de-meia/blob/main/02_agrega%C3%A7%C3%A3o.ipynb)
- [Análise exploratória e gráficos](https://colab.research.google.com/github/lucas-estanislau/pe-de-meia/blob/main/03_analise_graficos_atualizados.ipynb)

Se o Colab pedir, escolha **Conectar** para iniciar um ambiente de execução.

## 6. Configurar o ambiente e autorizar o Drive

Autorize o acesso solicitado pelo Google Colab usando **a sua própria conta Google**, na qual você copiou os arquivos. A autorização deve ser feita novamente quando for necessário montar o Drive em uma nova sessão.

Para instalar as bibliotecas no ambiente Colab, execute em uma célula:

```python
!pip install -q pandas numpy requests matplotlib xlrd openpyxl scipy seaborn
```

Se você clonar o repositório na sessão do Colab, também pode usar `!pip install -r requirements.txt` a partir da pasta do repositório. As bibliotecas `google.colab`, `os`, `re`, `zipfile`, `io`, `textwrap` e `unicodedata` **não precisam** constar no `requirements.txt`: as primeiras são próprias do Colab, e as demais fazem parte da biblioteca padrão Python.

## 7. Ordem de execução

### Opção A — Reproduzir a análise com os dados já tratados (mais rápida)

1. Copie integralmente a pasta de dados da seção 3 para o seu Drive, respeitando a estrutura da seção 4.
2. Abra `03_analise_graficos_atualizados.ipynb` no Colab.
3. Instale as dependências (se necessário).
4. No Colab, selecione **Ambiente de execução > Executar tudo** e acompanhe o carregamento das bases e a geração dos gráficos.
5. Se o código apontar para outro caminho, ajuste-o para o local onde os dados foram copiados.

### Opção B — Reexecutar a coleta, o tratamento e a análise

1. Prepare as pastas da seção 4 no seu Drive (incluindo `pe-de-meia-data/2024`, `2025`, `2026`, `inep/inep-data` e `agregados`).
2. Execute `01-coleta-pdm.ipynb` para baixar os dados mensais do Portal da Transparência e gerar os CSVs agregados por UF. Essa etapa pode demorar e depender da disponibilidade do portal.
3. Coloque as planilhas `.xls` do INEP (2007–2025) em `pe-de-meia/inep/` e execute `01_coleta_inep.ipynb`.
4. Execute `02_agregação.ipynb` para consolidar as tabelas e criar a base integrada.
5. Execute `03_analise_graficos_atualizados.ipynb` para reproduzir a análise e os gráficos.

Os notebooks devem ser executados **na sequência de células definida em cada arquivo**, sem depender de variáveis de sessões anteriores. Se algum resultado depender de execução fora de ordem, é necessário ajustar o notebook antes da entrega definitiva.

## 8. Principais variáveis e limitações

- **Pé-de-Meia:** unidade da federação (UF), ano, valor acumulado de pagamentos e quantidade de pagamentos; esta última **não deve ser interpretada automaticamente como número de estudantes beneficiados**.
- **INEP:** ano, UF e taxas de aprovação, reprovação e abandono do ensino médio na rede pública, considerando os recortes utilizados na coleta.
- **Integração:** junção das fontes por `ANO` e `UF`.
- As taxas do INEP abrangem o conjunto de estudantes do recorte adotado, e não apenas os beneficiários do Pé-de-Meia.
- Diferenças entre estados e associações estatísticas não comprovam efeito causal do programa.
- Os dados de 2026 do Pé-de-Meia são parciais no conjunto utilizado; o período de rendimento escolar comparável na análise é 2024–2025.

## 9. Reprodutibilidade

O código de coleta está disponível no repositório, e as fontes externas são identificadas acima. Para reproduzir os mesmos gráficos com a mesma base temporal e os mesmos tratamentos, utilize a cópia dos dados processados fornecida na seção 3. Uma nova coleta pode apresentar resultados diferentes em caso de atualização das fontes.

**Antes da submissão final**, recomenda-se testar cada notebook em uma sessão limpa do Colab usando somente os arquivos e as instruções fornecidos aqui. Este README descreve o procedimento, mas **não representa certificação de que todos os notebooks já foram executados de ponta a ponta sem erros**.
