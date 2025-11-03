# Gerador de Dados Sintéticos - Varejo Amana Beauty Lab

Este projeto é um script Python, idealmente executado em um notebook (Google Colab, Jupyter), projetado para gerar um conjunto completo de dados sintéticos (massa de dados) para a **Amana Beauty Lab**, uma empresa fictícia de varejo de cosméticos.

O objetivo é criar um dataset coeso, realista e interconectado, simulando as operações de vendas, estoque e clientes de uma rede de lojas e um e-commerce. O dataset gerado é perfeitamente adequado para projetos de Data Science, Business Intelligence e Engenharia de Dados.

## 🎯 Contexto de Negócio e Funcionalidades

Este gerador vai além de simplesmente criar dados aleatórios. Ele incorpora regras de negócio complexas para garantir que os dados façam sentido e possam ser usados para análises avançadas:

* **Perfis de Filiais:** As lojas são divididas em "Alto Padrão", "Médio Padrão" e "Baixo Padrão", além de um canal de "ECOMMERCE". O perfil da loja influencia os produtos que ela mais vende.
* **Perfis de Clientes:** Os clientes são classificados em perfis comportamentais (ex: `Premium`, `Custo-Benefício`, `Caçador de Ofertas`) que ditam sua afinidade por produtos e descontos.
* **Sazonalidade de Vendas:** O volume de transações aumenta significativamente em datas comemorativas importantes para o varejo (Natal, Black Friday, Dia das Mães, etc.).
* **Mix de Produtos Realista:** A geração de produtos segue proporções de mercado (ex: mais sabonetes do que perfumes) e uma divisão de tiers (30% Alto Padrão, 70% Médio Padrão).
* **Lógica de Preços e Descontos:** Os preços são calculados com base em `CUSTO`, `LUCRO`, `IMPOSTOS` e `DESCONTOS`. Os descontos são aplicados de forma inteligente, sendo mais frequentes na Black Friday e para clientes "Caçadores de Ofertas".

## 🚀 Como Executar (Google Colab)

1.  **Abrir no Colab:** Clique no emblema "Open in Colab" acima (depois de configurar seu link).
2.  **Montar o Google Drive:** Execute a primeira célula (**Passo 0**) para instalar o `Faker` e montar seu Google Drive. Você precisará autenticar sua conta para permitir que o Colab salve os arquivos.
3.  **Configurar Parâmetros:** Antes de executar a geração de vendas (**Passo 5**), ajuste as seguintes variáveis no bloco de chamada:
    * `DRIVE_PATH`: A pasta no seu Google Drive onde os arquivos `.csv` serão salvos (ex: `/content/drive/MyDrive/amana_beauty_lab`).
    * `PARAM_NUM_NOTAS`: O número de notas fiscais (transações) que você deseja gerar (ex: `150000`).
    * `PARAM_DATA_INICIO`: A data de início do período de vendas (ex: `datetime(2022, 1, 1)`).
    * `PARAM_DATA_FIM`: A data de fim do período de vendas (ex: `datetime(2026, 1, 1)`).
4.  **Executar Tudo:** No menu "Ambiente de execução", selecione "Executar tudo".
5.  **Verificar Saída:** Após a execução (que pode levar alguns minutos, especialmente no Passo 5), verifique a pasta `DRIVE_PATH` no seu Google Drive. Os cinco arquivos `.csv` estarão lá.

## 🗂️ Esquema de Dados (Arquivos Gerados)

O script gera e salva os cinco arquivos `.csv` a seguir:

### 1. `produtos.csv`
Catálogo de todos os produtos (SKUs) vendidos pela Amana Beauty Lab.
* `COD_EAN`: (Chave Primária) Código EAN único do produto (13 dígitos).
* `NOME_PRODUTO`: Nome comercial do produto (ex: "Sérum Poranga de Açaí").
* `DESCR_PRODUTO`: Descrição (ex: "250ml", "90g").
* `CATEGORIA`: Categoria principal (ex: "Shampoo", "Perfume").
* `TIER`: Perfil do produto (Alto Padrão / Médio Padrão).
* `CUSTO_PRODUTO`: Custo de produção.
* `LUCRO_MINIMO`: Margem mínima (100% do custo).
* `LUCRO_MAXIMO`: Margem máxima (200% do custo).
* `VALOR_LIQUIDO`: Preço de venda de lista (Custo + Lucro).
* `IMPOSTOS`: Imposto de 20% sobre o `VALOR_LIQUIDO`.
* `VALOR_BRUTO`: Preço de venda de lista bruto (`VALOR_LIQUIDO` + `IMPOSTOS`).

