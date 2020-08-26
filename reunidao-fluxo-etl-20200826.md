- Os seguintes cenários de publicação devem estar contemplados no fluxo ETL:
    - csv processado via FTP (eg. Despesa, Compras)
    - csv para processamento via FTP (eg. Remuneração)
    - csv para processamento via email (eg. Óbitos)
    - csv para processamento via armazém/email (eg. Compras emergenciais)
    - metadados via email (eg. Casos confirmados)

## Comportamento geral

- Todo conjunto de dados é um Data Package válido e possui um repositório de controle de versão associado

- Os repositórios estarão em uma organização própria em uma plataforma de hospedagem git (eg. Github)

- O valor da propriedade `name` do data package deve ser o mesmo que o conjunto de dados do CKAN e o repositório git
    - Ex: O data package com propriedade `name=compras-emergenciais-covid-19` possui um conjunto de dados `http://dados.mg.gov.br/dataset/compras-emergenciais-covid-19` e um repositório `https://github.com/dados-mg/compras-emergenciais-covid-19`

- Cada ambiente do CKAN possui um branch associado no repositório git. O ambiente de homologação está associado ao branch `homologa` e o ambiente de produção ao branch `prod`

- O primeiro commit no branch `homologa` gera a criação de um novo conjunto de dados na instância do CKAN em homologação

- O primeiro commit no branch `prod` gera a criação de um novo conjunto de dados na instância do CKAN em ambiente de produção

- O processo de criação nos dois ambientes deve validar que o arquivo `datapackage.json` existe e é um data package válido do ponto de vista estrutural (sintaxe)
    - Exemplo: Vírgula faltando no arquivo `json`

- Após a criação inicial, todo commit nos branchs `homologa` e `prod` deve acionar o processo de atualização de metadados

- O controle de atualização dos metadados do conjunto de dados, dos recursos, e do dicionário de dados é realizado pelo confronto entre a propriedade `version` do `datapackage.json` e a propriedade `version` do conjunto de dados no CKAN. A mudança de versão deve atualizar todos os metadados de acordo com o DE_PARA (link para arquivo)

## Data packages com armazenamento no repositório 

- Após a criação inicial, todo commit nos branches `homoloha` e `prod` que alterou arquivos de recursos em `data/` devem gerar atualização dos recursos para os recursos alterados
    - Essa informação está disponível, por exemplo, no histórico do commit

- Criação de novo recurso

- Atualização de recurso existente

## Data packages com armazenamento no FTP

- Os data packages que possuem arquivos armazenados no FTP possuem processamento diferenciado


# Problemas

- a criação de um novo repositório deve disparar a criação de conjuntos de dados vazios? Nesse momento somente existe a propriedade `name` proveniente da slug do repositório.

- o arquivo `datapackage.json` não pode ter informações especificas de determinado branch (eg.`path`) ou de determinada instância do CKAN (eg. `id`)


# Tarefas

- [ ] Criar issue para decisão de inserir organização no `datapackage.json`. Pela [documentação do CKAN](https://docs.ckan.org/en/2.8/api/index.html#module-ckan.logic.action.create) essa propriedade pode ser opcional:

    > owner_org (string) – the id of the dataset’s owning organization, see organization_list() or organization_list_for_user() for available values. This parameter can be made optional if the config option ckan.auth.create_unowned_dataset is set to True.

- [ ] Pensar nas associações entre os branches e os ambientes de tal forma que as convenções de nomeclatura sejam respeitadas e o fluxo de trabalho seja natural (eg. não é necessário lembrar de mudar o nome do branch padrão)