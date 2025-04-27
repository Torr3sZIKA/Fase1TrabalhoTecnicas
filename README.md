# Fase1 - Trabalho de Técnicas de Desenvolvimento de Vídeojogos
🔧 Trabalho realizado por: 
* Guilherme Torres nº31486
* Diogo Gomes
<h3>📦 Repositório original: https://github.com/MonoGame/MonoGame.Samples/tree/3.8.2/Platformer2D</h3>

O jogo "Platformer2D" não é nada mais, nada menos, do que um exemplo oficial da equipa MonoGame para demonstrar como criar um jogo de plataforma 2D usando a framework da mesma! 
O jogo contem inimigos, níveis e coletáveis como por exemplo, joias.


# ✨ Funcionalidades
* Mecânicas básicas de plataforma: correr, saltar e colisões.
* Animações de personagem.
* Sistema simples de pontuação.
* Sistema de níveis.
* Exemplo de utilização de SpriteBatch e ContentManager.

<h3>🌟 Mecânicas básicas de plataforma: correr, saltar e colisões:</h3>

<h3>1. 🏃‍♂️ Correr</h3>
<ul>
    <li><strong>Funções:</strong> <code>GetInput()</code> e <code>ApplyPhysics()</code></li>
    <li>Lê teclado, comando ou acelerómetro e define o movimento (<code>movement</code>).</li>
    <li>Aplica aceleração e atrito (<code>GroundDragFactor</code> e <code>AirDragFactor</code>).</li>
</ul>

<h3>2. 🕴️ Saltar</h3>
<ul>
    <li><strong>Funções:</strong> <code>GetInput()</code> e <code>DoJump()</code></li>
    <li>Controla o impulso no eixo Y baseado no tempo que o botão de salto é pressionado (<code>jumpTime</code>).</li>
    <li>O salto só acontece se o jogador estiver no chão (<code>IsOnGround</code>).</li>
</ul>

<h3>3. 🧱 Colisões</h3>
<ul>
    <li><strong>Função:</strong> <code>HandleCollisions()</code></li>
    <li>Deteta colisões com os tiles do mapa (<code>TileCollision</code>).</li>
    <li>Empurra o jogador para fora dos tiles para evitar sobreposição e detecta se está no chão.</li>
</ul>

<h3>📋 Resumindo</h3>

<table>
<thead>
<tr>
<th>Mecânica</th>
<th>Funções no Código</th>
<th>O que faz</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Correr</strong></td>
<td><code>GetInput()</code>, <code>ApplyPhysics()</code></td>
<td>Lê esquerda/direita → aplica força → cumpre o movimento</td>
</tr>
<tr>
<td><strong>Saltar</strong></td>
<td><code>GetInput()</code>, <code>DoJump()</code></td>
<td>Deteta salto → impulsiona o jogador no eixo Y</td>
</tr>
<tr>
<td><strong>Colidir</strong></td>
<td><code>HandleCollisions()</code></td>
<td>Deteta colisões com o mundo → ajusta a posição</td>
</tr>
</tbody>
</table>

<h3>🌟 Animações de personagem:</h3>

<table>
  <thead>
    <tr>
      <th>Função</th>
      <th>Classe</th>
      <th>O que faz?</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>PlayAnimation(Animation animation)</code></td>
      <td><code>AnimationPlayer</code></td>
      <td>Inicia ou muda uma animação (ex: mudar de "parado" para "a correr").</td>
    </tr>
    <tr>
      <td><code>Draw(GameTime gameTime, SpriteBatch spriteBatch, Vector2 position, SpriteEffects spriteEffects)</code></td>
      <td><code>AnimationPlayer</code></td>
      <td>Atualiza o frame atual com o tempo (<code>time</code>) e desenha o frame certo da animação na tela.</td>
    </tr>
  </tbody>
</table>

