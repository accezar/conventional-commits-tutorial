# Garantindo padrões de commit em repositórios

> _O histórico de commits de um repositório é como o índice de um livro: Ele nos leva a um momento do tempo onde uma mudança foi inserida na base de código. Garantir um histórico claro e padronizado facilita a manutenção e a localização de bugs na aplicação. Este artigo abordará as ferramentas disponíveis para padronizar os commits durante o desenvolvimento_

Como desenvolvedores, sabemos como o uso do git é essencial para nosso trabalho. O histórico de commits é como o índice de um livro: ele nos leva a um momento do tempo onde uma mudança foi inserida na base de código. É complicado para um desenvolvedor localizar-se em um histórico de commits com titulos e descrições sem padrão e muitas vezes sem informação. Executar tarefas de análise e encontrar em que ponto um bug foi inserido no código e as possíveis areas afetadas levam um tempo muito grande, ficamos perdidos com o histórico dos acontecimentos e no que eles realmente fazem.

![Exemplo de um histórico de commits sem contexto e sem padrões definidos](blob:https://madeiramadeira.atlassian.net/fe015446-210b-4d78-98a6-4b8564f06b61#media-blob-url=true&id=a0f6e3e7-44d0-4363-9226-21033474d470&contextId=2328953047&collection=contentId-2328953047 "Exemplo de um histórico de commits sem contexto e sem padrões definidoso")


Equipes perceberam então que era necessário dispor de uma lingua coerente e padronizada pra ajudar todos os envolvidos a entenderem o histórico do projeto e também que ajudasse a identificar as naturezas das alterações. Surgiu então a especificação ***Conventional Commits*** - inspirada na Angular Commits Guidelines - com o objetivo de estabelecer um conjunto fácil de regras para a criação de um histórico de commits explícito que torna mais fácil interpretar e gerir as mudanças.Há vários benefícios em adotar esse tipo de convenção, como por exemplo, poder automatizar a criação de changelogs, facilitar o entendimento na entrada de novos desenvolvedores no projeto, assim como poder gerar relatórios para avaliar a concentração do esforço nas horas do projeto (se em refatoração de código, criação de features, mudança de estilos, integração e deploy, entre outros). Adotando essa convenção também desestimulamos a mudança desordenada.

## Regras da especificação

As regras para esta especificação são simples, como demonstrado abaixo temos o tipo de commit (_type_), o escopo/contexto (_scope_) e o assunto do commit (_subject_) - _body_ e _footer_ representam o conteúdo e o rodapé do commit.

```bash
!type(?scope): !subject

<?body>
<?footer>
```

O type é responsável por nos dizer qual o tipo de alteração está sendo feita. Das regras da convenção, é obrigatório (!) e temos os seguintes tipos:

- **test**: indica qualquer alteração em códigos de teste. Exemplo: Criação ou modificação de testes unitários.

- **feat**: indica o desenvolvimento de uma nova feature ao projeto. Exemplo: Acréscimo de um serviço, funcionalidade, endpoint, etc.

- **refactor**: usado quando houver uma refatoração de código que não tenha qualquer tipo de impacto na lógica/regras de negócio do sistema. Exemplo: Mudanças de código após um code review.

- **style**: empregado quando há mudanças de formatação e estilo de código que não alteram o sistema de nenhuma forma. Exemplo: Indentações, remover espaços em brancos, remover comentários, etc..

- **fix**: utilizado quando há correção de erros que estão gerando bugs no sistema. Exemplo: Aplicar tratativa para uma função que não está tendo o comportamento esperado e retornando erro.

- **chore**: indica mudanças no projeto que não afetem o sistema ou arquivos de testes. São mudanças de desenvolvimento. Exemplo: Mudar regras do eslintrc, adicionar prettierrc, adicionar mais extensões de arquivos ao .gitignore.

- **docs**: usado quando há mudanças na documentação do projeto. Exemplo: adicionar informações na documentação da API, mudar o README, etc.

- **build**: utilizada para indicar mudanças que afetam o processo de build do projeto ou dependências externas. Exemplo: Adicionar/remover dependências do npm, editar scripts do package.json, etc.

- **perf**: indica uma alteração que melhorou a performance do sistema. Exemplo: alterar ForEach por while, melhorar a query do graphQL, etc.

- **ci**: utilizada para mudanças nos arquivos de configuração de CI. Exemplo: Github Actions, Git hooks etc.

- **revert**: indica reverter um commit anterior.

Com o type conseguimos entender a característica da alteração que foi realizada e com o subject entender com clareza o que o commit irá trazer se aplicado. Em repositórios enormes, como monorepos, ou projetos com vários pacotes ou features com mudanças paralelas, não fica bastante claro onde ou o quê commit irá alterar. Para isso, podemos utilizar o escopo(scope) do commit para entender o contexto da mudança.

![Exemplos de commit com scope. Fica fácil identificar qual contexto foi afetado e o tipo da alteração.](blob:https://madeiramadeira.atlassian.net/4e228cfd-99fe-45dc-99fa-5260b8136df9#media-blob-url=true&id=20fa99cb-42b2-4dbf-bd09-7c572f183fb7&contextId=2328953047&collection=contentId-2328953047 "Exemplos de commit com scope. Fica fácil identificar qual contexto foi afetado e o tipo da alteração.")


Mesmo o scope **não sendo obrigatório**, ele pode ser utilizado para contextualizar o commit e trazer menos responsabilidade para a subject, uma vez que dispondo do tipo de commit e o contexto que foi aplicado, a mensagem deve ser o mais breve e concisa possível. **Lembrando que o scope deve ser inserido no commit entre parênteses**.

Além disso, no caso do scope é possível adicionarmos múltiplos valores, como por exemplo: Caso houvesse uma refatoração de código em um repositório com versões mobile, web e desktop. A qual afeta o contexto mobile e web, poderíamos escrever o commit da seguinte maneira:

![Dessa maneira indicamos que é um commit de refatoração que afetara os contextos mobile e web da aplicação.](blob:https://madeiramadeira.atlassian.net/b249d8db-42eb-4116-a43b-67e3e7e1aff6#media-blob-url=true&id=42136942-472c-487c-b428-4acca3fc9394&contextId=2328953047&collection=contentId-2328953047 "Dessa maneira indicamos que é um commit de refatoração que afetara os contextos mobile e web da aplicação.")


**Observação**: Os escopos devem ser separados com `/` , `\\` ou `,`.

Resumindo, a convenção permite que o commit passe a conter elementos estruturais para comunicar sua intenção com outros consumidores da aplicação, como por exemplo, no caso do Versionamento Semântico. 

### Uma palha sobre o Semver..

A especificação de Versionamento Semântico consiste em um conjunto de regras que ditam como os números das versões da aplicação serão distribuidas e incrementadas. Em outras palavras, a quantidade de mudanças pelas quais o seu aplicativo ou projeto passou e quais alterações foram compatíveis ou incompatíveis com a versão anterior. 

![O contexto de cada mudança e o impacto da mesma pode ser identificado rapidamente por partes da numeração da versão.](blob:https://madeiramadeira.atlassian.net/81cca7cc-7a5c-44ce-893a-9df241159bcf#media-blob-url=true&id=880ca2fe-a576-41bd-a703-5d7236ccb47b&contextId=2328953047&collection=contentId-2328953047 "O contexto de cada mudança e o impacto da mesma pode ser identificado rapidamente por partes da numeração da versão.")


- **fix**: um commit com type fix corrige um bug na base e este é correlacionado a um PATCH no Versionamento Semântico.

- **feat**: um commit com type feat introduz uma nova feature e este é correlacionado a uma MINOR no Versionamento Semântico.

- **BREAKING CHANGE**: um commit com o footer BREAKING CHANGE:, ou que contenha um ! depois do type/scope, introduz uma mudança sem retrocompatibilidade e esta é correlacionada a uma MAJOR no Versionamento Semântico. Uma BREAKING CHANGE pode ser parte de um commit de qualquer type.

- _footers_ que fujam do formato BREAKING CHANGE: <description> devem ser fornecidos na convenção similar ao git trailer format.

Agora que sabemos como escrever nossos commits, vamos abordar as ferramentas que podem facilitar o processo de escrita e também na validação dos commits, garantindo que o padrão seja mantido. 

## Implementando a convenção

### Git Hooks

O git oferece um meio de disparar ações customizadas em diferentes estágios do processo de controle de versão. Estes ganchos aos eventos são conhecidos como hooks. Eles permitem que desenvolvedores e administradores automatizem tarefas durante o fluxo de trabalho, como por exemplo rodar um teste antes de um evento de commit. 

Existem dois tipos de hooks:

- ***client hooks***:  locais, são disparados por eventos no repositório local, como quando um desenvolvedor envia, recebe ou faz o merge do código.

- ***server hooks***:  remotos, são executados na rede que hospeda o repositório e são disparados por eventos como o recebimento de pushes.

Como queremos automatizar o processo da escrita e da validação das mensagens de commit vamos focar em criar client side hooks e em apenas alguns estágios do fluxo. Iremos usar apenas prepare-commit-msg e commit-msg, mas abaixo segue uma lista dos hooks mais utilizados.


![Hooks de maior uso](blob:https://madeiramadeira.atlassian.net/ed532551-1b5f-48c0-9c33-70827c323395#media-blob-url=true&id=6c20716a-d521-4e38-a9bd-d01031663446&contextId=2328953047&collection=contentId-2328953047 "Hooks de maior uso")


A forma manual de se escrever um hook consiste em criar uma pasta .git/hooks e adicionar um arquivo na sintaxe hook-name.sample. Os arquivos padrão são escritos como scripts de shell, mas você pode usar qualquer linguagem de script com a qual esteja familiarizado, desde que possa ser executado como um executável. Isso inclui Bash, Python, Ruby, Perl, Rust, Swift e Go. Escrever hooks manualmente não é produtivo e também é um desafio distribuir e garantir que os nossos hooks client side sejam instalados nas máquinas de outros desenvolvedores devido ao fato de que eles não são versionados no repositório. 

Vamos então conhecer o Husky.

### Husky

Husky é uma ferramenta que nos permite escrever facilmente hooks do Git e executar os scripts que queremos. Ao fazer isso, delegamos ao Husky as tarefas de lidar com o gerenciamento do ciclo de vida do git, gerar os hooks e determinar em que ponto do ciclo nossos scripts serão executados. O husky também permite que esses hooks sejam versionados no repositório. Vamos então instalar o Husky em um repositório exemplo, preparando-o para nossa automatização: 

```bash 
npx husky-init && npm install       # se preferir npm
npx husky-init && yarn              # caso use Yarn 1
yarn dlx husky-init --yarn2 && yarn # caso use Yarn 2
```

Este comando irá fazer o setup do husky, modificar o arquivo package.json do projeto adicionando o script prepare e criar uma pasta .husky/ na raiz com um hook pre-commit . Por default o instalador define npm test como comando a ser executado neste hook. Para testar rode git commit e perceba que caso exista um script de teste implementado, ele irá ser executado e caso não exista uma mensagem de erro será mostrada.

```bash
> echo 'Error: no test specified'

Error: no test specified
```

Com os hooks habilitados, iremos agora configurar duas outras ferramentas que precisamos: o commitizen e o commitlint.

### Commitizen

O commitizen é uma aplicação de linha de comando (CLI) que tem como principal objetivo definir uma forma de se comprometer as regras para os commits. Ele oferece um prompt de comando customizável e acelera o processo de escrita do commit, garantindo que este estará no formato correto. 

Para instalar o commitzen rode o comando: yarn global add commitizen. Ele permite definirmos diferentes ***"adapters”*** para o prompt. Com o cli instalado, vamos inicializar o projeto de modo a utilizar o adapter para convenção dos commits `cz-conventional-changelog`:

```bash 
# usando npm
commitizen init cz-conventional-changelog --save-dev --save-exact

# usando yarn
commitizen init cz-conventional-changelog --yarn --dev --exact
```

Temos o commitizen instalado e pré-configurado, mas ele ainda não está sendo chamado via hook. Vamos então remover o hook `pre-commit` existente e criar um hook para o evento de preparo da mensagem de commit. Rode:

```bash
npx husky add .husky/prepare-commit-msg "npm test" && yarn prepare
```

Substitua `npm test` por `exec < /dev/tty && node_modules/.bin/cz --hook`. Isso irá executar o comando do `cz`. Ao tentar rodar `git commit` agora, o prompt do commitizen será apresentado, permitindo escolher entre opções do adapter `cs-conventional-changelog`.

Facilitamos a escrita do commit com o CLI, agora precisamos validar o resultado construido para garantir que tudo está de fato correto. Entra em cena o commitlint.

### Commitlint

O commitlint é um linter para mensagens de commit. Ele nos ajuda a aderir a uma convenção qualquer de commit, permitindo a criação e consumo de convenções via dependências. Vamos instalar o commitlint via:

```bash
# yarn
yarn global add @commitlint/cli 

# npm
npm install -g @commitlint/cli
```

Podemos efetuar um teste rápido do comando com `echo 'foo' | commitlint` . O linter irá reclamar que não temos nenhuma regra configurada.

Vamos adicionar ao projeto a regra para especificação convencional, que é tb o padrão que adotamos no adapter do commitizen. Para isso instale `yarn add -D @commitlint/config-conventional`. Vamos precisar também de um arquivo de configuração `.commitlintrc` na raiz do projeto onde definiremos qual regra será usada na validação:

```json
// .commitlintrc

{
  "extends": [
    "@commitlint/config-conventional"
  ]
}
```

Finalmente podemos criar um novo hook, dessa vez no evento de commit. Para isso rode:

```bash 
npx husky add .husky/commit-msg "npm test" && yarn prepare
```

Substitua `npm test` por `npx --no-install commitlint --edit`. Isso executará o lint no commit preparado pelo commitzen. Caso existam erros o commit será abortado.Com isso conseguimos garantir que commits sejam enviados pro repositório seguindo um padrão e ferramentas de apoio nos ajudam a mantê-lo. Existem outras tarefas no dia a dia de trabalho que podem ser automatizadas via hooks, a padronização de commits é apenas uma. Verificações de integridade do código, formação, testes unitários e outras tarefas podem e devem ser pre-configuradas em diferentes estágios.



***Links uteis:***   

