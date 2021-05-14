# Aula 07 - Rastreabilidade e Governança

## Exercício

Neste exercício vamos praticar conceitos de proteção de branches, regras de aprovação e validações obrigatórias de pull requests.

### 0. Faça o fork deste repositório para a sua conta pessoal

Edite a linha **2** do arquivo `Dockerfile` para que a URL do label aponte para o seu repositório pessoal

### 1. Introduzindo uma mudança na aplicação

1. Crie um novo branch chamado `novo-background`
2. Na pasta `public` adicione este arquivo [coffe.jpg](https://github.com/pedrolacerda/aula-07-governanca/blob/novo-background/public/coffee.jpg) (via upload ou commit)
3. Na pasta **public**, edite o arquivo `style.css`, na linha **145**.

```css
background: url("coffee.jpg") left bottom;
```

4. Volte para a tela inicial do seu repositório, clique em `Compare & pull request` e crie o PR

#### :question: Mas como podemos garantir que as modificações propostas só vão estar no branch `main` com as validações e aprovações necessárias?

### 2. Configurando status obrigatórios no workflow ("status checks")

Do jeito que nosso workflow está, caso o build falhasse, seria possível fazer o merge de código quebrado no branch principal.

Vamos configurar qual(is) os status vindos do nosso pipeline deve obrigatoriamente passar antes de ser possível fazer o merge. Fazemos isso via proteção de branches (_"branch protection"_)

💡 Dica: Imagine que as regras de proteção de branches vão impedir que certas operações de Git (merge, por exemplo) sejam executadas até que determinadas condições mínimas sejam atendidas.

1. Vá em `Settings` > `Branches`
2. Na seção **Branch protection rules**, clique em `Add rule`
3. No campo **Branch protection name patttern** insira: `main`
4. Clique `Require status checks to pass before merging`
5. Clique `Require branches to be up to date before merging`
6. Selecione `build` e `build-container`
7. Clique `Create`

<!-- Demonstrar o que acontece caso um branch esteja desatualizado -->

#### :question: O que mudou no seu PR?

### 3. Configurando revisões de código

Como vimos em outras aulas, revisões de código são uma parte fundamental de um processo de desenvolvimento de software bem estruturado. Eles adicionam qualidade, uma vez que trazem diferentes perspectivas e experiências para o código sendo desenvolvido. Mas também servem como uma ferramenta de governança importante, uma vez que definem as regras de negócio a respeito das alçadas de aprovações.

1. Ainda na parte de **regra de proteção de branch**, clique em `Require pull request reviews before merging`
2. Configure `Required approving reviews` para **2**
3. Marque `Dismiss stale pull request approvals when new commits are pushed`
4. Marque `Require review from Code Owners`
5. Clique `Save changes`

#### :question: O que mudou no seu PR (2)?

:bulb: Agora nosso PR não pode ser _mergeado_ ao main (opção possível apenas usando privilégios de admin). Se clicarmos em `Reviewers` vamos ver que também não conseguimos adicionar nenhum revisor. **Por quê?**

#### Vamos adicionar nossos colegas de turma?

### 4. Configurando CODEOWNERS

O que é esse tal de Code Owners? São literalmente pessoas ou equipes responsáveis por determinada parte do código. Definindo Code Owners podemos definir regras de negócio para a revisão de código. Essas regras são definidas em um arquivo chamado `CODEOWNERS` que deve ficar na raíz do projeto, na pasta `docs/` ou na pasta `.github/`.

Um template de arquivo `CODEOWNERS` pode ser encontrado [aqui](https://github.com/pedrolacerda/aula-07-governanca/blob/codeowners/.github/CODEOWNERS).

1. Vá para o branch `main`
2. Crie um arquivo chamado `CODEOWNERS` na pasta `.github`
3. Copie e cole o conteúdo [deste aquivo](https://github.com/pedrolacerda/aula-07-governanca/blob/codeowners/.github/CODEOWNERS)

:question: Como você alteraria esse arquivo para que alguns de seus colegas fossem requisitados a revisar código do PR?

<!-- navegar e mostrar o ícone do Codeowners no PR e no arquivo -->

1. Mude novamente para o branch `novo-background`
2. Navegue para o arquivo `views/index.pug`
3. Edite as linhas **8 e 9** para que elas tenham o seguinte conteúdo

```pug
        h3 Making the Worst
        h1 Coffee For Devs
```

:question: Como poderíamos alterar nosso arquivo `CODEOWNERS` para definir responsáveis para revisar alterações desse tipo?
<!-- Explicar que podemos definir a regra para o arquivo específico, para esse tipo de arquivo ou para a pasta -->

### 5. E o que mais?

1. Obrigatório commits assinados
2. Obrigatório histórico linear
3. Incluir administradores sob as regras
4. Permitir _force pushes_
5. Permitir deleções

<!-- Porque nosso workflow dá erro?-->