<h3>📌 O processo:</h3>
<ul>
  <li><strong>PlayAnimation()</strong> é chamada para começar ou trocar uma animação.</li>
  <li><strong>Draw()</strong> é chamada a cada frame do jogo para:
    <ul>
      <li>Atualizar qual frame da animação deve ser mostrado (baseado no tempo).</li>
      <li>Desenhar o frame correto na posição certa do personagem.</li>
    </ul>
  </li>
</ul>

<h3>⚡ Relembrar:</h3>
<ul>
  <li>A classe <code>Animation</code> apenas <strong>guarda os dados</strong> da animação (imagem, tempo entre frames, se repete ou não).</li>
  <li>A classe <code>AnimationPlayer</code> é <strong>quem realmente faz as animações acontecerem</strong>.</li>
</ul>


<h3>🌟 Sistema simples de pontuação:</h3>

No código da classe <code>Gem</code>, a pontuação é atribuída pelo valor da pedra preciosa que o jogador apanha. O valor de cada pedra preciosa é armazenado na propriedade <code>PointValue</code>, que define a quantidade de pontos que o jogador ganha ao apanhar-la.

<pre><code>public readonly int PointValue = 30;</code></pre>

<p>O valor de <code>PointValue</code> é atualmente definido como 30 pontos. Quando a pedra preciosa é apanhada, ela "chama" o método <code>OnCollected()</code>, mas a lógica para adicionar os pontos ao jogador ainda não está implementada dentro da classe <code>Gem</code>.</p>

<p>Para implementar a lógica de pontuação, seria necessário atualizar o método <code>OnCollected()</code> para integrar com a classe do jogador ou outra classe responsável pela pontuação. Um exemplo de como poderiamos fazer seria o seguinte:</p>

<pre><code>
public void OnCollected(Player collectedBy)
{
    collectedSound.Play();

    // Adiciona os pontos ao jogador
    collectedBy.AddPoints(PointValue);
}
</code></pre>

<p>Neste exemplo, o jogador é passado como parâmetro para o método <code>OnCollected()</code>. Dentro do método, chama-se a função <code>AddPoints()</code> no objeto <code>collectedBy</code>, passando o valor da <code>PointValue</code> da gema. A função <code>AddPoints()</code> seria responsável por atualizar a pontuação do jogador.</p>

<p>Portanto, a lógica da pontuação está no valor atribuído à propriedade <code>PointValue</code>, mas a integração com a pontuação do jogador depende da implementação de um sistema de pontuação, que pode ser gerido pela classe <code>Player</code> ou outra classe similar.</p>

<h3>🌟 Sistema de níveis</h3>

<p>A classe <code>Level</code> é responsável pela gestão de um nível de jogo, controlando a estrutura do mapa, os objetos no nível e o estado do jogo. Isso acontece através destas funções:</p>

