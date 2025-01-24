# Projeto AWS-DevOps

## Índice
- [Sobre o Projeto](#sobre-o-projeto)
- [Arquitetura Geral](#arquitetura-geral)
- [Serviços AWS Utilizados](#serviços-aws-utilizados)
- [Etapas do Projeto](#etapas-do-projeto)
  - [1 - Configurar uma Aplicação Web na Nuvem](#1-configurar-uma-aplicação-web-na-nuvem)
  - [2 - Conectar um repositório GitHub à AWS](#2-conectar-um-repositório-github-à-aws)
  - [3 - Proteger as dependências com AWS CodeArtifact](#3-proteger-as-dependências-com-o-aws-codeartifact)
  - [4 - Empacotar uma aplicação com AWS CodeBuild](#4-empacotar-uma-aplicação-com-o-aws-codebuild)
  - [5 - Implante uma aplicação com AWS CodeDeploy](#5-implante-uma-aplicação-com-o-aws-codedeploy)
  - [6 - Pipeline CI/CD com AWS CodePipeline](#6-pipeline-cicd-com-codepipeline)


## Sobre o Projeto
Este projeto tem como objetivo criar um pipeline CI/CD para construir e implantar uma aplicação web simples utilizando 
serviços da AWS voltados para DevOps. Para facilitar o aprendizado, o projeto foi dividido em seis etapas, proporcionando uma 
abordagem prática e estruturada, além de permitir uma melhor compreensão e aplicação dos serviços da AWS e das tecnologias utilizadas.

## Arquitetura Geral
[... conteúdo ...]

## Serviços AWS Utilizados
AWS IAM: criar usuário, configurar políticas e roles. <br> 
Amazon EC2: servir como ambiente de desenvolvimento e ambiente de produção. <br>
AWS CodeArtifact: salvar cópias das dependências da aplicação web. <br>
AWS CodeBuild: compilar e empacotar o código-fonte da aplicação em um arquivo WAR. <br>
AWS CodeDeploy: implantar o arquivo WAR no servidor de produção. <br>
AWS CloudFormation: criar a instância e a VPC do ambiente de desenvolvimento. <br>
AWS CodePipeline: automatizar as integrações entre GitHub, CodeBuild e CodeDeploy. <br>

## Etapas do Projeto
### 1 - Configurar uma Aplicação Web na Nuvem
#### Configurar um usuário IAM
Por questões de segurança, acesse o console da AWS com seu usuário IAM. Caso ainda não tenha um, consulte a 
[documentação oficial](https://docs.aws.amazon.com/pt_br/streams/latest/dev/setting-up.html#:~:text=Para%20criar%20um%20grupo%20de,Administrators%20e%20escolha%20Pr%C3%B3xima%20etapa.) 
para criá-lo.

#### Lançar uma instância EC2
Para hospedar o ambiente de desenvolvimento, é necessária a criação de uma instância EC2.
Consulte a [documentação oficial](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/tutorial-launch-a-test-ec2-instance.html) 
para lançar a instância, configurar um par de chaves e a rede da instância.

#### Estabelecer uma conexão SSH com a instância EC2
Caso seja necessário, utilize o comando `chmod 400 arquivo.pem` para alterar as permissões do seu arquivo .pem. <br>
Para conectar à instância, utilize: 
`ssh -i [CAMINHO PARA O SEU ARQUIVO .PEM] ec2-user@[SEU DNS PÚBLICO IPV4]`

#### Instalar o Apache Maven e o Amazon Corretto 8 para gerar uma aplicação web simples
Instalar Apache Maven na Instância EC2:
```
wget https://archive.apache.org/dist/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz
sudo tar -xzf apache-maven-3.5.2-bin.tar.gz -C /opt
echo "export PATH=/opt/apache-maven-3.5.2/bin:$PATH" >> ~/.bashrc
source ~/.bashrc
```

Instalar Amazon Corretto 8, uma versão do Java na AWS:
``` 
sudo dnf install -y java-1.8.0-amazon-corretto-devel
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64
export PATH=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64/jre/bin/:$PATH
```

#### Executar os comandos Maven no terminal para gerar uma aplicação web em Java
```
mvn archetype:generate \
   -DgroupId=com.awsdevops.app \
   -DartifactId=aws-devops-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false
```

#### Conectar o VSCode à instância EC2 usando o Remote-SSH
Instalar a extensão [Remote-SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) 
no VSCode para que você possa ver e editar a app web que acabou de criar.
![remote-SSH2](./images/remote-SSH1.png)


### 2 - Conectar um repositório GitHub à AWS
#### Instalar o Git na instância EC2
[... conteúdo ...]

#### Conectar o seu projeto de aplicação web a um repositório GitHub
[... conteúdo ...]

### 3 - Proteger as dependências com AWS CodeArtifact
#### Criar seu domínio e repositório
[... conteúdo ...]

#### Conectar o repositório CodeArtifact ao VSCode
[... conteúdo ...]

#### Testar a conexão entre CodeArtifact e VSCode
[... conteúdo ...]

#### Conferir o repositório no CodeArtifact
[... conteúdo ...]

#### Configure uma política do IAM para usar o CodeArtifact
[... conteúdo ...]

### 4 - Empacotar uma aplicação com AWS CodeBuild
#### Criar um bucket do S3
[... conteúdo ...]

#### Criar um projeto de build no CodeBuild
[... conteúdo ...]

#### Criar o arquivo buildspec.yml da sua aplicação web
[... conteúdo ...]

#### Modificando a IAM role do seu CodeBuild
[... conteúdo ...]

#### Testar o projeto de build
[... conteúdo ...]

### 5 - Implante uma aplicação com AWS CodeDeploy
#### Criar uma instância EC2 e VPC com AWS CloudFormation
[... conteúdo ...]

#### Criar scripts para executar a aplicação
[... conteúdo ...]

#### Criar a IAM role do CodeDeploy
[... conteúdo ...]

#### Criar uma aplicação do CodeDeploy
[... conteúdo ...]

#### Criar um deployment group
[... conteúdo ...]

#### Criar seu deployment
[... conteúdo ...]

### 6 - Pipeline CI/CD com AWS CodePipeline
#### Configurar seu pipeline
[... conteúdo ...]

#### Lançar uma Alteração
[... conteúdo ...]

#### Acionar um Rollback
[... conteúdo ...]

#### Release Change
[... conteúdo ...]
