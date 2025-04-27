# Fase1 - Trabalho de Técnicas de Desenvolvimento de Vídeojogos
🔧 Trabalho realizado por: 
* Guilherme Torres nº31486
* Diogo Gomes
<h3>📦 Repositório original: https://github.com/MonoGame/MonoGame.Samples/tree/3.8.2/Platformer2D</h3>

O jogo "Platformer2D" não é nada mais, nada menos, do que um exemplo oficial da equipa MonoGame para demonstrar como criar um jogo de plataforma 2D usando a framework da mesma! 
O jogo contem inimigos, níveis e coletáveis como por exemplo, joias.


# ✨ Funcionalidades
* Mecânicas básicas de plataforma: correr, saltar e colisões.
* Detecção de colisões com o ambiente.
* Animações de personagem.
* Sistema simples de pontuação e recoleção de moedas.
* Exemplo de utilização de SpriteBatch e ContentManager.

<h3>Mecânicas básicas de plataforma: correr, saltar e colisões:</h3>
<b>Correr:</b>
Função:
+GetInput(...) → lê o teclado/gamepad para ativar isJumping = true
+DoJump(...) → altera velocity.Y se o jogador está a saltar



if (isJumping)
{
    if ((!wasJumping && IsOnGround) || jumpTime > 0.0f)
    {
        if (jumpTime == 0.0f)
            jumpSound.Play();

        jumpTime += (float)gameTime.ElapsedGameTime.TotalSeconds;
        sprite.PlayAnimation(jumpAnimation);
    }

    if (0.0f < jumpTime && jumpTime <= MaxJumpTime)
    {
        velocityY = JumpLaunchVelocity * (1.0f - (float)Math.Pow(jumpTime / MaxJumpTime, JumpControlPower));
    }
    else
    {
        jumpTime = 0.0f;
    }
}
else
{
    jumpTime = 0.0f;
}
wasJumping = isJumping;