### 2. `filiais.csv`
Lista de todas as lojas físicas e o canal de e-commerce.
* `COD_FILIAL`: (Chave Primária) Código identificador da filial (ex: "LOJA_001", "ECOM_001").
* `NOME_FILIAL`: Nome da loja (ex: "Amana Lab - Shopping Iguatemi").
* `PERFIL`: Perfil da loja (Alto Padrão / Médio Padrão / Baixo Padrão / ECOMMERCE).

### 3. `clientes.csv`
Base de clientes que realizam compras.
* `COD_CLIENTE`: (Chave Primária) Código identificador do cliente (ex: "CLI_00001").
* `NOME_CLIENTE`: Nome do cliente.
* `SOBRENOME_CLIENTE`: Sobrenome do cliente.
* `PERFIL_COMPRA`: Perfil comportamental (Premium / Custo-Benefício / Ocasional / Caçador de Ofertas).

### 4. `estoque.csv`
Um snapshot (foto) do estoque em uma data específica para fins de análise de abastecimento.
* `COD_FILIAL`: (Chave Estrangeira de `filiais.csv`)
* `EAN`: (Chave Estrangeira de `produtos.csv`)
* `ESTOQUE_MINIMO`: Nível mínimo de estoque.
* `ESTOQUE_MAXIMO`: Nível máximo de estoque.
* `ESTOQUE_ATUAL`: Quantidade em estoque na data da foto.
* `DATA_FOTO_ESTOQUE`: Data em que o snapshot foi tirado.

### 5. `vendas.csv`
Tabela transacional (Fato Vendas). Cada linha representa um item de uma nota fiscal.
* `NUM_NOTA`: Número da nota fiscal (agrupa itens da mesma compra).
* `SERIE_NOTA`: Série da nota.
* `DATA_NOTA`: Data da transação.
* `COD_FILIAL`: (Chave Estrangeira de `filiais.csv`) Onde a venda ocorreu.
* `COD_CLIENTE`: (Chave Estrangeira de `clientes.csv`) Quem comprou.
* `COD_EAN`: (Chave Estrangeira de `produtos.csv`) O que foi comprado.
* `QUANTIDADE`: Quantidade vendida do item.
* `VALOR_LIQUIDO_lista`: Preço unitário de tabela do produto (pré-desconto).
* `DESCONTO`: Valor monetário total do desconto aplicado na linha.
* `VALOR_LIQUIDO`: Valor total da linha (preço final * quantidade, pós-desconto, antes de impostos).
* `IMPOSTOS`: Valor total dos impostos sobre a linha.
* `VALOR_BRUTO`: Valor total final da linha (`VALOR_LIQUIDO` + `IMPOSTOS`).

## 📊 Casos de Uso para Análise

Este conjunto de dados foi projetado para permitir uma ampla gama de projetos de Data Science e BI, incluindo:

1.  **Segmentação de Clientes:** Análise **RFV (Recência, Frequência, Valor)** para identificar os clientes mais valiosos.
2.  **Previsão de Demanda:** Modelos de *Time Series* (SARIMAX, Prophet, LSTM) para prever vendas por loja, categoria ou produto, levando em conta a sazonalidade.
3.  **Sistemas de Recomendação:** Análise de Cesta de Compras (*Market Basket Analysis*) para encontrar padrões (ex: "Quem compra Produto A também compra Produto B").
4.  **Otimização de Estoque:** Análise de previsão para calcular o estoque de segurança ideal e evitar rupturas.
5.  **Análise de Elasticidade de Preço:** Entender como os descontos afetam o volume de vendas e a receita.
6.  **Dashboards de BI:** Criação de painéis no Looker Studio, Power BI ou Tableau para monitorar KPIs de vendas, margem e desempenho das filiais.

## 📄 Licença

Distribuído sob a licença MIT. Veja o arquivo `LICENSE` para mais informações.
