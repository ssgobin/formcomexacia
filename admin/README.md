# 📊 Painel Admin - ACIA Comex Diagnósticos

Sistema de administração profissional para visualização, análise e exportação de dados do formulário de diagnóstico ACIA.

## 🎯 Funcionalidades

### 📈 Visão Geral
- **Estatísticas Principais**: Total de respostas, última submissão, setores únicos, cidades representadas
- **Gráficos Rápidos**: Distribuição de experiência de exportação e importação
- **Dashboard Executivo**: Visão rápida das métricas mais importantes

### 📊 Gráficos Avançados
Seis gráficos de análise profissional:
- **Top 10 Setores**: Setores econômicos mais representados
- **Top 10 Cidades**: Localidades com maior número de respostas
- **Nível de Conhecimento**: Distribuição do grau de conhecimento sobre comércio exterior
- **Associados ACIA**: Proporção de empresas associadas vs não-associadas
- **Certificações**: Tipos de certificações possuídas
- **Dificuldades Mais Comuns**: Principais desafios enfrentados pelas empresas

### 📋 Respostas Completas
- **Tabela Interativa**: Visualização de todas as 30+ respostas coletadas
- **Filtros Avançados**:
  - 🔍 Busca por Empresa (razão social ou CNPJ)
  - 🏭 Filtro por Setor
  - 🏙️ Filtro por Cidade
- **Exportação Profissional XLSX**: Botão para exportar todos os dados

## 📥 Exportação XLSX

O arquivo exportado é profissional e bem organizado com:

### ✨ Formatação
- **Cabeçalho**: Fundo azul (#1A7FC1), texto branco, bold
- **Linhas Alternadas**: Cores alternadas (branco e cinza claro) para melhor legibilidade
- **Bordas**: Bordas em todos os campos para melhor visualização
- **Colunas**: Largura otimizada (18 caracteres) para conteúdo
- **Fonte**: Montserrat (uniforme com o formulário)

### 📊 Conteúdo
31 colunas com todos os dados coletados:
- Informações da Empresa (razão social, CNPJ, cidade, estado)
- Perfil (setor, produtos, funcionários, associação)
- Exportação (experiência, percentual faturamento, países, forma)
- Produtos (NCM, certificações, capacidade)
- Recursos (equipe, material, idiomas, feiras)
- Importação (importa?, forma, países, insumos)
- Desafios (dificuldades, interesse exportar, apoio desejado)
- Programa PEIEX

## 🚀 Como Usar

### Acessar o Painel
1. Abra `admin/index.html` no navegador
2. Os dados são carregados automaticamente do Firebase Firestore

### Navegar entre Abas

**Visão Geral**
- Visualize estatísticas principais
- Veja gráficos de distribuição

**Gráficos**
- Analise tendências e padrões
- 6 gráficos diferentes para insights diversos

**Respostas**
- Veja todos os formulários preenchidos
- Use filtros para buscar específico
- Exporte para XLSX

### Filtros e Busca

```
1. Pesquisar: Digite razão social ou CNPJ
2. Setor: Selecione da lista de setores únicos
3. Cidade: Selecione da lista de cidades únicas
```

Os filtros funcionam em conjunto - selecione múltiplos para refinar a busca.

### Exportar para Excel

1. Vá até a aba **Respostas**
2. Clique no botão **📥 Exportar XLSX**
3. Arquivo será baixado automaticamente com nome:
   ```
   Diagnosticos_ACIA_DD-MM-YYYY.xlsx
   ```

## 🔐 Segurança

⚠️ **Importante**: Este painel atualmente usa as credenciais Firebase públicas. Recomenda-se:

1. **Implementar Autenticação**: Adicionar Google Sign-In ou outro método
2. **Regras Firestore**: Configurar regras para permitir leitura apenas a usuários autenticados
3. **Proteção por Senha**: Implementar senha antes de acessar o painel

### Adicionar Autenticação (Futura Melhoria)
```javascript
firebase.auth().onAuthStateChanged(user => {
  if (!user) {
    // Redirecionar para login
  }
});
```

## 📱 Responsividade

O painel é totalmente responsivo:
- ✅ Desktop (1400px+): Layout completo
- ✅ Tablet (768px-1400px): Layout adaptado
- ✅ Mobile (<768px): Single column, full width

## 🛠️ Customização

### Alterar Cores
No CSS, procure por `#1A7FC1` (azul primário) e `#3DAEE9` (azul secundário)

### Adicionar Novo Gráfico
1. Copie um gráfico existente
2. Altere o seletor do canvas
3. Modifique a lógica de dados
4. Configure o tipo de gráfico (bar, pie, doughnut, etc)

### Modificar Campos de Exportação
No JavaScript, procure pela função `exportToExcel()` e adicione/remova campos conforme necessário.

## 📚 Tecnologias

- **Frontend**: HTML5, CSS3, JavaScript Vanilla
- **Gráficos**: Chart.js 3.9.1
- **Exportação**: XLSX (SheetJS) 0.18.5
- **Database**: Firebase Firestore
- **Font**: Google Fonts - Montserrat
- **Design**: Material-inspired, profissional

## 📞 Suporte

Dúvidas ou problemas?
- Verifique o console do navegador (F12)
- Confirme que as credenciais Firebase estão corretas
- Verifique a conexão com a internet

## 📝 Notas

- Os dados são carregados automaticamente ao abrir a página
- Os gráficos se atualizam automaticamente com novos dados
- A tabela pode ser filtrada por múltiplos critérios simultaneamente
- A exportação inclui ALL respostas, mesmo com filtros aplicados

---

**Desenvolvido com ❤️ para ACIA - Núcleo de Comércio Exterior**