<table>
  <tr>
    <td><h3>1. <code>Level(IServiceProvider serviceProvider, Stream fileStream, int levelIndex)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Constrói um novo nível a partir de um fluxo de dados de ficheiro (<code>fileStream</code>). Carrega as texturas de fundo, sons e inicia a contagem de tempo.</p>
      <p><strong>Objetivo:</strong> Inicializa o nível com base no índice do nível, carrega o layout de tiles e define o ambiente de jogo.</p>
    </td>
  </tr>
  <tr>
    <td><h3>2. <code>void LoadTiles(Stream fileStream)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Lê os dados de um ficheiro de nível e carrega a estrutura dos tiles.</p>
      <p><strong>Objetivo:</strong> Verifica o formato correto do ficheiro, valida a posição de início e a saída, além de instanciar as entidades do nível (como gemas, inimigos e plataformas).</p>
    </td>
  </tr>
  <tr>
    <td><h3>3. <code>Tile LoadTile(char tileType, int x, int y)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Carrega um tile com base no tipo de caractere lido do ficheiro (por exemplo, '.' para espaço vazio, 'X' para saída, 'G' para gema).</p>
      <p><strong>Objetivo:</strong> Instancia o tile adequado para a posição <code>(x, y)</code> com base no tipo de caractere.</p>
    </td>
  </tr>
  <tr>
    <td><h3>4. <code>Tile LoadStartTile(int x, int y)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Cria o jogador e define a sua posição inicial no nível.</p>
      <p><strong>Objetivo:</strong> Atribui o ponto de início do jogador e adiciona o personagem ao nível.</p>
    </td>
  </tr>
  <tr>
    <td><h3>5. <code>Tile LoadExitTile(int x, int y)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Define a posição de saída do nível.</p>
      <p><strong>Objetivo:</strong> Marca a localização da saída no nível, que o jogador deve alcançar.</p>
    </td>
  </tr>
  <tr>
    <td><h3>6. <code>void Update(GameTime gameTime, KeyboardState keyboardState, GamePadState gamePadState, AccelerometerState accelState, DisplayOrientation orientation)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Atualiza o estado de todos os objetos do nível, incluindo o jogador, inimigos, gemas e o tempo restante.</p>
      <p><strong>Objetivo:</strong> Gerencia o fluxo do jogo, como o tempo, a interação do jogador e as condições de vitória (alcançar a saída) ou derrota (morrer ou esgotar o tempo).</p>
    </td>
  </tr>
  <tr>
    <td><h3>7. <code>void UpdateGems(GameTime gameTime)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Atualiza o estado das gemas e verifica se o jogador as coletou.</p>
      <p><strong>Objetivo:</strong> Verifica se as gemas estão a ser coletadas pelo jogador e atualiza a pontuação.</p>
    </td>
  </tr>
  <tr>
    <td><h3>8. <code>void UpdateEnemies(GameTime gameTime)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Atualiza o estado dos inimigos e verifica se o jogador colide com eles.</p>
      <p><strong>Objetivo:</strong> Garante que os inimigos se movam corretamente e que o jogador seja morto caso colida com um inimigo.</p>
    </td>
  </tr>
  <tr>
    <td><h3>9. <code>void OnGemCollected(Gem gem, Player collectedBy)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Executa ações quando o jogador coleta uma gema.</p>
      <p><strong>Objetivo:</strong> Aumenta a pontuação do jogador e executa qualquer outra lógica relacionada à coleta de gemas.</p>
    </td>
  </tr>
  <tr>
    <td><h3>10. <code>void OnPlayerKilled(Enemy killedBy)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Lida com a morte do jogador.</p>
      <p><strong>Objetivo:</strong> Executa as ações necessárias quando o jogador morre, como reiniciar ou finalizar o nível.</p>
    </td>
  </tr>
  <tr>
    <td><h3>11. <code>void OnExitReached()</code></h3></td>
    <td>
      <p><strong>Função:</strong> Executa ações quando o jogador atinge a saída do nível.</p>
      <p><strong>Objetivo:</strong> Marca a vitória do jogador, toca o som de vitória e permite que o jogador avance para o próximo nível.</p>
    </td>
  </tr>
  <tr>
    <td><h3>12. <code>void StartNewLife()</code></h3></td>
    <td>
      <p><strong>Função:</strong> Restaura o jogador à posição inicial para tentar o nível novamente.</p>
      <p><strong>Objetivo:</strong> Reinicia o nível após a morte do jogador, permitindo que ele recomece o jogo.</p>
    </td>
  </tr>
  <tr>
    <td><h3>13. <code>void Draw(GameTime gameTime, SpriteBatch spriteBatch)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Desenha todos os elementos do nível, incluindo o fundo, os tiles, gemas, inimigos e o jogador.</p>
      <p><strong>Objetivo:</strong> Renderiza a tela do jogo, organizando as camadas de fundo, o nível de tiles, os inimigos e o jogador.</p>
    </td>
  </tr>
  <tr>
    <td><h3>14. <code>TileCollision GetCollision(int x, int y)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Obtém o tipo de colisão de um tile específico.</p>
      <p><strong>Objetivo:</strong> Retorna o tipo de colisão (por exemplo, passável, impassável) para a posição <code>(x, y)</code>.</p>
    </td>
  </tr>
  <tr>
    <td><h3>15. <code>Rectangle GetBounds(int x, int y)</code></h3></td>
    <td>
      <p><strong>Função:</strong> Obtém as dimensões de um tile em espaço de mundo.</p>
      <p><strong>Objetivo:</strong> Calcula as dimensões de um tile baseado na sua posição <code>(x, y)</code>.</p>
    </td>
  </tr>
