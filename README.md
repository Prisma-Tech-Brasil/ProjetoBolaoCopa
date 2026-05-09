# ProjetoBolaoCopa
Atividade que abrange os três pilares do desenvolvimento web: estruturação (HTML), estilização (CSS) e lógica de dados/manipulação de DOM (JavaScript), para a criação de um Bolão temático com a Copa do Mundo 2026.


# Exercício: Simulador de Bolão - Copa do Mundo

### **Objetivo**

Desenvolver uma aplicação web onde usuários possam palpitar sobre os jogos da fase de grupos e um administrador possa validar os resultados reais, calculando automaticamente a pontuação dos participantes.

---

### **1. Estrutura de Dados (JSON)**

Você receberá um arquivo `grupos.json` contendo a lista de seleções e os confrontos de cada grupo. Seu primeiro desafio será consumir esses dados via **Fetch API** para renderizar os campos de palpite na tela.

---

### **2. Requisitos Funcionais**

#### **A. Sistema de Perfis**

O site deve alternar entre duas visões (pode ser um simples "toggle" ou abas):

* **Perfil Usuário:** Consegue visualizar os jogos e digitar seus palpites (ex: Brasil 2 x 1 Sérvia).
* **Perfil Administrador:** Consegue inserir os **resultados oficiais** das partidas após o apito final.

#### **B. Regras de Pontuação**

O sistema deve comparar o palpite do usuário com o resultado do administrador e somar os pontos seguindo esta lógica:

* **Acertar o vencedor ou empate:** +1 ponto.
* **Acertar os gols de um time (individual):** +1 ponto por time.
* **Acertar o placar exato (Bônus):** +2 pontos extras.

*Exemplo: Palpite (2x1) | Resultado Real (2x1) = 1 (vencedor) + 1 (gols time A) + 1 (gols time B) + 2 (bônus) = **5 pontos**.*

---

### **3. Requisitos Técnicos (O que usar)**

* **HTML5:** Uso de tags semânticas e inputs do tipo `number` para os gols.
* **CSS3:** Layout responsivo (Flexbox ou Grid). Use cores que remetam ao evento.
* **JavaScript:**
* **Fetch API:** Para ler o arquivo JSON.
* **Local Storage:** Para salvar os palpites do usuário e os resultados do ADM, garantindo que os dados não sumam ao atualizar a página.
* **Manipulação de DOM:** Para criar os cards dos jogos dinamicamente.
* **Lógica de Condicionais:** Para o cálculo matemático da pontuação.

---

### **4. Desafios Extras (Opcional)**

1. **Ranking:** Criar uma tabela que mostre o total de pontos acumulados.
2. **Validação:** Impedir que o usuário envie palpites vazios ou números negativos.
3. **Estilização Dinâmica:** Mudar a cor do card do jogo (Verde para acerto, Amarelo para acerto parcial, Vermelho para erro) após o ADM postar o resultado.

---

### **Dica: Tabela de Referência de Pontos**

| Palpite | Placar Real | Explicação | Total |
| --- | --- | --- | --- |
| 2 x 0 | 2 x 0 | Acertou tudo (Vencedor + 2 gols exatos + Bônus) | **5 pts** |
| 2 x 1 | 1 x 0 | Acertou apenas o vencedor | **1 pt** |
| 1 x 1 | 1 x 1 | Acertou empate + 2 gols exatos + Bônus | **5 pts** |
| 3 x 0 | 2 x 0 | Acertou vencedor + gols de um time | **2 pts** |
| 0 x 0 | 1 x 1 | Acertou apenas o empate | **1 pt** |
