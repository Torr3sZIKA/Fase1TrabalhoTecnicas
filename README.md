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
* Sistema simples de pontuação e de moedas.
* Exemplo de utilização de SpriteBatch e ContentManager.

<h3>Mecânicas básicas de plataforma: correr, saltar e colisões:</h3>

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

<h3>Animações de personagem:</h3>

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

