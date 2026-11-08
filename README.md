# Herança da Vovó Milionária

Jogo de tabuleiro para 2 a 4 participantes no mesmo computador ou uma pessoa contra até três adversários do jogo. A IA tem três níveis e funciona no navegador.

## Publicar no GitHub Pages

1. Extraia o ZIP. Crie um repositório público no GitHub, por exemplo `heranca-da-vovo-milionaria`.
2. Envie o conteúdo extraído para a raiz da branch `main`, mantendo `index.html`, `style.css`, `js/` e `assets/` no mesmo nível. Inclua o arquivo vazio `.nojekyll` se estiver visível ou usando Git.
3. No repositório, abra **Settings → Pages**. Em **Source**, selecione **Deploy from a branch**. Escolha **main** e **/(root)**, depois salve.
4. Após a publicação, abra o endereço exibido em **Settings → Pages**.

[Configuração da publicação no GitHub Pages](https://docs.github.com/pt/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

## Tabuleiro e animações

As casas reveladas mostram seu efeito no próprio tabuleiro. No celular, as cinco colunas cabem na largura da tela. Os efeitos aparecem resumidos nas casas reveladas e o dado fica na barra de partida abaixo do tabuleiro. O dado de exploração gira antes de mostrar o resultado e os peões se deslocam passo a passo. O peão com a chave fica maior e recebe um aro dourado.

## Jogar localmente

Na pasta extraída, execute `python3 -m http.server 8000` e acesse [localhost:8000](http://localhost:8000). No Windows, o comando também pode ser `py -m http.server 8000`. Nenhuma dependência JavaScript precisa ser instalada.

## Regras adotadas

- O Hall é sorteado entre os quatro cantos. Só ele começa aberto.
- O maior dado inicial joga primeiro. Os demais seguem em ordem crescente do resultado original. Empates são desfeitos com novas rolagens, com prioridade para o maior resultado entre empatados. Os demais empatados no maior resultado original jogam após os resultados inferiores.
- Um trajeto pode virar, sem repetir casas no mesmo turno. A escolha de um passo precisa permitir que a rolagem seja completada considerando os bloqueios já conhecidos.
- A Faxineira e a Doméstica bloqueiam a casa ao serem reveladas e interrompem o deslocamento principal na casa anterior. Uma parada antecipada não ativa efeitos.
- A escada para subir mantém a direção do último passo. A escada para descer volta à casa anterior. Café e chá permitem um passo ortogonal respeitando a direção proibida. O uso da passagem é opcional. Deslocamentos extras exploram o destino e não encadeiam efeitos de parada.
- O roubo ocorre no último passo da movimentação do dado, inclusive na chegada ao cofre. Nesse caso, o roubo é resolvido antes da vitória.
- Se os bloqueios revelados isolarem um objetivo necessário, a partida termina sem vencedor.
- As espiadas são privadas na interface. No mesmo computador, os outros participantes devem desviar o olhar.

## Arte manual

Os símbolos que acompanham o jogo são provisórios. Digitalize as ilustrações manuais, coloque os arquivos em `assets/` e adicione seus caminhos relativos em `assets/artwork.mjs`. Use os índices de 0 a 24 conforme `js/tiles.mjs`, e `back` para o verso comum. Exemplo: `1: './assets/chave.png'`.

## Arquivos

- `js/game.mjs` implementa tabuleiro, turnos e efeitos.
- `js/tiles.mjs` contém o catálogo de tiles.
- `js/ai.mjs` escolhe movimentos para os adversários do jogo.
- `js/ui.mjs` conecta os controles ao motor.
