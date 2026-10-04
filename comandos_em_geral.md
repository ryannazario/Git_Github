# COMANDOS GIT APRENDIDOS DATACAMP



## 1. TERMINAL E CRIAÇÃO DE REPOSITÓRIO


pwd  ->  Mostra em qual pasta (diretório) você está agora.
ls  ->  Lista os arquivos e pastas do diretório atual.
cd archive  ->  Entra na pasta "archive".

git --version  ->  Mostra a versão do Git instalada.

git init  ->  Transforma a pasta atual em um repositório Git. Pode ser git init .
git init mental-health-workspace  ->  Cria a pasta "mental-health-workspace" já como repositório Git.
git status  ->  Mostra o estado do repositório: arquivos modificados, em staging e não rastreados.


## 2. STAGING E COMMITS


git add README.md  ->  Coloca o README.md na área de staging (prepara para o commit).
git add .  ->  Coloca todas as alterações da pasta atual na área de staging.
git commit -m "Adding a README."  ->  Cria um commit com o que está em staging; -m define a mensagem entre aspas.


## 3. HISTÓRICO DE COMMITS


git log  ->  Mostra o histórico de commits (hash, autor, data e mensagem).
git log -3  ->  Mostra só os 3 commits mais recentes.
git log report.md  ->  Mostra só os commits que alteraram o report.md.
git log -2 mental_health_survey.csv  ->  Mostra os 2 commits mais recentes que alteraram esse arquivo.
git log --since='Month Day Year'  ->  Mostra os commits feitos a partir de uma data (formato genérico).
git log --since='Apr 2 2024'  ->  Mostra os commits feitos desde 2 de abril de 2024.
git log --since='Apr 2 2024' --until='Apr 11 2024'  ->  Mostra os commits entre 2 e 11 de abril de 2024.

No git log:
  Space  ->  Avança uma página do histórico.
  q  ->  Sai da tela do log.


## 4. INSPECIONAR UM COMMIT


git show c27fa856  ->  Mostra os detalhes e as alterações do commit com esse hash.
git show <hash>  ->  Mesmo comando para qualquer commit (trocar <hash> pelo código dele).


## 5. COMPARAR VERSÕES COM GIT DIFF


git diff  ->  Mostra as alterações feitas que ainda NÃO estão em staging.
git diff report.md  ->  Mesmo, só para o report.md.
git diff --staged  ->  Mostra as alterações que JÁ estão em staging (prontas para o commit).
git diff --staged report.md  ->  Mesmo, só para o report.md.
git diff 35f4b4d 186398f  ->  Compara dois commits pelos seus hashes.
git diff HEAD~1 HEAD  ->  Compara o commit anterior com o atual (mostra o que mudou no último commit).
git diff HEAD~1 HEAD~2  ->  Compara o penúltimo commit com o antepenúltimo.
git diff main summary-statistics  ->  Compara a branch main com a branch summary-statistics.
git diff main chatbot  ->  Compara a branch main com a branch chatbot.
git diff main hotfix  ->  Compara a branch main com a branch hotfix.

Referências:
  HEAD  ->  O commit atual (o mais recente da branch em que você está).
  HEAD~1  ->  Um commit antes do HEAD.
  HEAD~2  ->  Dois commits antes do HEAD.


## 6. DESFAZER ALTERAÇÕES


git revert HEAD  ->  Cria um novo commit que desfaz as mudanças do último commit (abre o editor para a mensagem).
git revert HEAD --no-edit  ->  Igual, mas aceita a mensagem padrão sem abrir o editor.
git revert --no-edit HEAD  ->  Equivalente ao anterior (a ordem das opções não importa).
git revert HEAD -n  ->  Desfaz as mudanças do último commit, mas SEM criar o commit (-n = --no-commit); deixa tudo em staging.
git revert -n HEAD  ->  Equivalente ao anterior.
git checkout HEAD~1 -- report.md  ->  Restaura o report.md para a versão do commit anterior.
git restore --staged report.md  ->  Tira o report.md do staging, sem perder as alterações no arquivo.
git restore --staged summary_statistics.csv  ->  Tira o summary_statistics.csv do staging.
git restore --staged  ->  Sozinho o Git dá erro: precisa de um caminho (ex.: "git restore --staged ." tira tudo do staging).


## 7. BRANCHES


