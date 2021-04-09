# Aula 07 - Rastreabilidade e Governança

## Exercício

Neste exercício vamos praticar conceitos de proteção de branches, regras de aprovação e validações obrigatórias de pull requests.

### 0. Faça o fork deste repositório para a sua conta pessoal

Edite a linha **2** do arquivo `Dockerfile` para que a URL do label aponte para o seu repositório pessoal

### 1. Introduzindo uma mudança na aplicação

1. Crie um novo branch chamado `novo-background`
2. Na pasta `public` adicione este arquivo [coffe.jpg](https://github.com/pedrolacerda/aula-07-governanca/blob/novo-background/public/coffee.jpg) (via upload ou commit)
3. Na pasta **public**, edite o arquivo `style.css`, na linha **154**.

```css
background: url("coffee.jpg") left bottom;
```

4. Volte para a tela inicial do seu repositório, clique em `Compare & pull request` e crie o PR

#### :question: Mas como podemos garantir que as modificações propostas só vão estar no branch `main` com as validações e aprovações necessárias?

Do jeito que nosso workflow está, caso o build falhasse, seria possível fazer o merge de código quebrado no branch principal.

### 2. Configurando status obrigatórios no workflow ("status checks")

Vamos configurar qual(is) os status vindos do nosso pipeline deve obrigatoriamente passar antes de ser possível fazer o merge. Fazemos isso via proteção de branches (_"branch protection"_)

💡 Dica: Imagine que as regras de proteção de branches vão impedir que certas operações de Git (merge, por exemplo) sejam executadas até que determinadas condições mínimas sejam atendidas.

1. Vá em `Settings` > `Branches`
2. Na seção **Branch protection rules**, clique em `Add rule`
3. No campo **Branch protection name patttern** insira: `master`
4. Clique `Require status checks to pass before merging`
5. Clique `Require branches to be up to date before merging`
6. Selecione `build` e `build-container`
7. Clique `Create`

#### :question: O que mudou no seu PR?