</table>

<h3>🌟 Utilização de <code>SpriteBatch</code> e <code>ContentManager</code> no Platformer2D</h3>

<h3>SpriteBatch</h3>
<p>
O <code>SpriteBatch</code> é utilizado para desenhar texturas na tela de forma eficiente. No projeto <strong>Platformer2D</strong>, ele é criado e usado em vários pontos:
</p>
<ul>
  <li><strong>PlatformerGame.cs</strong>: criado no método <code>LoadContent</code> para desenhar o cenário, o jogador e a interface (HUD).</li>
  <li><strong>Level.cs</strong>: passado para as classes <code>Player</code>, <code>Enemy</code> e <code>Gem</code> para desenhar os seus respetivos sprites no método <code>Draw</code>.</li>
  <li><strong>Gem.cs</strong>, <strong>Enemy.cs</strong> e <strong>Player.cs</strong>: usados nos métodos <code>Draw</code> para renderizar as texturas dos objetos no jogo.</li>
</ul>

<h3>ContentManager</h3>
<p>
O <code>ContentManager</code> é responsável por carregar os recursos do jogo, como texturas, fontes e sons. No projeto <strong>Platformer2D</strong>:
</p>
<ul>
  <li><strong>PlatformerGame.cs</strong>: inicializa o <code>ContentManager</code> e carrega conteúdos principais como a fonte usada na HUD.</li>
  <li><strong>Level.cs</strong>: utilizado para carregar as texturas dos tiles, inimigos, gemas e sons, através do método <code>Content.Load&lt;T&gt;</code>.</li>
  <li><strong>Player.cs</strong> e <strong>Enemy.cs</strong>: carregam as suas próprias animações usando o <code>ContentManager</code> associado ao nível (<code>Level.Content</code>).</li>
</ul>

<h3>Exemplos de Código</h3>

<pre>
<!-- SpriteBatch criação -->
spriteBatch = new SpriteBatch(GraphicsDevice);

<!-- SpriteBatch uso -->
spriteBatch.Begin();
level.Draw(gameTime, spriteBatch);
spriteBatch.End();

<!-- ContentManager carregamento -->
_texture = Content.Load&lt;Texture2D&gt;("Sprites/Player");
_soundEffect = Content.Load&lt;SoundEffect&gt;("Sounds/GemCollected");
</pre>

<p>
Estes dois componentes são fundamentais para o funcionamento do motor gráfico do Platformer2D.
</p>

<h1>📦 Requisitos</h1>
<ul>
    <li>MonoGame 3.8.2</li>
    <li>.NET SDK 6.0+</li>
    <li>IDE recomendada: Visual Studio 2022</li>
</ul>

<h1>📂 Estrutura do projeto</h1>

<code>Platformer2D/
├── Content/              # Assets do jogo (texturas, fontes, sons)
├── Screens/              # Diferentes partes do jogo (Menu, Gameplay, etc.)
├── Tiles/                # Implementação de tiles e colisões
├── Game1.cs              # Classe principal do jogo
├── Program.cs            # Ponto de entrada do programa
├── Platformer2D.csproj   # Arquivo do projeto
└── README.md             # Ficheiro README
</code>

<h1>🎮 Como jogar?</h1>
<ul>
    <li>Seta Esquerda/Direita: Mover personagem </li>
    <li>Espaço: Saltar</li>
    <li>ESC: Sair do jogo</li>
</ul>











