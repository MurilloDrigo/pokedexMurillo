# Pokémon Search App

Este é um aplicativo de busca de Pokémons construído com Vue.js 3, que permite aos usuários pesquisar Pokémons por nome, número ou tipo. O app também exibe detalhes do Pokémon selecionado, como estatísticas e evoluções.

## Tecnologias Utilizadas

- **Vue.js 3**: Framework JavaScript progressivo.
- **PokeAPI**: API pública usada para obter dados sobre Pokémons.
- **TypeScript**: Utilizado para tipagem estática no código Vue.

## Funcionalidades

- Pesquisar Pokémons por nome ou número.
- Filtrar Pokémons por tipo.
- Visualizar detalhes do Pokémon selecionado, como:
  - Nome
  - ID
  - Experiência base
  - Altura
  - Imagem (Sprite)
  - Estatísticas (HP, Ataque, Defesa, Velocidade, etc.)
  - Tipos do Pokémon
- Exibir evoluções do Pokémon selecionado.

## Estrutura do Projeto

### Components

- **CardPokemonSelected.vue**: Exibe detalhes do Pokémon selecionado.
- **ListPokemons.vue**: Lista os Pokémons com base na busca e filtro selecionado.
- **PokemonEvolutions.vue**: Mostra as evoluções do Pokémon.
- **PokemonTypeFilter.vue**: Dropdown para selecionar o tipo de Pokémon.

### Views

- **HomeView.vue**: A principal view do aplicativo, onde os componentes são montados e a lógica de busca e filtragem é realizada.

## Como Rodar o Projeto

### Pré-requisitos

- [Node.js](https://nodejs.org/) (versão 12 ou superior)
- [Vue CLI](https://cli.vuejs.org/)

### Instalação

```sh
git clone https://github.com/seu-usuario/seu-repositorio.git
```

```sh
npm install
```

```sh
npm run dev
```

```sh
npm run build
```