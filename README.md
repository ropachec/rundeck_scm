# Rundeck - SCM - Criação, Commit e Push
### Automação da integração do Rundeck com SCM, Criação, Commit e Push

Este script permite que seja criado no rundeck a integração com o SCM caso não exista para o projeto.
Valida os jobs alterados e realiza o commit e push dos mesmos.
Valida os jobs deletados e realiza o commit e push dos mesmos.


Para COnfigurar o SCM o script utiliza um template json criado anteriormente com o comando:
### rd projects scm config -p NOMEPROJETO --file config.json --integration export

Para o template foi ajustado uma única PRIVATEKEY e definido o nome de projeto: PROJECTNAME
O nome de projeto é substituido via sed assim que o template é invocado.

### Descrição das ações conforme comentários no script:

Recebe os projetos listados pela variavel project_list
Verifica a saida do scm status a fim de identificar qual projeto tem job passivel de commit
A partir da lista de projetos com pendência de commit, lista os uuids dos jobs
Executa o comando para export dos jobs para o git e seu respectivo commit
Executa o push dos jobs commitados

Caso a variavel ${valida_commit} seja nula - entende que o scm não está configurado
copia o template do json gerado anteriormente pelo comando
### rd projects scm config -p NOMEPROJETO --file config.json --integration export
O arquivo foi pré ajustado de forma que todos os locais com nome do projeto recebem o valor: PROJECTNAME
Para todos os repositorios ficou definida a mesma private key, criada anteriormente no projeto que gera o template
O nome do arquivo para template ficou: config.json.template

Realiza a copia do arquivo de template para um arquivo do projeto
Realiza a troca dos nomes de: PROJECTNAME para o nome do projeto em si
Inicia o setup passando o nome do projeto, arquivo json, tipo de integração e tipo de plugin.
Tipo de integração pode receber export ou import
tipo de plugin pode receber git-export ou git-import

