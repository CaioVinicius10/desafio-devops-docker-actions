# Desafio inicial de DevOps — Docker e GitHub Actions

**Nível:** iniciante  
**Tempo estimado:** 2 a 4 horas

## Objetivo

Executar a página HTML fornecida em um container Docker e criar um workflow no GitHub Actions que construa a imagem e valide automaticamente o funcionamento da aplicação.

## Pré-requisitos

- Conta no GitHub com acesso ao GitHub Actions.
- Git e Docker instalados e funcionando.
- Conhecimentos básicos de terminal, commits, branches e pull requests.

## Aplicação

Crie o arquivo `index.html` com o conteúdo abaixo:

```html
<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Desafio DevOps</title>
  </head>
  <body>
    <h1>Meu primeiro desafio DevOps</h1>
    <p>Docker e GitHub Actions funcionando!</p>
  </body>
</html>
```

## 1. Repositório

Crie um repositório chamado `desafio-devops-docker-actions`, com a branch principal `main`. Desenvolva a solução na branch `feature/desafio-inicial`.

O repositório deve conter:

| Arquivo | Finalidade |
| --- | --- |
| `index.html` | Página da aplicação |
| `Dockerfile` | Construção da imagem Docker |
| `.dockerignore` | Exclusões do contexto de build |
| `.github/workflows/ci.yml` | Workflow de integração contínua |
| `README.md` | Documentação da solução |

## 2. Docker

- Utilize a imagem oficial do Nginx como base, informando uma tag.
- Copie a página HTML para o diretório servido pelo Nginx durante o build.
- Configure o `.dockerignore` para excluir, pelo menos, `.git`, `.github` e `README.md`.
- Construa a imagem com o nome `desafio-devops:v1`.
- Execute um container chamado `desafio-web` em segundo plano.
- Disponibilize a porta `80` do container na porta `8080` do computador, vinculada a `127.0.0.1`.
- Confirme que `http://127.0.0.1:8080` retorna HTTP `200` e contém a mensagem `Meu primeiro desafio DevOps`.
- Consulte os logs, pare e remova o container após a validação local.

## 3. GitHub Actions

Crie o workflow `.github/workflows/ci.yml`, executado em um runner Ubuntu hospedado pelo GitHub, com estes gatilhos:

- Abertura e atualização de pull requests destinados à branch `main`.
- Push na branch `main`.

O workflow deve:

1. Fazer checkout do repositório.
2. Construir a imagem Docker.
3. Iniciar um container com a imagem construída no próprio job, usando o HTML incluído na imagem.
4. Validar por HTTP o status `200` e a presença da mensagem `Meu primeiro desafio DevOps`.
5. Encerrar com falha se o build, a execução ou a validação apresentar erro.
6. Remover o container ao final, inclusive em caso de falha.

## 4. Validação

Abra um pull request da branch `feature/desafio-inicial` para `main` e comprove:

1. Uma execução do workflow com sucesso.
2. Uma execução com falha após alterar temporariamente a mensagem do `<h1>`, mantendo a mensagem esperada no teste.
3. Uma nova execução com sucesso após restaurar a mensagem original.

Deixe o pull request aberto para revisão, com a versão final funcionando.

## 5. Entrega

Envie ao avaliador os links do repositório e do pull request. Se o repositório for privado, conceda acesso ao avaliador.

O `README.md` deve conter:

- Objetivo do projeto e pré-requisitos para execução.
- Comandos para construir a imagem, iniciar o container, consultar os logs, parar e remover o container.
- Endereço de acesso à aplicação.
- Explicação breve dos gatilhos e etapas do workflow.
- Evidência da execução local: captura de tela da página ou saída de uma requisição HTTP.
- Links das execuções do workflow que demonstram sucesso, falha e correção.

## Documentação de apoio

- [Docker: Dockerfile](https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/)
- [Docker: publicação de portas](https://docs.docker.com/get-started/docker-concepts/running-containers/publishing-ports/)
- [GitHub Actions: primeiro workflow](https://docs.github.com/en/actions/get-started/quickstart)
