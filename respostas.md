# Respostas · Avaliação Prática de Docker · ViaSerra Transportes (Turma C)

Nome: Yasmin Alencar da Silva
Matrícula: 26174744
Usuário do GitHub: YasminAlencarSilva
Usuário do Docker Hub: yasminalencar

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?
Imagem base: `nginx:1.27-alpine`.  
Tamanho final da imagem: `73.6 MB`.
2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.
O Nginx procura os arquivos do site em `/usr/share/nginx/html`.
Comando utilizado:docker exec avaliacao-docker-viaserra-portal-1 sh -c "grep -n '26174744' /usr/share/nginx/html/index.html"

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.
Imagem: yasminalencar/viaserra-portal:1.0-26174744

Link: https://hub.docker.com/r/yasminalencar/viaserra-portal
4. Se você mudar o HTML, quais comandos precisa rodar para que a versão nova chegue ao Docker Hub?
docker build -t yasminalencar/viaserra-portal:1.0-26174744 ./portal
docker push yasminalencar/viaserra-portal:1.0-26174744
## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução                  | O que estava errado                                                 | O que você viu acontecer                                  | Como corrigiu                                      |
| - | -------------------------- | ------------------------------------------------------------------- | --------------------------------------------------------- | -------------------------------------------------- |
| 1 | `COPY pagina/ .`           | A pasta `pagina/` não existia; o site estava em `site/`.            | O `docker build` falhou com `"/pagina": not found`.       | Alterei para `COPY site/ .`.                       |
| 2 | `WORKDIR /usr/share/nginx` | O diretório de trabalho não era o diretório de publicação do Nginx. | O container iniciava, mas encerrava com `Exited (0)`.     | Alterei para `WORKDIR /usr/share/nginx/html`.      |
| 3 | `CMD ["nginx"]`            | O Nginx não estava sendo mantido em primeiro plano no container.    | O container iniciava e depois aparecia como `Exited (0)`. | Alterei para `CMD ["nginx", "-g", "daemon off;"]`. |



6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

-p 7042:80 publica a porta 80 do container na porta 7042 do host. Já -p 80:7042 publica a porta 7042 do container na porta 80 do host. Portanto, o número da direita é a porta do container.

## Parte 4 · Primeiro docker-compose

7. Escreva os dois comandos `docker run` que fariam o mesmo que o seu `docker-compose.yml`.

docker run -d --name portal -p 8044:80 --restart unless-stopped yasminalencar/viaserra-portal:1.0-27174744

docker run -d --name manutencao -p 7044:80 --restart unless-stopped avaliacao-docker-viaserra-manutencao

8. Qual comando derruba os dois containers de uma vez?

docker compose down

## Verificador

9. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```
