# nlw-heat-origin
Projeto NLW Heat - Trilha Origin

## Anotações

### Javascript

- **Alterar o valor de uma tag usando um ID:**

```html
<h1 id="userName">Nome do Usuário</h1>
```

```js
document.getElementById('userName').textContent = 'Novo Nome'

// ou

userName.textContent = 'Novo Nome'
```

Essas funções tambem retornam o valor atribuído:

```js
let novoNome = (userName.textContent = 'Novo Nome')

console.log(novoNome) // Novo Nome
```

Essa mudança também pode ser feita usando `.innerHTML`, a diferença é:

> - `.textContent` altera apenas o conteúdo textual. Se receber "\<b>Nome\</b>", vai mostrar "\<b>Nome\</b>". É mais rápido.
> - `.innerHTML` espera receber um conteúdo em HTML que será interpretado, portanto é mais lento. Se receber "\<b>Nome\</b>", vai mostrar "<b>Nome</b>". É mais rápido.

<br>

- **Acessando valores de tags e filhos:**

Usar o `id` com o "método" `.children`, pode-se então acessar os filhos passando um index como se fosse uma array.

```html
<ul id="socialMediaLinks">
  <li class="youtube">
    <a href="https://www.youtube.com/"> Youtube </a>
  </li>
  <li class="instagram">
    <a href="https://www.instagram.com/"> Instagram </a>
  </li>
</ul>
```

```js
function changeSocialMediaLinks() {
  for (let li of socialMediaLinks.children) {
    let classeDaTag = li.getAttribute('class')
    li.children[0].href = `https://www.link.com`
  }
}
```

<br>

- **Consumindo a API do github:**

Passar a url para `fetch(url)` que armazenará a resposta da API. `.then` recebe esses dados e, usando uma função anônima de flecha (_arrow function_), transforma em JSON usando `.json()`. Finalmente, pode-se acessar os dados com notação de ponto (ex: `data.name`).

```js
function getGithubProfileInfo() {
  const url = `https://api.github.com/users/${linksSocialMedia.github}`

  fetch(url)
    .then(response => response.json())
    .then(data => {
      userName.textContent = data.name
      userBio.textContent = data.bio
      userLink.href = data.html_url
      userImage.src = data.avatar_url
      userLogin.textContent = data.login
    });
}
