# API na prática

Repositório companheiro do curso **Testes de API na prática: do contrato à regressão no pipeline**, da Avant QA's.

Aqui ficam a coleção do Postman, os ambientes e, mais adiante, os schemas e o pipeline que o curso constrói aula a aula.

## O que você precisa

- **Node.js** (versão LTS) para rodar a API do laboratório: <https://nodejs.org>
- **Postman** (aplicativo desktop): <https://www.postman.com/downloads/>

Não é preciso saber programar.

## A API do laboratório: ServeRest

O curso usa a [ServeRest](https://github.com/ServeRest/ServeRest), uma API REST gratuita feita para estudo de testes. Ela tem usuários, login com token, produtos e carrinhos.

Para subir a API no seu computador:

```bash
npx serverest@latest
```

A API sobe em `http://localhost:3000`. Para conferir, abra `http://localhost:3000/usuarios` no navegador.

O curso foi gravado com a **versão 3.2.2**. Se algo estiver diferente na sua máquina, rode a mesma versão:

```bash
npx serverest@3.2.2
```

Opções úteis (`npx serverest --help` mostra todas):

| Opção | O que faz |
|---|---|
| `--porta 3500` | usa outra porta |
| `--timeout 3600` | token de login dura 1 hora (o padrão é 600 segundos) |
| `--nodoc` | não abre a documentação sozinha |

Os dados ficam só enquanto a API está rodando. Parou e subiu de novo, volta ao estado inicial.

## Como importar no Postman

1. No Postman, clique em **Import**.
2. Selecione `collections/api-na-pratica.postman_collection.json`.
3. Importe também os dois arquivos da pasta `environments/`.
4. No canto superior direito, escolha o ambiente **API na prática — local**.
5. Com a ServeRest rodando, abra a pasta **Aula 03 — Laboratório** e envie as requisições.

## Estrutura

```text
collections/    coleção do Postman, com uma pasta por aula
environments/   ambientes: local (sua máquina) e online (serverest.dev)
data/           tabelas de casos do data-driven (CSV e JSON)
```

Para rodar uma pasta com tabela de casos:

```bash
npx newman run collections/api-na-pratica.postman_collection.json   -e environments/local.postman_environment.json   --folder "Aula 15 — Data-driven" -d data/usuarios-cadastro.csv
```

## Ambientes

| Ambiente | baseUrl | Quando usar |
|---|---|---|
| API na prática — local | `http://localhost:3000` | sempre que possível: é seu, dá para apagar e recomeçar |
| API na prática — online | `https://serverest.dev` | só para consultas rápidas, sem instalar nada |

A versão online é compartilhada por todo mundo. Não cadastre dados reais e não use essa versão para testes destrutivos.

## Rodando pela linha de comando (Newman)

Com a ServeRest no ar:

```bash
npx newman run collections/api-na-pratica.postman_collection.json -e environments/local.postman_environment.json
```

A partir da Aula 22 o curso usa isso no dia a dia; aqui já serve para conferir se está tudo certo.

## Andamento

| Aula | O que entra no repositório |
|---|---|
| 03 — Montando o laboratório | coleção inicial, ambientes local e online |
| 10 — Token dinâmico | login que guarda o token, autorização no nível da coleção e login automático antes de cada requisição |
| 11 — Asserções | asserção frágil × forte, e verificações de status, corpo, cabeçalho e tempo |
| 12 — Contrato (JSON Schema) | schema do login e da listagem, com tipos, obrigatórios e campo a mais barrado |
| 13 — Fluxo encadeado e estado | o ciclo criar, consultar, editar, apagar e conferir, com o id passando entre as requisições e limpeza no fim |
| 14 — Dados dinâmicos | dado único por execução, a armadilha do mesmo gerador escrito duas vezes e a receita prefixo + carimbo + aleatório |
| 15 — Data-driven | uma requisição e um arquivo de casos (`data/`), com o esperado em cada linha |

As próximas aulas acrescentam pastas na coleção, schemas e o workflow do GitHub Actions.
