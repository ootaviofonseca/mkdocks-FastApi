# Melhores Práticas e Dicas

## Estrutura de Projeto

Organize seu projeto utilizando uma estrutura de pastas clara. Uma estrutura recomendada pode incluir:

- **`app/`**: Contém o código principal da aplicação.
  - **`main.py`**: Arquivo principal onde a aplicação FastAPI é criada.
  - **`routers/`**: Contém os módulos de roteamento.
  - **`models/`**: Contém os modelos de dados.
  - **`schemas/`**: Contém os esquemas de validação (usando Pydantic).
  - **`services/`**: Contém a lógica de negócios.
- **`tests/`**: Contém os testes da aplicação.
- **`requirements.txt`** ou **`pyproject.toml`**: Gerencia as dependências do projeto.

## Uso de Dependências

Utilize as dependências do FastAPI para simplificar e organizar a lógica comum, como autenticação, conexão com banco de dados e validação. Defina dependências em funções de endpoint e use o sistema de injeção de dependências para manter o código modular e reutilizável.

## Tratamento de Erros

Implemente tratamento de erros adequado para fornecer feedback claro e útil aos usuários da API. Use a exceção `HTTPException` para retornar códigos de status HTTP apropriados e mensagens de erro. Exemplo:

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

@app.get("/items/{item_id}")
def read_item(item_id: int):
    if item_id not in fake_items_db:
        raise HTTPException(status_code=404, detail="Item not found")
    return fake_items_db[item_id]
