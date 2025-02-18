# 2D to 3D

## Iniciando o Backend (API)

1. Acesse a pasta `2dTO3d-API` logo acima
2. Entre no arquivo `2dTO3d_API.ipynb`
3. Abra o Colab
![Abrir Colab](/images/open-colab.png)
3. Copie a url da API pra usar no front-end.
![Copiar URL da API](/images/copia-url.png)

## Iniciando a Comunicação com o Front-end

1. Acesse a pasta `2dTO3d` logo acima
2. No arquivo `.env`, substitua o valor da variavel `VITE_API_URL` pela URL da API copiada
3. Instale as dependências necessárias:
   ```sh
   npm i
   ```
4. Inicie a aplicação:

   ```sh
   npm run dev
   ```

5. Abra a aplicação pressionando `Ctrl + Clique` no link exibido no terminal.

## Informações de Usabilidade da Aplicação

1. Selecione o modelo para criar seu objeto 3D:
   - **Tirar uma foto:**
     1. Confirme o envio da foto.
     2. Visualize o objeto gerado.
   - **Enviar um arquivo:**
     1. Selecione o arquivo.
     2. Visualize o objeto gerado.
