# Tech Challenge Fase 3 - Atrasos de Voos (EUA)

Este repositório contém a solução consolidada para o Tech Challenge da Fase 3, cujo foco é construir um pipeline de Machine Learning para prever atrasos de voos nos EUA e identificar perfis de aeroportos usando aprendizado não supervisionado.

O processo de exploração de dados, limpeza, engenharia de features e modelagem foi todo organizado em um único notebook principal.

**Nota sobre os dados:**
Os dados originais (em formato `.csv`) são muito grandes (`airlines.csv`, `airports.csv`, `flights.csv`) e, portanto, **não estão versionados** neste repositório. O link para download ou acesso a eles estará [aqui](https://drive.google.com/drive/folders/1aS7exW5N0qq1uIxvIBcAfc18OHojOMjj). Para rodar este projeto localmente, você deve baixá-os e colocá-los na pasta `data/` na raiz do projeto.

---

## Requisitos

- Python 3.14 (recomendado)
- pip (gerenciador de pacotes)
- ambiente virtual opcional (venv, virtualenv, conda)

## Como rodar o projeto

1. **Clone o repositório**
2. Vá para a raiz do repositório
3. **Crie e ative um ambiente virtual** (recomendado)

   ```bash
   python -m venv .venv
   source .venv/bin/activate      # linux/mac
   .venv\Scripts\activate       # windows
   ```

4. **Instale as dependências**

   ```bash
   pip install -r requirements.txt
   ```

5. **Baixe os dados**, coloque-os em uma pasta `data/`
6. **Rode o notebook principal**

   ```bash
   jupyter notebook pipeline_completo.ipynb
   ```

## Arquitetura da Solução

O arquivo central e foco de avaliação desta entrega é o **`pipeline_completo.ipynb`**. Nele as etapas do estudo foram desenvolvidas na seguinte ordem:

1. **Carga e Setup:** Bibliotecas e leitura da base a partir de `/data/`.

2. **Preparo Inicial e Seleção de Features:** Tratamento de nulos, união de datasets, casting de tipos.

3. **Exploração de Dados (EDA):** Entendimento de distribuições (tempos de atraso, frequências de voo, impacto de companhias aéreas e aeroportos).

4. **Modelagem Supervisionada (Classificação):**
   - Previsão de status de atraso através de XGBoost.
   - Avaliação com métricas adequadas a dados desbalanceados: accuracy, precision, recall e F1.

5. **Modelagem Não Supervisionada:**
   - Clusterização (K-Means) aliada a redução de dimensionalidade (PCA) para definir os perfis atuantes dos aeroportos na base.

## Principais Resultados

- **Modelagem Supervisionada**: O modelo **XGBoost** foi usado para predição de atrasos (> 0 minutos), com avaliação em accuracy, precision, recall, F1 e matriz de confusão.
- **Limitações Evidenciadas**: Apenas variáveis de agendamento (aeroporto, companhia, horário previsto) impõem um limite preditivo. Fatores essenciais da vida real, como condições climáticas e problemas de manutenção, se mostraram faltantes para explicar a totalidade da variância dos atrasos.
- **Modelagem Não Supervisionada**: A combinação de **K-Means e PCA** conseguiu dividir os aeroportos da base em **3 perfis operacionais/clusters** distintos, com as duas componentes principais retendo mais de 83% da variância explicada.
