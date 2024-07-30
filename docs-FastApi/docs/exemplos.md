
# Exemplos Práticos

## Criando uma API Simples

Vamos criar uma API simples que retorna uma mensagem de boas-vindas.

### Arquivo `main.py`

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Bem-vindo à FastAPI!"}