git branch  ->  Lista as branches; o * marca a branch atual.
git branch speed-test  ->  Cria a branch "speed-test" (sem mudar para ela).
git switch main  ->  Muda para a branch main.
git switch speed-test  ->  Muda para a branch speed-test.
git switch -c speed-test  ->  Cria a branch speed-test e já muda para ela.
git branch -m  ->  Renomeia uma branch (-m = mover/renomear); precisa dos nomes, como nas linhas abaixo.
git branch -m feature_dev chatbot  ->  Renomeia a branch "feature_dev" para "chatbot".
git branch -m old_name new_name  ->  Forma geral: renomeia de nome_antigo para nome_novo.
git branch -d chatbot  ->  Apaga a branch "chatbot", mas só se ela já foi mesclada (merge).
git branch -D chatbot  ->  Apaga a branch "chatbot" à força, mesmo sem ter sido mesclada.


## 8. MERGE DE BRANCHES


git switch main  ->  Vai para a branch que vai RECEBER as mudanças.
git merge source  ->  Mescla a branch "source" (origem) na branch atual.
git merge ai-assistant  ->  Mescla a branch "ai-assistant" na branch atual.
git merge source destination  ->  Forma usada no curso: mescla "source" em "destination".
git merge ai-assistant main  ->  Exemplo da forma acima: mescla "ai-assistant" na "main".

Obs.: no Git "puro", o jeito padrão é estar na branch de destino e rodar
"git merge source". Com dois nomes, o Git mescla os dois na branch em que
você está no momento.


## 9. RESOLVER MERGE CONFLICTS


git merge documentation  ->  Tenta mesclar a branch "documentation"; se houver conflito, o Git para e marca os arquivos conflitantes.
nano README.md  ->  Abre o README.md no editor nano para resolver o conflito na mão.
git add README.md  ->  Marca o arquivo como resolvido (coloca em staging).
git commit -m "Resolving README.md conflict"  ->  Conclui o merge com um commit.
git merge documentation  ->  Repetido na lista: roda o merge de novo; depois de resolvido, o Git avisa que já está atualizado.

No nano:
  Ctrl + O  ->  Salva o arquivo (Write Out).
  Enter  ->  Confirma o nome do arquivo ao salvar.
  Ctrl + X  ->  Sai do nano.

Marcadores de conflito:
  <<<<<<<  ->  Início da versão da branch atual (HEAD).
  =======  ->  Separa a versão da branch atual da versão da outra branch.
  >>>>>>>  ->  Fim da versão da outra branch.
  (Para resolver: escolha ou combine as versões e apague os três marcadores.)


## 10. CLONAR REPOSITÓRIOS


git clone path-to-project-repo  ->  Copia um repositório existente (com todo o histórico) para uma nova pasta.
git clone /home/george/repo  ->  Clona um repositório que está no seu computador.
git clone /home/george/repo new_repo  ->  Clona e dá o nome "new_repo" à nova pasta.
git clone URL  ->  Clona um repositório a partir de uma URL.
git clone https://github.com/datacamp/project  ->  Clona um projeto do GitHub.


## 11. REMOTES


git remote  ->  Lista os nomes dos repositórios remotos configurados (ex.: origin).
git remote -v  ->  Lista os remotos junto com as URLs (fetch e push).
git remote add name URL  ->  Adiciona um remoto, dando a ele um apelido (name) e a URL.
git remote add george https://github.com/george_datacamp/repo  ->  Adiciona o remoto "george" apontando para o repositório do George.


## 12. FETCH


git fetch origin  ->  Baixa as novidades do remoto "origin" sem mesclar nada na sua branch.
git fetch origin main  ->  Baixa só as novidades da branch main do remoto.
git merge origin  ->  Mescla na sua branch o que foi baixado (em geral, usa-se git merge origin/main).


## 13. PULL


git pull origin  ->  Faz fetch + merge: baixa do remoto "origin" e já mescla na branch atual.
git pull origin dev  ->  Traz e mescla a branch "dev" do remoto.
git pull origin main  ->  Traz e mescla a branch "main" do remoto.
git pull --no-edit origin main  ->  Igual ao anterior, mas sem abrir o editor para a mensagem do merge.


## 14. PUSH


git push  ->  Envia os commits da branch atual para o remoto configurado.
git push remote local_branch  ->  Forma geral: envia a branch local para o remoto indicado.
git push origin main  ->  Envia a branch main para o remoto "origin".
git push origin hotfix  ->  Envia a branch hotfix para o remoto "origin".
git push origin documentation  ->  Envia a branch documentation para o remoto "origin".

