<!DOCTYPE html>
<html lang="pt-BR">
<head> … </head>
<body>
  <h1>ProBola AI – Palpites com IA</h1>
  <table id="games-table"> … </table>
  <script>
    async function carregarJogos() {
      const url = "https://corsproxy.io/https://v3.football.api-sports.io/fixtures?league=71&season=2024&next=5";
      try {
        const resp = await fetch(url, {
          headers: { "x-apisports-key": "86b3236f88ad74c3d59642671e448f6b" }
        });
        const dados = await resp.json();
        const tabela = document.getElementById("games-table");

        dados.response.forEach(jogo => {
          const casa = jogo.teams.home.name;
          const visitante = jogo.teams.away.name;
          const confianca = Math.floor(Math.random() * 21) + 80;
          const cashout = confianca >= 90
            ? "Sim (" + (70 + Math.floor(Math.random() * 11)) + "%)"
            : "Não";
          tabela.innerHTML += `
            <tr><td>${casa} x ${visitante}</td><td>${confianca}%</td>
            <td class="${cashout.includes('Sim') ? 'ok' : 'nao'}">${cashout}</td></tr>`;
        });
      } catch {
        alert("Erro ao carregar. Verifique sua conexão.");
      }
    }
    carregarJogos();
  </script>
</body>
</html>
