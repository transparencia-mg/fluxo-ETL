# Setup da máquina para uso de repositórios git com controle de versão

## Indispensável

- [ ] Autorizar usuário como administrador da máquina pois algumas instalações necessitam deste privilégio.
- [ ] Instalar editor de Texto de sua preferência.
  * Indicação: Sublime.
  * Pesquisar no google "sublime download for windows".
  * Realizar o download e instalação da versão mais recente disponível.
  * Importante instalar editor primeiro pois durante instalação git (próxima etapa) deverá ser selecionado o editor padrão.

 - Incluir o caminho de instalação do Sublime no path do window:
   - Abra o prompt de comando e digite "sysdm.cpl".
   - Na aba "Advanced" selecione "Environment variables".
   - Na "system variables" chamada "Path" clique em "edit".
   - Adicione "C:\Program Files\Sublime Text3".
   - Salve e reinicie o prompt de comando.
 - Obs.: Selecione o caminho de instalação da sua máquina e não copie e cole o que os tutorais sugerem, pois poderá haver divergência.
 - Utilização: Navegando até a pasta desejada digite "subl ."
- [ ] Configurar atalho [Sublime auto-save](https://lucybain.com/resources/setting-up-sublime-autosave/).
- [ ] Configurar atalho para [comentar linhas](https://newbedev.com/shortcut-to-comment-out-a-block-of-code-with-sublime-text) no Sublime
- [ ] Instalar [git](https://git-scm.com/).
  -  Apenas a título de sugestão, visto que isso não atrapalhará em nada a instalação, como utilizaremos muito github, seguir com as opções padrão até "Adjusting the name of the initial branch in new repositories" e selecionar a opção "Override the default branch name for new repositories" com "main" na caixa de diálogo aberta para inserção da sua branch padrão. 
  -  Em "Configuring the terminal emulator to use with Git Bash" selecione "Use Windows' default console window"
  - Conferência de instalação realizada com sucesso:

```Git Bash Terminal
$ git --version

# Tipo de resposta esperada, podendo a versão ser diferente devido à data de instalação
git version 2.33.0.windows.2
```

- [ ] Configurar git para clone, pull, push via Proxy.
  - Clonar repositórios sempre visa https. 
  - [Link de Referência](https://stackoverflow.com/questions/18356502/github-failed-to-connect-to-github-443-windows-failed-to-connect-to-github). 

```Git Bash Terminal
# Modelo
# Não copie e cole cegamente, troque USER, PASSOWORD, PROXYADDRESS e PORT
$ git config --global http.proxy http://USER:PASSWORD@PROXYADDRESS:PORT

# Exemplo
$ git config --global http.proxy http://m123456:123456@proxycamg.prodemge.gov.br:8080
```
- [ ] Instalação [git large files - glf](https://git-lfs.github.com/)
 - [ ] Download e instalação de executável para Windows.
 - [ ] Finalização da instalação via terminal e conferência 

```Git Bash Terminal
# Instalação
git lfs install

# Tipo de resposta esperada, podendo a versão ser diferente devido à data de instalação
$ git lfs --version
git-lfs/2.13.3 (GitHub; windows amd64; go 1.16.2; git a5e65851)
```

## Aconselhável

- [ ] Instalar [Sublime ZK](https://github.com/renerocksai/sublime_zk), caso sublime tenha sido escolhido como editor de sua preferência.
- [ ] Configurar abertura Sublime via terminal.
 - [Vídeo de Referência](https://www.youtube.com/watch?v=MlnH8t4S4Qw).
 - [Link de Referência](https://stackoverflow.com/questions/9440639/sublime-text-from-command-line#:~:text=Add%20the%20installation%20folder%20to,cpl).


## Para rodar pacote dtamg

- [ ] Instalar Python 3.9
 - [Baixar e instalar Python 3.9](https://www.python.org/downloads/).
  - [Vídeo de Referência](https://www.youtube.com/watch?v=8aZkrsIQT3Y)
  - Muito importante na primeira tela da importação marcar a opção "Add Python 3.9 to PATH".
  - Selecionar a opção "Customize installation".
  - Em "Advanced Options" marque "Install for all users".
  - Conferência de instalação realizada com sucesso:

```Git Bash Terminal
$ python --version

# Tipo de resposta esperada, podendo a versão ser diferente devido à data de instalação
Python 3.9.6
```

## Para rodar validação local com makefile

- [ ] Instalar [R](https://vps.fmvz.usp.br/CRAN/)
- [ ] Instalar Make
 - [Vídeo de Referência](https://www.youtube.com/watch?v=taCJhnBXG_w) - Não consegui fazer o comando make funcionar isoladamente, conforme explicado no final do vídeo. Por enquanto somente  mingw32-make
- Realizar login no [Portal de Dados Abertos - Produção](https://dados.mg.gov.br)
- Realizar login no [Portal de Dados Abertos - Homologação](https://homologa.cge.mg.gov.br)
- Realizar cadastro de [variáveis de ambiente Windows](https://www.architectryan.com/2018/08/31/how-to-change-environment-variables-on-windows-10/) para publicação de recursos nos ambientes de produção e homologação:
 - Produção:
  - CKAN_HOST_PRODUCAO e CKAN_KEY_PRODUCAO
 - Homologação:
  - CKAN_HOST e CKAN_KEY
- [Configurar proxy para instalar pacotes python](https://leifengblog.net/blog/how-to-use-pip-behind-a-proxy/)