# Guia de Solução do Projeto

## Passo 1: Preparação da Estrutura (HTML Semântico)

Antes de tudo, crie a "casca" da aplicação. O foco aqui é organização.

1. **Cabeçalho (`<header>`)**: Coloque o título do projeto e, muito importante, os **botões de alternância** (Toggle) entre "Modo Usuário" e "Modo Administrador".
2. **Container Principal (`<main>`)**: Crie uma `div` ou `section` vazia com um `id` (ex: `container-jogos`). É aqui que o JavaScript vai "injetar" os cards dos jogos.
3. **Área de Resultados (`<section>`)**: Um espaço para exibir a pontuação total do usuário.
4. **Tags Chave**:
* `<template>`: (Opcional, mas avançado) Para definir a estrutura de um card de jogo.
* `<input type="number">`: Para os campos de gols (bloqueie números negativos no HTML com `min="0"`).
* `<button>`: Para salvar os palpites ou resultados.

---

## Passo 2: Estilização e Layout (CSS)

Deixe o visual pronto para receber os dados.

1. **Layout de Grid/Flexbox**: Defina como os cards dos jogos serão exibidos (ex: uma grade de 3 colunas para desktop e 1 coluna para mobile).
2. **Estilo dos Cards**: Crie classes para os estados dos jogos:
* Uma classe padrão.
* Classes de feedback: `.acerto-total`, `.acerto-parcial`, `.erro`.


3. **Visibilidade**: Crie uma classe `.hidden { display: none; }` para esconder elementos do Administrador quando o Usuário estiver logado e vice-versa.

---

## Passo 3: Consumo de Dados (JavaScript - Fetch)

Agora a mágica começa.

1. **Fetch API**: Crie uma função `async` para ler o arquivo `grupos.json`.
2. **Renderização Dinâmica**:
* Use um loop (`forEach` ou `map`) para percorrer os grupos e jogos.

### 3.1 Mapeamento da Estrutura do JSON

Primeiro, entenda como os dados estão organizados. 
* Um objeto principal com chaves para cada grupo ("Grupo A", "Grupo B").
* Dentro de cada grupo, um array com 4 seleções.

### 3.2 A Lógica de Geração de Jogos (JavaScript)

Após fazer o `fetch` e obter o objeto dos grupos, você precisará de uma função que transforme "Lista de Países" em "Lista de Confrontos".

1. **Iterar sobre os Grupos**: Use um `for...in` ou `Object.entries()` para percorrer cada grupo do JSON.
2. **Algoritmo de Combinação**: Para cada grupo, você deve garantir que todos joguem contra todos (em um grupo de 4, são 6 jogos).
* Use dois loops `for` aninhados.
* O primeiro loop seleciona o `País A`.
* O segundo loop começa a partir do próximo país da lista para selecionar o `País B`.
* *Exemplo lógico:* Se o grupo tem [Brasil, Suíça, Sérvia, Camarões], o loop vai gerar:
1. Brasil x Suíça
2. Brasil x Sérvia
3. Brasil x Camarões
4. Suíça x Sérvia... e assim por diante.

### 3.3 **Criação do Objeto de Jogo**: 

Para cada combinação encontrada, crie um objeto ou elemento no DOM que contenha:
* Um ID único (ex: `grupoA-jogo1`).
* Nome do Time 1 e Nome do Time 2.

* Para cada jogo, use `createElement` ou `innerHTML` para criar o card com os nomes das seleções e os campos de input.
* **Dica de Ouro**: Adicione um atributo `data-id` em cada card ou input para saber exatamente a qual jogo aquele palpite pertence.

---

## Passo 4: Persistência (Local Storage)

Para os dados não sumirem ao dar F5:

1. **Salvar Palpites**: Crie um evento de `click` no botão de "Salvar". Pegue todos os valores dos inputs e salve-os em um objeto ou array no `localStorage` usando `JSON.stringify()`.
2. **Carregar Dados**: Ao abrir a página, verifique se existem dados no `localStorage`. Se sim, preencha os inputs automaticamente com `JSON.parse()`.

---

## Passo 5: A Lógica do Administrador

O administrador funciona quase igual ao usuário, mas ele define a "Verdade".

1. **Toggle de Perfil**: Ao clicar no botão "Admin", use JS para trocar a classe dos cards ou mostrar os inputs de "Resultado Oficial".
2. **Salvar Oficial**: Salve esses resultados em uma chave separada no `localStorage` (ex: `resultados_oficiais`).

---

## Passo 6: O Coração do Projeto (Cálculo de Pontos)

Crie uma função `calcularPontuacao()` que deve ser disparada sempre que o Admin salvar um resultado ou quando a página carregar.

1. **Comparação**:
* Recupere o `Palpite do Usuário` e o `Resultado Real`.
* **Lógica do Vencedor**: Verifique quem ganhou (Time A, Time B ou Empate) em ambos os placares. Se coincidirem: `+1 ponto`.
* **Lógica Individual**: Se `palpiteA === realA`, `+1`. Se `palpiteB === realB`, `+1`.
* **Bônus**: Se `palpiteA === realA` **E** `palpiteB === realB`, `+2`.


2. **Exibição**: Atualize o texto do HTML com o total somado de todos os jogos.

---

## Ordem Sugerida de Comandos JS para Pesquisar:

* `fetch().then()` ou `async/await`
* `document.querySelector()` e `document.getElementById()`
* `localStorage.setItem()` e `localStorage.getItem()`
* `addEventListener('click', ...)` e `addEventListener('input', ...)`
* `element.classList.toggle()` (para trocar de usuário para admin)

---

### Dica para o Desafio Extra (Cores Dinâmicas):

Dentro da sua função de cálculo, use um `if/else` para verificar a pontuação de cada card. Se a pontuação do card for 5, adicione a classe CSS verde; se for entre 1 e 4, amarelo; se for 0, vermelho.
