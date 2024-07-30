# Instalação do FastAPI e suas Dependências (Ambiente Linux)

## 1. Instalar o Python

Antes de instalar o FastAPI, você precisa ter o Python 3.7 ou superior instalado no seu sistema. Se ainda não o tiver, siga estas etapas:

  1. Abra o terminal.
  2. Instale o Python usando o gerenciador de pacotes da sua distribuição. Por exemplo, no Ubuntu, use:

     ```bash
     sudo apt update
     sudo apt install python3 python3-pip
     ```

## 2. Criar um Ambiente Virtual

É uma boa prática usar um ambiente virtual para gerenciar dependências de projetos Python. Isso ajuda a isolar as bibliotecas do projeto das instaladas globalmente.

1. **Crie um ambiente virtual:**

   ```bash
   python -m venv venv
   ```

Isso criará uma pasta chamada venv no diretório atual, contendo o ambiente virtual.

2. **Ative o ambiente virtual:**

   ```bash
   source venv/bin/activate
   ```

## 3. **Instalar o FastAPI e Uvicorn:**

Com o ambiente virtual ativado, instale o FastAPI e Uvicorn, que é um servidor ASGI recomendado para executar aplicações FastAPI.


1. **Instale FastAPI e Uvicorn:**

   ```bash
   pip install fastapi uvicorn
   ```

    - FastAPI: A framework para construir APIs.
    - Uvicorn: O servidor ASGI para executar a aplicação FastAPI.