# Banco Senac — ADO 2

Aplicação web de abertura de conta digital desenvolvida como atividade do Banco Senac. O projeto reúne a interface do repositório `banco-senac-front` com a implementação da ADO 2, incluindo validações de formulário por expressões regulares e envio assíncrono para a API.

## Site publicado

Após a ativação do GitHub Pages, a aplicação estará disponível em:

<https://doglatfpn.github.io/banco-senac-ado2/>

## Funcionalidades

- navegação entre login, cadastro, confirmação e painel do cliente;
- login demonstrativo com clientes armazenados em memória;
- reconhecimento do último usuário por cookies;
- salvamento automático do rascunho de cadastro no `localStorage`, com expiração;
- descarte manual do rascunho;
- mensagens de erro na interface e foco automático no campo inválido;
- cadastro enviado como JSON por `fetch` com `async/await`;
- layout responsivo e identidade visual do Banco Senac.

## Validações do cadastro

O formulário valida os valores com o método `RegExp.test()` antes de realizar qualquer requisição:

| Campo | Regra |
| --- | --- |
| Nome completo | Duas ou mais palavras, aceitando letras com acentos e espaços |
| CPF | `000.000.000-00` ou 11 dígitos contínuos |
| E-mail | Endereço com usuário, `@`, domínio e extensão |
| Celular | 11 dígitos, com parênteses, espaço e hífen opcionais |
| CEP | `00000-000` ou 8 dígitos contínuos |
| Senha | Mínimo de 8 caracteres, com minúscula, maiúscula e número |
| Confirmação | Deve ser exatamente igual à senha |

Quando uma regra falha, o envio é interrompido, a mensagem aparece em `#cadastro-erro` e o foco é direcionado ao campo correspondente.

## Integração com a API

Os cadastros aprovados pelas validações são enviados em JSON para:

```text
POST https://senac-bank-api.dennislopes.com.br/api/clientes
```

A aplicação aguarda a resposta com `async/await`. Em caso de sucesso, limpa o rascunho e abre a tela de confirmação; em caso de erro, informa o problema na própria interface.

## Executar localmente

Como o projeto usa apenas HTML, CSS e JavaScript, basta servir esta pasta com um servidor HTTP estático. Exemplos:

```bash
npx serve .
```

ou usar a extensão Live Server do VS Code. Abrir o arquivo diretamente também exibe a interface, mas um servidor local reproduz melhor o comportamento do GitHub Pages.

## Credenciais demonstrativas

Para testar o painel sem cadastrar um novo cliente:

```text
CPF: 111.222.333-44
Senha: 123
```

## Estrutura

```text
.
├── index.html       # Estrutura das telas e formulário
├── script.js        # Navegação, persistência, Regex e integração com a API
├── style.css        # Estilos e responsividade
├── senac-logo.png   # Identidade visual
└── .nojekyll        # Publicação estática direta no GitHub Pages
```

## Tecnologias

- HTML5
- CSS3
- JavaScript
- Fetch API
- Web Storage e cookies
- GitHub Pages