## 15. GIT CHECKOUT E SUAS FUNCIONALIDADES

 
O git checkout é um comando "faz-tudo": serve para trocar de branch, viajar
para um commit antigo e restaurar arquivos. Por isso o Git criou o git switch
(para branches) e o git restore (para arquivos), que fazem cada parte
separadamente. Mesmo assim, o checkout continua muito usado.
 
A) Trocar de branch
git checkout main  ->  Muda para a branch main (equivale a git switch main).
git checkout speed-test  ->  Muda para a branch speed-test.
git checkout -  ->  Volta para a branch em que você estava antes.
 
B) Criar uma branch e mudar para ela
git checkout -b speed-test  ->  Cria a branch speed-test e já muda para ela (equivale a git switch -c speed-test).
git checkout -b hotfix main  ->  Cria a branch hotfix a partir da main e muda para ela.
 
C) Ir para um commit antigo (detached HEAD)
git checkout c27fa856  ->  Vai para o commit com esse hash; você vê os arquivos como estavam naquele momento.
git checkout HEAD~1  ->  Vai para o commit anterior ao atual.
git checkout main  ->  Volta para a ponta da branch main (sai do detached HEAD).
 
  Detached HEAD: significa que o HEAD não está em nenhuma branch. Serve para
  olhar ou testar o passado. Commits feitos nesse estado podem se perder ao
  trocar de branch. Para guardar o trabalho, crie uma branch ali mesmo:
  git checkout -b nova-branch (ou git switch -c nova-branch).
 
D) Restaurar um arquivo de outro commit ou branch
git checkout HEAD~1 -- report.md  ->  Traz o report.md como estava no commit anterior (o arquivo já fica em staging).
git checkout c27fa856 -- report.md  ->  Traz o report.md como estava nesse commit específico.
git checkout main -- report.md  ->  Traz o report.md como está na branch main.
 
  O "--" separa o nome da branch/commit do nome do arquivo. Só o arquivo
  indicado muda; o resto do projeto e a branch atual ficam como estão.
  Depois, é só fazer o commit para registrar a restauração.
 
E) Descartar alterações que ainda não foram para o staging
git checkout -- report.md  ->  Joga fora as alterações não salvas do report.md e volta ao último estado registrado.
git checkout .  ->  Faz o mesmo para todos os arquivos da pasta atual.
 
  CUIDADO: essas alterações descartadas NÃO podem ser recuperadas depois.
 
F) Pegar uma branch que só existe no remoto
git checkout dev  ->  Se "dev" só existe no remoto (após um git fetch), cria uma branch local dev ligada a ela.
git checkout --track origin/dev  ->  Mesmo resultado, escrito de forma explícita.
 
Equivalentes modernos (aproximados):
  Trocar de branch                  ->  git switch main
  Criar e mudar de branch           ->  git switch -c nova-branch
  Voltar à branch anterior          ->  git switch -
  Ir para um commit (só olhar)      ->  git switch --detach c27fa856
  Restaurar arquivo de um commit    ->  git restore --source=HEAD~1 report.md
  Descartar alterações do arquivo   ->  git restore report.md


### RESUMO DOS PRINCIPAIS COMANDOS


pwd  ->  Mostra a pasta atual.
ls  ->  Lista arquivos e pastas.
cd  ->  Muda de pasta.
git --version  ->  Mostra a versão do Git.
git init  ->  Cria um repositório.
git status  ->  Mostra o estado dos arquivos.
git add  ->  Coloca alterações em staging.
git commit  ->  Registra as alterações em staging como um commit.
git log  ->  Mostra o histórico de commits.
git show  ->  Mostra os detalhes de um commit.
git diff  ->  Compara versões (arquivos, commits ou branches).
git revert  ->  Desfaz um commit criando um novo commit.
git checkout  ->  Troca de branch, vai para um commit antigo ou restaura arquivos (ver seção 15).
git restore  ->  Aqui: tira arquivos do staging.
git branch  ->  Lista, cria, renomeia ou apaga branches.
git switch  ->  Muda de branch (ou cria com -c).
git merge  ->  Junta uma branch em outra.
git clone  ->  Copia um repositório existente.
git remote  ->  Gerencia os repositórios remotos.
git fetch  ->  Baixa novidades do remoto sem mesclar.
git pull  ->  Baixa do remoto e mescla (fetch + merge).
git push  ->  Envia commits para o remoto.
nano  ->  Editor de texto no terminal.