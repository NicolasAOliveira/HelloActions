# ML Pipeline – Workflow Automatizado com GitHub Actions

Este projeto demonstra uma *pipeline de Machine Learning automatizada* utilizando *GitHub Actions*.  
A cada push no repositório, o workflow executa o script train.py, treina um modelo simples de classificação e gera um *relatório de desempenho* com métricas de avaliação salvas em report.txt.

---

##  Estrutura do Projeto

ml-pipeline/
├── data/
│ └── sample.csv # Dataset de exemplo (dados sintéticos)
├── train.py # Script de Machine Learning
├── requirements.txt # Dependências do projeto
└── .github/
└── workflows/
└── ml.yml # Workflow do GitHub Actions

yaml
Copiar código

---

##  Fluxo da Pipeline

### 1. *Disparo do Workflow*
O arquivo .github/workflows/ml.yml é executado automaticamente *a cada push* no repositório.

```yaml
on: [push]
2. Etapas do Workflow
  Passo 1 – Checkout do código
Baixa o código do repositório dentro do runner do GitHub:

yaml
Copiar código
- uses: actions/checkout@v4
Passo 2 – Configurar o ambiente Python
Cria o ambiente com Python 3.11:

yaml
Copiar código
- name: Configurar Python
  uses: actions/setup-python@v5
  with:
    python-version: "3.11"
Passo 3 – Instalar dependências
Instala as bibliotecas listadas em requirements.txt:

yaml
Copiar código
- name: Instalar dependências
  run: pip install -r requirements.txt
Passo 4 – Executar o script de treinamento
Roda o script train.py, que:

Lê os dados de data/sample.csv

Divide o dataset em treino e teste

Treina um modelo de Regressão Logística

Gera o relatório de métricas (acurácia, precisão, recall, F1-score)

yaml
Copiar código
- name: Executar treinamento
  run: python train.py
Passo 5 – Publicar o relatório como artefato
Após a execução, o relatório report.txt é armazenado como artefato do workflow, podendo ser baixado diretamente da aba Actions.

yaml
Copiar código
- name: Upload do relatório
  uses: actions/upload-artifact@v4
  with:
    name: classification-report
    path: report.txt
Saída Esperada
Após o push, o workflow gerará um arquivo report.txt com conteúdo semelhante a:

markdown
Copiar código
              precision    recall  f1-score   support

           0       0.75      1.00      0.86         3
           1       1.00      0.67      0.80         3

    accuracy                           0.83         6
   macro avg       0.88      0.83      0.83         6
weighted avg       0.88      0.83      0.83         6
 Tecnologias Utilizadas
Python 3.11

Pandas → Manipulação de dados

Scikit-learn → Treinamento e avaliação do modelo

GitHub Actions → Automação da pipeline

Como Executar Localmente
Clone o repositório:

bash
Copiar código
git clone https://github.com/SEU_USUARIO/ml-pipeline.git
cd ml-pipeline
Crie um ambiente virtual (opcional):

bash
Copiar código
python -m venv venv
venv\Scripts\activate
Instale as dependências:

bash
Copiar código
pip install -r requirements.txt
Execute o script de treinamento:

bash
Copiar código
python train.py
O relatório report.txt será gerado na raiz do projeto.

  Conceitos Envolvidos
Conceito	Descrição
CI/CD	Integração e Entrega Contínua — automatiza testes e entregas
Workflow	Arquivo YAML que define as etapas de automação
Runner	Máquina virtual onde as ações são executadas
Artefato	Resultado final de um workflow (ex.: relatório, log, binário)

  Referências
Documentação GitHub Actions

Documentação Scikit-learn
oficial de GitHub Actions (Microsoft Learn)
