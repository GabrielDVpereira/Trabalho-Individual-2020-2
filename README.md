
[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=GabrielDVpereira_Trabalho-Individual-2020-2&metric=bugs)](https://sonarcloud.io/dashboard?id=GabrielDVpereira_Trabalho-Individual-2020-2) [![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=GabrielDVpereira_Trabalho-Individual-2020-2&metric=code_smells)](https://sonarcloud.io/dashboard?id=GabrielDVpereira_Trabalho-Individual-2020-2) [![Duplicated Lines (%)](https://sonarcloud.io/api/project_badges/measure?project=GabrielDVpereira_Trabalho-Individual-2020-2&metric=duplicated_lines_density)](https://sonarcloud.io/dashboard?id=GabrielDVpereira_Trabalho-Individual-2020-2) [![Coverage Status](https://coveralls.io/repos/github/GabrielDVpereira/Trabalho-Individual-2020-2/badge.svg?branch=coveralls)](https://coveralls.io/github/GabrielDVpereira/Trabalho-Individual-2020-2?branch=coveralls)


# Trabalho Individual 2020.2 

| Aluno | Matrícula |
|-------| :-------: |
| Gabriel Davi | 170010341 |

## Containerização 

Para ambos os projetos foi criado um dockerfile com as devidas instruções para a construção das imagens que irão executar as aplicações em desenvolvimento: 

- Dockerfile api: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/api/dockerfile)
- Dockerfile client: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/client/dockerfile)

Após a criação de cada dockerfile, foi criado um docker-compose para a devida orquestração dos containers de cada módulo. Além disso, foi adicionado o container de banco de dados utilizando a imagem do postgres:13 mapeado na porta 5432: 

- Docker-compose: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/docker-compose.yaml)

Para dar início à aplicação em execução em ambiente docker, basta entrar na pasta raiz do projeto e executar o comando: 

```sh
docker-compose up --build
```
 O resuldado do comando deve ser o seguinte: 
 
 ![image](https://user-images.githubusercontent.com/37307099/116793729-d7fa6c80-aa9e-11eb-9bde-6da276d68fa0.png)

Obs: Há casos em que a porta 5432 já esteja em uso. Caso isso aconteça, a execução do comando acima irá resultar em um erro para a execução do container para o postgres. Certifique-se que a porta não está em uso através do comando: _sudo lsof -i -P -n | grep LISTEN_ .

## Continous Integration 

Para a integração contínua, foi utilizado o github Actions. Para cada módulo, foi criado um workflow que executa os comandos de linting e testes para cada push em branches do projeto. A branch _master_ foi configurada para aceitar integrações de outras branches somente se todos os jobs configurados nos workflows forem executados com sucesso. A seguir, os arquivos de cada ci: 

- api: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/.github/workflows/ci-api.yaml)
- client: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/.github/workflows/ci-client.yaml)

![image](https://user-images.githubusercontent.com/37307099/116793963-412eaf80-aaa0-11eb-815b-d74f9e437175.png)

![image](https://user-images.githubusercontent.com/37307099/116793980-54417f80-aaa0-11eb-9df5-c40b503395ae.png)

Obs: Para o ci do client, foi criado um step que coleta a cobertura gerado pelos testes e publica no Coveralls 

![image](https://user-images.githubusercontent.com/37307099/116794022-a1bdec80-aaa0-11eb-9421-ac8d1ad78879.png)

## Coleta de métricas de qualidade

Para a coleta de métricas de qualidade, foi configurado para o projeto a utilização da ferramenta [sonarcloud](https://sonarcloud.io/). Com isso, há o monitoramento constante da qualidade do código em produção. Infomações como bugs, code smells e etc são mostrados após cada pull request para certificar a saúde do código a ser integrado. Há também no próprio site do sonarcloud um dashboard para monitoramento da métricas coletadas. 

![image](https://user-images.githubusercontent.com/37307099/116794135-3fb1b700-aaa1-11eb-9112-5be171e56333.png)

![image](https://user-images.githubusercontent.com/37307099/116794146-50fac380-aaa1-11eb-85f1-36655262baf2.png)

## Deploy e Continous Deployment

Ambas as aplicações foram hospedadas no heroku. Seguem os links dos projetos em produção: 
- api: [link](https://trabalho-gces-api.herokuapp.com/task/)
- Client: [link](https://trabalho-gces-client.herokuapp.com/#/)

Para os dois módulos do projeto, foram criados workflows que realizam o deploy automátido para o heroku através das imagens do docker toda vez que é integrado um código na branch principal. Para isso, foi criado em cada projeto um arquivo dockerfile.prod que realiza as devidas configurações necessárias para que o deploy contínuo seja realizado com sucesso. A seguir os links para cada dockerfile e também para os workflows responsávieis pelo Continous Deployment. 

 ### Dockerfiles: 
 
- api: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/api/dockerfile.prod)
- Client: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/client/dockerfile.prod)

 ### Workflows:
 
- api: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/.github/workflows/cd-api.yaml)
- Client: [file](https://github.com/GabrielDVpereira/Trabalho-Individual-2020-2/blob/master/.github/workflows/cd-client.yaml)


## Coveralls

Como já citado na etapa de CI, foi configurado junto aos passos a coleta de cobertura de testes e sua publicação no coveralls, essa informação também é mostrada junto a outros checks durante a abertura de um pull resquest

![image](https://user-images.githubusercontent.com/37307099/116794430-2e69aa00-aaa3-11eb-97fe-d13b79f8cc17.png)


