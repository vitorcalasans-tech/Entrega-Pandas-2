# 🏛️ Análise de Emendas Parlamentares

## 📌 Sobre o Projeto
Construção de um pipeline de **ETL (Extração, Transformação e Carga)** aplicado a dados públicos do governo brasileiro. Desenvolvido como resolução da Atividade 2 da disciplina de Introdução à Ciência de Dados (Prof. Pedro Mello), o repositório demonstra como receber uma base de dados bruta e entregá-la higienizada, estruturada e pronta para consumo por outras aplicações.

👨‍💻 **Desenvolvido por:** https://github.com/vitorcalasans-tech

## 🎯 O Desafio
Bases de dados reais costumam apresentar inconsistências: valores ausentes, tipos de dados incorretos e informações redundantes. O objetivo principal deste repositório foi utilizar a biblioteca **Pandas** para resolver esses problemas, garantindo a integridade e a qualidade dos dados referentes aos repasses financeiros (emendas) de 2022.

## ⚙️ Arquitetura da Solução (Fluxo de Dados)

# ETAPAS

### 1. 📥 Extração (Extract)
- Leitura otimizada da base bruta em formato `.parquet` (`emendas_tratamento.parquet`), garantindo performance no carregamento de grandes volumes de dados.

### 2. 🧹 Transformação e Limpeza (Transform & Clean)
- **Sanitização de Nulos:** Preenchimento inteligente de lacunas (ex: imputação de `-1` para códigos faltantes e `"Desconhecido"` para nomes de autores em branco).
- **Otimização Estrutural:** Detecção e eliminação de colunas 100% vazias e remoção rigorosa de registros duplicados (validação por *Código da Emenda* e *Município*).
- **Tipagem de Dados (Casting):** Conversão estratégica da coluna `Ano da Emenda` de *Integer* para *String*, garantindo que seja tratada como dado categórico em futuras ferramentas de BI.
- **Padronização de Texto:** Correção de nomenclaturas (ex: "Sem informação" para "Não disponível") e padronização de funções para *UPPERCASE*.

### 3. 📊 Análise e Feature Engineering
- **Criação de Variáveis:** Geração da coluna `Saldo a Pagar` a partir da lógica de negócio (`Valor Empenhado - Valor Pago`).
- **Filtros e Agrupamentos:**
  - Isolamento de dados focados no ano de 2022.
  - Análise de repasses para a Região Norte superiores a R$ 500 mil.
  - Consolidado financeiro por região e cruzamentos comparativos entre RJ e SP.

### 4. 📤 Carga e Exportação (Load)
- Conversão do *DataFrame* final para um formato interoperável.
- Exportação em **JSON** (`emendas_transformadas.json`) utilizando `orient='records'`, formato ideal para APIs, sistemas web e bancos de dados NoSQL.

## 💻 Stack Tecnológica

* **Linguagem:** Python
* **Manipulação de Dados:** Pandas, PyArrow/Fastparquet
* **Ambiente de Desenvolvimento:** Google Colab / Jupyter Notebook
* **Versionamento:** Git, Git Bash, VS Code
