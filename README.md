# Challenge DevOps

## Desafio

Considerando as aplicações presentes neste repositório detalhadas abaixo, precisamos de uma stack que permita a comunicação entre ambas e o acesso de desenvolvedores.

* **Aplicação Frontend** - Aplicação em Python com Flask expondo na porta 8000 um formulário de criação de usuário contendo os campos ID e Name que realiza uma chamada Post com tais dados para a aplicação Backend.

* **Aplicação Backend** - Aplicação em Go (Golang) expondo na porta 8080 o CRUD de Usuários e armazena em um banco Sqlite3 local.

## Como entregar sua solução?

1) Clone do repositório

2) Realize as alterações necessárias para construção/automação da stack. Considere um ambiente local (máquina do desenvolvedor) ou algum provedor de cloud (AWS ou GCP).

3) Adicione e commit todos os arquivos criados/alterados (todos mesmo)

4) Gere um patch conforme comando de exemplo abaixo

5) Nos envie o patch através do email que entramos em contato

*Para gerar o patch:*
```
git format-patch origin/master --stdout > seu_nome.patch
```
## Requisitos

* Crie imagens Docker para ambas as aplicações. 
* Preencher este arquivo README.md com os detalhes, linha de raciocínio e dicas para os desenvolvedores que utilizarão sua solução.
* Considere que os desenvolvedores estão iniciando carreira e precisarão de mais detalhes de como executar sua solução.
* A Stack pode usar os recursos do próprio desenvolvedor(ex. VirtualBox, Docker, Docker-Compose) ou recursos de um provedor de cloud (Amazon Web Service ou Google Cloud)
* Não é necessário a criação de um pipeline. Considere que sua solução fará o bootstrap da Stack em questão.
* Não se preocupe em montar uma solução complexa. Dê preferência em montar uma solução simples que permita que o desenvolvedor realize melhorias.
* Apresente um desenho macro de arquitetura de sua solução.

## Bonus

* Sinta-se a vontade para realizar melhorias no código das aplicações, caso julgue necessário.

## Dúvidas

Entre em contato e nos questione.

## Solução
1. Foram criadas imagens para ambas aplicações seguindo algums práticas:

   a. Imagens oficiais Docker Hub
    Backend https://hub.docker.com/_/golang / https://hub.docker.com/_/alpine
    Frontend: https://hub.docker.com/_/python 

   b. multi-stage build: Para a aplicação backend foi usado um Dockerfile multi-stage que permite uma imagem final da aplicação somente com o necessário para ser executada, além de ser fácil de ler e manter. (https://docs.docker.com/develop/develop-images/multistage-build/)     
   
   c. Tags: Foram usadas nas imagens base versões estáveis de tag do repositório Docker Hub, evitando a tag 'latest' por questões de estabilidade das versões da stack geradas nesse ciclo de desenvolvimento  


2. Docker-compose
   a. Maior agilidade em tempo de desenvolvimento, permitindo flexibilidade para que o desenvolvedor construa/reconstrua a stack em seu desenvolvimento.   

   b. As configurações do docker-compose disponíveis podem ser convertidas posteriormente para plataformas como kubernetes, Openshift, AWS ECS, por exemplo;   

   c. Figuradamente, o Docker-compose disponibilizado poderia ser um template padronizado de stack, convertido de uma stack que roda nas plataformas produtivas.    

3. Desenho da solução:

![Stack](stack.png)

## Pre requisitos
* Docker 17.05 ou maior (https://docs.docker.com/install/)
* Docker-Compose (https://docs.docker.com/compose/install/)

## Build e boostrap da stack
*Executar os command lines:
   Essa linha de comando irá disponibilizar as imagens para o container   
`docker-compose build`

   Essa linha de comando irá disponibilizar a criação dos containers   
`docker-compose up`
⋅

## Release Note Backend
 * Adicionado um arquivo de módulo para download das dependências da solução backend

## Release Note Frontend
 * Adicionado arquivo .env para carregamento de variaveis de ambiente solução frontend

