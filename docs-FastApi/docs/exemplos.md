
# Criar e Executar uma Aplicação FastAPI

Agora que você instalou o FastAPI e o Uvicorn, vamos criar uma aplicação mais robusta. Esta aplicação incluirá endpoints para operações CRUD (Create, Read, Update, Delete) e usará Pydantic para validação de dados.

## 1. Crie um arquivo main.py com o seguinte conteúdo:

Crie um arquivo chamado `main.py` e adicione o seguinte conteúdo:

```python
from typing import List, Optional

from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

# Modelo de dados
class Item(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    tax: Optional[float] = None

# Simulando um banco de dados em memória
fake_items_db = {}

@app.post("/items/", response_model=Item)
def create_item(item: Item):
    item_id = len(fake_items_db) + 1
    fake_items_db[item_id] = item
    return item

@app.get("/items/", response_model=List[Item])
def read_items():
    return list(fake_items_db.values())

@app.get("/items/{item_id}", response_model=Item)
def read_item(item_id: int):
    item = fake_items_db.get(item_id)
    if item is None:
        raise HTTPException(status_code=404, detail="Item not found")
    return item

@app.put("/items/{item_id}", response_model=Item)
def update_item(item_id: int, item: Item):
    if item_id not in fake_items_db:
        raise HTTPException(status_code=404, detail="Item not found")
    fake_items_db[item_id] = item
    return item

@app.delete("/items/{item_id}", response_model=dict)
def delete_item(item_id: int):
    if item_id not in fake_items_db:
        raise HTTPException(status_code=404, detail="Item not found")
    del fake_items_db[item_id]
    return {"message": "Item deleted successfully"}
```

## 2. Executar a Aplicação FastAPI

No terminal, navegue até o diretório onde o arquivo main.py está localizado e execute o seguinte comando para iniciar o servidor:

```bash
    uvicorn main:app --reload

```

Isso iniciará o servidor Uvicorn e a aplicação FastAPI estará disponível em http://127.0.0.1:8000.

## 3. Testar a Aplicação

Você pode testar a aplicação usando o Swagger UI e ReDoc, que são automaticamente gerados pelo FastAPI:

- Swagger UI: Acesse http://127.0.0.1:8000/docs para ver a documentação interativa da API e testar os endpoints diretamente do navegador.
- ReDoc: Acesse http://127.0.0.1:8000/redoc para uma documentação alternativa e detalhada.

### Exemplos de testes

1. Criar um Item:

    - Método: POST
    - URL: http://127.0.0.1:8000/items/
    - Corpo da Requisição:
    ```json
    {
        "name": "Item1",
        "description": "Descrição do Item1",
        "price": 25.50,
        "tax": 2.50
    }
    ```

2. Ler Itens:

    - Método: GET
    - URL: http://127.0.0.1:8000/items/

3. Ler um Item Específico:

    - Método: GET
    - URL: http://127.0.0.1:8000/items/1

4. Atualizar um Item:

    - Método: PUT
    - URL: http://127.0.0.1:8000/items/1
    - Corpo da Requisição:
    ```json
    {
        "name": "Item1 Atualizado",
        "description": "Descrição atualizada",
        "price": 30.00,
        "tax": 3.00
    }
    ```

5. Excluir um Item:

    - Método: DELETE
    - URL: http://127.0.0.1:8000/items/1