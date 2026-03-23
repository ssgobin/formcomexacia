/* GUIA DE CUSTOMIZAÇÃO - Painel Admin ACIA */

/* ============================================
   1. ALTERAR CORES DO TEMA
   ============================================ */

/* Cores Atuais */
--primary: #1A7FC1;      /* Azul primário */
--secondary: #3DAEE9;    /* Azul secundário */
--success: #4caf50;      /* Verde */
--warning: #ff9800;      /* Laranja */
--danger: #f44336;       /* Vermelho */

/* Para mudar para tema verde, por exemplo:
   Substitua no CSS:
   #1A7FC1 → #2e7d32 (verde escuro)
   #3DAEE9 → #4caf50 (verde claro)
*/

/* ============================================
   2. ALTERAR ESPAÇAMENTO E LAYOUT
   ============================================ */

/* Alterar padding do container */
.container {
  padding: 32px 24px;  /* Aumentar primeiro valor para mais espaço vertical */
}

/* Alterar gap entre cards */
.stats-grid {
  gap: 20px;  /* Aumentar para 30px para mais espaço */
}

/* ============================================
   3. ADICIONAR NOVO GRÁFICO
   ============================================ */

// 1. Adicione no HTML:
<div class="chart-card">
  <h3>Novo Gráfico</h3>
  <div class="chart-container">
    <canvas id="novoGraficoChart"></canvas>
  </div>
</div>

// 2. Adicione no JavaScript (em createCharts()):
new Chart(document.getElementById('novoGraficoChart'), {
  type: 'bar',  // ou 'pie', 'doughnut', 'line', etc
  data: {
    labels: ['Opção A', 'Opção B', 'Opção C'],
    datasets: [{
      label: 'Contagem',
      data: [10, 20, 15],
      backgroundColor: chartColors.primary,
      borderRadius: 6
    }]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    plugins: {
      legend: {
        position: 'bottom',
        labels: { font: { family: "'Montserrat', sans-serif" } }
      }
    }
  }
});

/* ============================================
   4. ADICIONAR CAMPO NA EXPORTAÇÃO
   ============================================ */

// No objeto exportData dentro de exportToExcel():
const exportData = allData.map(d => ({
  'Data/Hora': new Date(d.timestamp).toLocaleString('pt-BR'),
  // ... campos existentes ...
  'Novo Campo': d.novo_campo_aqui || '',  // ADICIONE AQUI
}));

/* ============================================
   5. ADICIONAR NOVO FILTRO
   ============================================ */

// 1. No HTML (em .filters):
<div class="filter-group">
  <label>Novo Filtro</label>
  <select id="novoFiltro" onchange="filterTable()">
    <option value="">Todos</option>
  </select>
</div>

// 2. No JavaScript (em populateFilters()):
const novoFiltroData = [...new Set(allData.map(d => d.novo_campo))];
const novoFiltroSelect = document.getElementById('novoFiltro');
novoFiltroData.forEach(item => {
  const option = document.createElement('option');
  option.value = item;
  option.textContent = item;
  novoFiltroSelect.appendChild(option);
});

// 3. Em filterTable(), adicione a condição:
const matchNovoFiltro = !novoFiltroFilter || data.novo_campo === novoFiltroFilter;

/* ============================================
   6. ADICIONAR AUTENTICAÇÃO COM FIREBASE
   ============================================ */

// No início do script, após Firebase init:
firebase.auth().onAuthStateChanged(user => {
  if (!user) {
    // Mostrar tela de login
    document.body.innerHTML = '<div style="...">Faça login para acessar</div>';
    // Ou redirecionar:
    // window.location.href = '/login.html';
  } else {
    // Usuário autenticado, carregar dados
    loadData();
  }
});

// Função de logout:
function handleLogout() {
  firebase.auth().signOut().then(() => {
    window.location.href = '/';
  });
}

/* ============================================
   7. ADICIONAR ABAS NOVAS
   ============================================ */

// 1. No HTML (em .tabs):
<button class="tab-btn" onclick="switchTab('nova-aba')">Nova Aba</button>

// 2. No HTML (em container):
<div id="nova-aba" class="tab-content">
  <!-- Conteúdo aqui -->
</div>

// 3. A função switchTab() já suporta automaticamente novas abas

/* ============================================
   8. ADICIONAR ESTATÍSTICA NOVA
   ============================================ */

// No HTML (em .stats-grid):
<div class="stat-card">
  <h3>Nova Métrica</h3>
  <div class="value" id="nova-metrica">-</div>
  <div class="subtitle">Descrição</div>
</div>

// No JavaScript (em updateStats()):
const novaMetrica = allData.filter(d => d.campo === 'valor').length;
document.getElementById('nova-metrica').textContent = novaMetrica;

/* ============================================
   9. ALTERAR TIPO DE GRÁFICO
   ============================================ */

// Tipos disponíveis:
- 'bar'       // Gráfico de barras
- 'line'      // Gráfico de linhas
- 'pie'       // Gráfico de pizza
- 'doughnut'  // Gráfico de rosca
- 'radar'     // Gráfico de radar
- 'bubble'    // Gráfico de bolhas
- 'scatter'   // Gráfico de dispersão

// Exemplo: Trocar gráfico de experiência de doughnut para pie:
new Chart(document.getElementById('experienceChart'), {
  type: 'pie',  // Alterado de 'doughnut'
  // ... resto do config ...
});

/* ============================================
   10. ADICIONAR VALIDAÇÃO DE ACESSO
   ============================================ */

// Proteger com senha simples (não recomendado em produção):
const ADMIN_PASSWORD = 'sua-senha-aqui';

function checkPasswordAndLoad() {
  const pass = prompt('Digite a senha do admin:');
  if (pass === ADMIN_PASSWORD) {
    loadData();
  } else {
    alert('Senha incorreta');
    window.location.href = '/';
  }
}

// Chamar em DOMContentLoaded:
document.addEventListener('DOMContentLoaded', checkPasswordAndLoad);

/* ============================================
   DICAS GERAIS
   ============================================ */

/*
1. Use o Chrome DevTools (F12) para debugar
2. Procure erros no Console
3. Use elementos de rede para verificar requisições Firebase
4. Teste mudanças em uma cópia antes de aplicar
5. Mantenha backup dos arquivos originais
6. Use nomes descritivos para novos campos
7. Documente suas customizações
8. Teste em diferentes tamanhos de tela (responsividade)
9. Valide dados antes de exibir em gráficos
10. Use console.log() para debugar lógica complexa
*/
