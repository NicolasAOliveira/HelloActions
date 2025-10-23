
## Funcionalidades

- **Workflow Automatizado**: Executa a cada push no repositório
- **Treinamento de Modelo**: Usa Regressão Logística para classificação
- **Geração de Relatório**: Cria relatório com métricas de avaliação
- **Artefatos**: Salva o relatório como artefato no GitHub

## Como usar

1. Faça push do código para o repositório
2. O workflow será executado automaticamente
3. Verifique a aba "Actions" no GitHub
4. Baixe o relatório na seção de artefatos

## Métricas Incluídas

- Acurácia
- Precisão
- Recall
- F1-Score
'''
    
    with open('ml-pipeline/README.md', 'w') as f:
        f.write(readme_content)
    
    # 5. Criar sample data
    np.random.seed(42)
    n_samples = 200
    X = np.random.randn(n_samples, 4)
    y = (X[:, 0] + X[:, 1] * 0.5 - X[:, 2] * 0.3 + np.random.randn(n_samples) * 0.1) > 0
    y = y.astype(int)
    
    df = pd.DataFrame(X, columns=[f'feature_{i}' for i in range(4)])
    df['target'] = y
    df.to_csv('ml-pipeline/data/sample.csv', index=False)
    
    # Criar arquivo ZIP
    with zipfile.ZipFile('ml-pipeline.zip', 'w', zipfile.ZIP_DEFLATED) as zipf:
        for root, dirs, files in os.walk('ml-pipeline'):
            for file in files:
                file_path = os.path.join(root, file)
                arcname = file_path
                zipf.write(file_path, arcname)
    
    print("Arquivo ml-pipeline.zip criado com sucesso!")
    
    # Limpar diretórios temporários
    import shutil
    shutil.rmtree('ml-pipeline')

if __name__ == "__main__":
    create_ml_pipeline_zip()
