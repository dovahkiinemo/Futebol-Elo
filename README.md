# Futebol-Elo  
Automação de cálculo de ratings Elo para o Campeonato Brasileiro, classificação e projeção de resultados.

## 📦 Visão geral  
Este repositório constitui um pipeline para:  
- Ler resultados de jogos do brasileiro (ex: arquivo `jogos_todos_formatados.csv`).  
- Computar o rating Elo de cada time rodada a rodada.  
- Gerar a classificação atual do campeonato.  
- Simular projeções com base em previsões de resultados.  
- Identificar jogos que ainda faltam ocorrer (cada confronto ocorre duas vezes: mando e visita).

## 🗂 Estrutura de diretórios e arquivos  
- `jogos/` - Contém arquivos de jogos formatados.  
- `jogos_todos_formatados.csv` - Dataset completo de todas partidas.  
- `jogos_2025_formatados.csv` - Subconjunto para o ano de 2025.  
- `elo_historico.csv` - Histórico Elo calculado por jogo.  
- `elo_2025.csv` - Elo acumulado para 2025.  
- `classificacao_brasileirao_2025.csv` - Classificação atual da temporada de 2025.  
- `classificacao_brasileirao_2025_projetada.csv` - Classificação projetada com previsões aplicadas.  
- `jogos_faltantes_2025.csv` - Jogos pendentes (mandante/visitante invertido ainda não jogado).  
- `elo_construction.ipynb` & `load_data.ipynb` - Notebooks para processamento interativo.

## 🎯 Funcionalidades principais  
1. **Cálculo de Elo**  
   - Cada time inicia com 1000 pontos.  
   - A cada jogo, o Elo é atualizado conforme:  
     - Probabilidade de vitória baseada nos Elos atuais.  
     - Margem de gols influencia mudança (diferença de gols multiplica o ganho/perda).  
     - Fator casa aplicado: vitória em casa tem impacto menor (× 0.9); derrota em casa tem impacto maior (× 1.1).  
   - Resultado armazenado em `elo_historico.csv`.

2. **Classificação do Campeonato**  
   - Pontuação: vitória = 3 pontos, empate = 1 ponto, derrota = 0.  
   - Critérios de desempate: pontos → vitórias → saldo de gols → gols marcados → menos gols sofridos → nome do time.  
   - Geração do arquivo `classificacao_brasileirao_2025.csv`.

3. **Projeção de Resultados**  
   - Permite aplicar previsões manuais (ex: lista de jogos com resultado “Mandante”, “Empate” ou “Visitante”).  
   - Simula resultados com 1×0 (mandante vence), 0×1 (visitante vence) ou 0×0 (empate).  
   - Recalcula a classificação projetada e salva em `classificacao_brasileirao_2025_projetada.csv`.

4. **Identificação de Jogos Faltantes**  
   - Considera que cada par de times se enfrenta duas vezes (um em cada mando).  
   - Verifica quantas vezes cada confronto (independente de ordem) já ocorreu.  
   - Gera lista de jogos ainda pendentes e salva em `jogos_faltantes_2025.csv`.

## 🛠 Como usar  
1. Clone o repositório:  
   ```bash
   git clone https://github.com/dovahkiinemo/Futebol-Elo.git
   cd Futebol-Elo
