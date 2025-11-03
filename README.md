# Laboratório de Data Science Aplicada ao Varejo

![Badge de Status](https://img.shields.io/badge/status-em_desenvolvimento-green)
![Badge de Licença](https://img.shields.io/badge/license-MIT-blue)

## 🎯 Propósito do Repositório

Bem-vindo ao Laboratório de Data Science Aplicada! Este repositório serve como um ambiente de estudo e experimentação (*sandbox*) focado na aplicação prática de técnicas de análise de dados, estatística e *machine learning* em um contexto de negócios realista.

O objetivo é construir um portfólio de projetos que demonstrem soluções para problemas de negócio comuns, indo desde a estatística descritiva básica até modelos sofisticados de *deep learning* e previsão.

## 💡 O Conceito: Um Varejo Fictício

Para conectar todos os estudos de caso e garantir um conjunto de dados rico e coeso, todo o repositório é baseado em um universo de dados de uma **empresa de varejo fictícia (Amana Beauty Lab)**.

Isso nos permite simular problemas de negócio reais e construir soluções analíticas ponta-a-ponta, desde a geração dos dados (nosso ponto de partida) até a clusterização de clientes, sistemas de recomendação, previsão de demanda e otimização de estoque.

## 🧪 Casos de Estudo e Projetos

Este laboratório é organizado em diretórios, onde cada um representa um projeto ou caso de estudo específico.

---

### 1. Geração de Massa de Dados (O Ponto de Partida)

Antes de qualquer análise, precisamos de dados. Este projeto detalha a criação de um ecossistema de dados sintéticos completo — simulando produtos, clientes, filiais, vendas sazonais e estoque — que servirá de base para todas as análises futuras no repositório.

* **Descrição:** Script Python para gerar um dataset realista, com regras de negócio, perfis de clientes e sazonalidade.
* **Tecnologias:** Python, Pandas, Numpy, Faker, Google Colab.
* **O que você encontra lá:** O código-fonte comentado passo a passo e um `README.md` detalhado do módulo.

> **[➡️ Acesse o README do projeto de Geração de Massa de Dados](./GeracaoMassaDados/README.md)**

---

### 2. Análise RFV e Clusterização de Clientes (Em Breve)
* **Descrição:** Aplicação do modelo RFV (Recência, Frequência, Valor) e técnicas de clusterização (K-Means) para segmentar nossa base de clientes.
* **Objetivo:** Identificar clientes "Premium", "Em Risco", "Fiéis", etc.

### 3. Previsão de Demanda (Time Series) (Em Breve)
* **Descrição:** Utilização de modelos de séries temporais (SARIMAX, Prophet) para prever o volume de vendas futuro, levando em conta a forte sazonalidade do varejo.
* **Objetivo:** Otimizar estoque e planejamento.

*(...outros casos de estudo serão adicionados aqui...)*

## 🛠️ Stack Tecnológico Principal

Este laboratório utiliza primariamente o ecossistema Python para análise de dados. As principais ferramentas incluem:

* **Python 3.x**
* **Google Colab / Jupyter Notebooks** (para experimentação e prototipagem)
* **Pandas** (para manipulação e análise de dados)
* **Numpy** (para operações numéricas)
* **Scikit-learn** (para modelos de machine learning)
* **Matplotlib / Seaborn / Plotly** (para visualização de dados)
* **Faker** (para geração de dados fictícios)

## 🚀 Como Utilizar este Repositório

1.  **Clone o repositório:**
    ```bash
    git clone [URL_DO_SEU_REPOSITORIO_AQUI]
    ```
2.  **Comece pelo Começo:** Navegue até o diretório `GeracaoMassaDados/` e siga as instruções do `README.md` local para gerar seu próprio conjunto de dados.
3.  **Explore os Casos:** Após gerar os dados, explore os outros diretórios de projetos para ver as análises em ação.

## 📄 Licença

Este projeto é distribuído sob a licença MIT. Veja o arquivo `LICENSE` para mais informações.
