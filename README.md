# [fimtab.shop](http://fimtab.shop/)

O [Fimtab](https://fimtab.shop/) é um _clone_ de um projeto do [tabnews](https://wwww.tabnews.com.br) na comunidade da área de tecnologia, destinado a debates e troca de conhecimentos por meio de publicações e comentários criados pelos próprios usuários.

**Conteúdo**

- [fimtab.shop](#fimtabshop)
  - [Instalar e rodar o projeto](#instalar-e-rodar-o-projeto)
    - [Dependências globais](#dependências-globais)
    - [Dependências locais](#dependências-locais)
    - [Rodar o projeto](#rodar-o-projeto)
  - [Rodar os testes](#rodar-os-testes)

## Instalar e rodar o projeto

Rodar o TabNews em sua máquina local é uma tarefa extremamente simples.

### Dependências globais

Você precisa ter duas principais dependências instaladas:

- Node.js LTS v20 (ou qualquer versão superior)
- Docker Engine v17.12.0 com Docker Compose v1.29.2 (ou qualquer versão superior)

### Dependências locais

Com o repositório clonado e as dependências globais instaladas, você pode instalar as dependências locais do projeto:

```bash
npm install
```

### Rodar o projeto

Para rodar o projeto localmente, basta executar o comando abaixo:

```bash
npm run dev
```

Isto irá automaticamente rodar serviços como Banco de dados (incluindo as Migrations), Servidor de Email e irá expor um Serviço Web (Frontend e API) no seguinte endereço:

```bash
http://localhost:3000/
http://localhost:3000/api/v1/status
```

Observações:

- Para derrubar todos os serviços, basta utilizar as teclas `CTRL+C`, que é o padrão dos terminais para matar processos.
- Você pode conferir o endereço dos outros serviços dentro do arquivo `.env` encontrado na raiz do projeto, como por exemplo o endereço e credenciais do Banco de Dados local ou o Frontend do Serviço de Email.

## Rodar os testes

Há várias formas de rodar os testes dependendo do que você deseja fazer, mas o primeiro passo antes de fazer qualquer alteração no projeto é rodar os testes de forma geral para se certificar que tudo está passando como esperado. O comando abaixo irá rodar todos os serviços necessários, rodar os testes e em seguida derrubar todos os serviços.

```bash
npm test
```

Caso queira manter os serviços e testes rodando enquanto desenvolve (e rodando novamente a cada alteração salva), use o modo `watch` com o comando abaixo:

```bash
npm run test:watch:services
```

Os logs do Serviço Web e Vitest (dos testes) irão se misturar, então caso queira rodar eles de forma separada, abra dois terminais separados e rode o seguinte:

```bash
# Terminal 1
npm run dev

# Terminal 2
npm run test:watch
```

Caso não queira executar (ou dar `watch`) em todos os testes e queira isolar arquivos específicos de teste, você pode filtrar pelo caminho. Não é necessário digitar o caminho inteiro para o arquivo e você também pode fornecer mais de um caminho, veja alguns exemplos abaixo:

```bash
# Rodar todos os testes de "users" e "status" da api "v1"
npm run test -- v1/users/ v1/status/

# Rodar apenas o arquivo tests/integration/api/v1/_use-cases/registration-flow.test.js
npm run test -- registration-flow

# Rodar apenas o arquivo tests/integration/api/v1/contents/[username]/patch.test.js
npm run test:watch:services -- username]/patch

# Rodar apenas o arquivo tests/integration/api/v1/contents/[username]/[slug]/get.test.js
npm run test:watch -- contents/[username]/[slug]/get
```

Observações:

- A forma como é tratado o caminho dos arquivos pode mudar dependendo do seu sistema operacional.
- A forma como o seu terminal interpreta caracteres especiais como `/` ou `[` pode mudar.
