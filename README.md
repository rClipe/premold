# 🏭 PréMold — Gestão de Produção de Pré-Moldados

> Sistema web completo para gestão de produção, estoque, custos e lucratividade de fábricas de pré-moldados.

---

## ✅ Funcionalidades

### Produção
- Registro de produção com cálculo automático de custo por peça
- Snapshot imutável de consumo de insumos por lançamento
- Suporte a produtos por traço e por peça (pp)
- Edição e exclusão com reversão opcional de estoque

### Financeiro
- Custo real = insumos + mão de obra + rateio de despesas
- Rateio automático: total de despesas mensais ÷ peças produzidas
- Margem de lucro por produto e por período
- Relatório de lançamentos com totais

### Estoque
- Controle de entrada e saída de insumos
- Desconto automático ao registrar produção
- Estorno de insumos ao excluir produção (opcional)
- Extrato completo de movimentações

### Relatórios
- Consumo real de insumos (baseado em snapshots)
- Lucratividade por produto
- Comparativo de custos × venda
- Lançamentos filtráveis por período e produto
- Exportação CSV com 10 colunas detalhadas

### Multi-empresa / Multi-usuário
- Login por e-mail e senha (administrador)
- Login por código + nome + senha (funcionários)
- Dados completamente isolados por empresa
- Sincronização em tempo real entre dispositivos (Firebase)
- Funcionamento offline com sync automático ao reconectar

### Dados
- Backup e restauração em JSON
- Migração automática entre versões
- Resolução de conflito por timestamp (offline/online)

---

## 🚀 Acesso

**[→ Abrir o sistema](https://SEU-USUARIO.github.io/premold/)**

---

## ⚙️ Configuração Firebase (nuvem)

Para ativar sincronização em nuvem entre dispositivos:

1. Crie um projeto em [console.firebase.google.com](https://console.firebase.google.com)
2. Ative **Firestore Database** e **Authentication → E-mail/senha**
3. Registre um app Web (`</>`) nas configurações do projeto
4. Cole os 6 valores do `firebaseConfig` no `index.html`
5. Configure as regras do Firestore:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /empresas/{uid}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
    match /codigos/{code} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

Sem Firebase configurado, o sistema funciona normalmente em modo local (dados salvos no navegador).

---

## 📦 Produtos cadastrados

48 produtos reais do setor de pré-moldados em 7 categorias:

| Categoria | Exemplos |
|---|---|
| Blocos | Bloco 10/15/20 Areia e Brita, Bloquetes, Cobogó |
| Manilhas | Manilha 40/60/80/100 Armada, Meia, Simples, Boca de Lobo |
| Anéis | Anel Cisterna, Anel PV, Zanel c/Tampa |
| Lajes | Laje Isopor, Lajota, Vigota, Treliça |
| Mourões | Mourão Reto 2,5/2,7/3,0/3,4 MT, Estaca |
| Tampas | Tampa Anel, Tampa Manilha 60/80, Chapéu p/Muro, Tampa Canaleta |
| Meio-Fio | Meio-Fio 80×35 e 80×11 |

> Preços de referência: Dois Irmãos Materiais de Construção — Porto Firme MG (mai/2026)

---

## 🏗 Tecnologia

- HTML + CSS + JavaScript puro — arquivo único, sem dependências
- Firebase Authentication + Firestore (opcional)
- Funciona em qualquer browser moderno, desktop e mobile
- Deploy via GitHub Pages — sem servidor, sem custo

---

*PréMold v9.5 — desenvolvido para o setor de pré-moldados*
