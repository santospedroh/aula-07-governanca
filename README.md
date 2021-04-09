# Aula 07 - Rastreabilidade e Governança

## Exercício

Neste exercício vamos praticar conceitos de proteção de branches, regras de aprovação e validações obrigatórias de pull requests.

### 0. Forke este repositório para a sua conta pessoal

Edite a linha **2** do arquivo `Dockerfile` para que a URL do label aponte para o seu repositório pessoal

### 1. Adicionando um novo background

1. Crie um novo branch chamado `novo-background`
2. Na pasta `public` adicione este arquivo [coffe.jpg](https://github.com/pedrolacerda/aula-07-governanca/blob/novo-background/public/coffee.jpg) (via upload ou commit)
3. Na pasta **public**, edite o arquivo `style.css`, na linha **154**.

```css 
background: url("coffee.jpg") left bottom;
```

#### :question: Mas como podemos garantir que as modificações propostas só vão estar no branch main com as validações e aprovações necessárias?
