- Os seguintes cenários de publicação devem estar contemplados no fluxo ETL:
    - csv processado via FTP (eg. Despesa, Compras)
    - csv para processamento via FTP (eg. Remuneração)
    - csv para processamento via email (eg. Óbitos)
    - csv para processamento via armazém/email (eg. Compras emergenciais)
    - metadados via email (eg. Casos confirmados)

## Comportamento geral

- Cada ambiente do CKAN possui um branch associado no repositório git. O ambiente de homologação está associado ao branch `homologa` e o ambiente de produção ao branch `prod`

- O primeiro commit no branch `homologa` gera a criação de um novo conjunto de dados na instância do CKAN em homologação

- O primeiro commit no branch `prod` gera a criação de um novo conjunto de dados na instância do CKAN em ambiente de produção

- O processo inicial de criação deve popular:
	 
	 os metadados do conjunto de dados; 

	 os metadados dos recursos;

	 os metadados do dicionário de dados (Data Store), caso existam;

	 os dados do recurso

- Todo datapackage deve ter pelo menos um recurso (Na especificação do frictionless data, é obrigatório que o data package tenha propriedade fazendo referência ao recurso.)

- O processo de criação nos dois ambientes deve validar que o arquivo `datapackage.json` existe e é um data package válido do ponto de vista estrutural (sintaxe)
    - Exemplo: Vírgula faltando no arquivo `json`

- Após a criação inicial, todo commit nos branchs `homologa` e `prod` deve verificar a necessidade de mudança de metadados, em pelo menos algum dos 3 níveis (conjunto, recurso ou dicionário). 

- As seguintes mudanças no datapackage.json deverão ser refletidas no ambiente apropriado do CKAN:

	+ Atualizar metadados datapackage
    + Atualizar metadados dos recursos
    + Atualizar metadados do dicionário de dados (modificação de propriedades, adição ou exclusão de variáveis)
    + Adicionar recursos
    + Excluir recursos

- A necessidade de atualização de metadados deve ser realizada pelo confronto entre a propriedade `version` do `datapackage.json` e a propriedade `version` do conjunto de dados no CKAN. A mudança de versão deve atualizar todos os metadados 


## Data packages com armazenamento no repositório 

- Após a criação inicial, todo commit nos branches `homologa` e `prod` deve gerar atualização dos recursos alterados da pasta `data`. Essa informação está disponível no histórico do commit. O commit é um evento, que tem de ser interpretado para determinar a ação a ser refletida no conjunto de dados. As mudanças podem ser relativas a:

- Commit (evento) - Após commit inicial
    - Evento deve ser interpretado pela rotina para determinação da mudança que deve ser refletida no conjunto de dados
    - As mudanças podem ser relativas à:
        + Atualizar metadados datapackage
        + Atualizar metadados dos recursos
        + Atualizar metadados do dicionário de dados
        + Adicionar recursos
        + Excluir recursos
    - Atualizar dados dos recursos

- Para cada job de execução, deve haver um log acessível e perene no tempo com:
	- identificador, 
	- resultado de validação (sintaxe/estrutura arquivos)

- Se houver algum desvio nos comportamentos descritos nesta especificação, uma notificação deve ser enviada para o email determinado contendo a listagem de jobs com erro

## Data packages com armazenamento no FTP

- Os data packages que possuem arquivos armazenados no FTP possuem processamento diferenciado

https://github.com/frictionlessdata/forum/issues/23


# Dúvidas

- Há casos de uso para conjuntos de dados sem recursos? Na especificação do frictionless data, é obrigatório que o data package tenha propriedade fazendo referência ao recurso. (ex.: As chamadas para APIs do portal federal também são recursos)

- Mudança de versão MINOR de datasets com atualizações diárias: vide [especificações da frictionless data](https://specs.frictionlessdata.io/patterns/#specification-7)


# Problemas

- controle de atualização realizado por meio da propriedade `version` não discrimina em qual nível de metadado a alteração deve ser processada (dicionário, recurso, conjunto). Vale a pena fazer um diff das mundanças?

- a criação de um novo repositório deve disparar a criação de conjuntos de dados vazios? Nesse momento somente existe a propriedade `name` proveniente da slug do repositório.

- o arquivo `datapackage.json` não pode ter informações especificas de determinado branch (eg.`path`) ou de determinada instância do CKAN (eg. `id`)


# Tarefas

- [ ] Criar issue para decisão de inserir organização no `datapackage.json`. Pela [documentação do CKAN](https://docs.ckan.org/en/2.8/api/index.html#module-ckan.logic.action.create) essa propriedade pode ser opcional:

    > owner_org (string) – the id of the dataset’s owning organization, see organization_list() or organization_list_for_user() for available values. This parameter can be made optional if the config option ckan.auth.create_unowned_dataset is set to True.

- [ ] Pensar nas associações entre os branches e os ambientes de tal forma que as convenções de nomeclatura sejam respeitadas e o fluxo de trabalho seja natural (eg. não é necessário lembrar de mudar o nome do branch padrão)