# Una Alerta

Portal Una Alerta: Sistema de Monitoramento Preventivo do Rio Una (Palmares - PE)

Projeto acadêmico da disciplina de Gerenciamento de Configuração e Controle de Versão.

Data de apresentação: 01/10/2026

## Visão Geral

O município de Palmares, localizado na Zona da Mata Sul de Pernambuco, possui histórico recorrente de enchentes e inundações provocadas pelo transbordamento do Rio Una. A falta de um sistema centralizado de monitoramento, comunicação e apoio emergencial dificulta a prevenção e a resposta rápida à população em momentos de risco.

O "Una Alerta" é uma solução de software desenvolvida para consolidar dados de telemetria do rio, emitir alertas preventivos por SMS/push e catalogar pontos de apoio e abrigos seguros na cidade. A proposta tem como objetivo reduzir os riscos associados às enchentes e facilitar a tomada de decisão por parte da população e das autoridades locais.

---

## Problemática Local

A cidade de Palmares enfrenta riscos constantes de enchentes devido ao comportamento do Rio Una em períodos de chuva intensa. A ausência de informações em tempo real, de alertas preventivos e de mapeamento de locais de apoio eleva o nível de vulnerabilidade da população.

Entre os principais problemas identificados, destacam-se:

- ausência de monitoramento centralizado do nível do rio;
- baixa agilidade na comunicação de alertas;
- falta de organização sobre abrigos e pontos de apoio;
- dificuldade de acesso à informação em situações de emergência.

---

## Objetivo do Projeto

O sistema tem como objetivos principais:

- monitorar o nível do Rio Una em tempo real;
- identificar condições de risco para enchentes;
- emitir alertas preventivos para moradores em áreas vulneráveis;
- catalogar abrigos e pontos de apoio públicos;
- apoiar a gestão de informações essenciais para a Defesa Civil e para a comunidade local.

---

## Funcionalidades

### 1. Monitoramento do nível do rio
- leitura de dados de telemetria;
- comparação com limites de alerta;
- indicação do status do rio;
- suporte à decisão preventiva.

### 2. Alertas preventivos
- envio de notificações por SMS;
- alertas por push;
- comunicação mais rápida com população em risco.

### 3. Catálogo de abrigos
- cadastro de abrigos e pontos de apoio;
- localização por bairro;
- capacidade de atendimento;
- informações úteis em situação de emergência.

### 4. Dashboard de acompanhamento
- visão geral do estado do rio;
- indicadores de risco;
- suporte à análise e tomada de decisão.

---

## Requisitos do Ambiente

### Pré-requisitos
- Node.js v18.x ou superior
- Git v2.30+
- npm

### Clonagem do repositório
```bash
git clone https://github.com/alex-araujo/una-alerta-palmares.git
cd una-alerta-palmares
```

### Instalação de dependências
```bash
npm install
```

### Configuração de variáveis de ambiente
Crie um arquivo `.env` na raiz do projeto com o conteúdo abaixo:

```env
PORT=3000
API_RIO_UNA_URL=https://api.pe.gov.br/rio-una
ALERT_SMS_KEY=sua_chave_aqui
```

### Execução local
```bash
npm run dev
```

---

## Estrutura Inicial do Projeto

Os arquivos abaixo foram criados na raiz do projeto para dar suporte ao sistema:

- `index.js`
- `monitoramento.js`
- `abrigos.js`

### `index.js`
```js
const express = require("express");
const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.json());

app.get("/", (req, res) => {
  res.json({
    projeto: "Una Alerta - Palmares",
    desenvolvedores: ["Alex Araújo", "Paulo"],
    status: "Operacional",
    versao: "1.0.1"
  });
});

app.listen(PORT, () => {
  console.log(`[Una Alerta] Servidor rodando na porta ${PORT}`);
});
```

### `monitoramento.js`
```js
function consultarNivelRioUna() {
  const nivelAtualMetros = 2.45;
  const cotaAlertaMetros = 3.5;

  return {
    rio: "Rio Una - Palmares",
    nivel: nivelAtualMetros,
    status:
      nivelAtualMetros >= cotaAlertaMetros
        ? "ALERTA DE ENCHENTE"
        : "NORMAL",
    fusoHorario: "America/Recife (UTC-3)"
  };
}

module.exports = { consultarNivelRioUna };
```

### `abrigos.js`
```js
const abrigosPalmares = [
  { id: 1, nome: "Escola Municipal Modelo", bairro: "Centro", capacidade: 150 },
  { id: 2, nome: "Ginásio Coberto Principal", bairro: "Santo Antônio", capacidade: 300 },
  { id: 3, nome: "Centro Comunitário", bairro: "Santa Rosa", capacidade: 80 }
];

function listarAbrigos() {
  return abrigosPalmares;
}

module.exports = { listarAbrigos };
```

---

## Estratégia de Branching (Git Flow adaptado)

O projeto adota uma adaptação da estratégia Git Flow para o trabalho colaborativo em dupla.

### Branches principais
- `main`: branch de produção, com código estável e pronto para entrega;
- `develop`: branch principal de integração;
- `feature/*`: desenvolvimento de novas funcionalidades;
- `release/*`: preparação e validação de versões;
- `hotfix/*`: correções urgentes aplicadas em produção.

### Política adotada
- nenhuma alteração é enviada diretamente para `main` ou `develop`;
- todas as mudanças passam por Pull Request;
- a revisão cruzada é obrigatória;
- conflitos são resolvidos localmente antes da aprovação do PR.

---

## Padrões de Contribuição e Commits

Para manter a rastreabilidade e a organização do histórico, o projeto segue a convenção Conventional Commits.

### Formato
```bash
<tipo>(<escopo>): <descrição curta em imperativo>
```

### Tipos utilizados
- `feat`: nova funcionalidade;
- `fix`: correção de bug;
- `docs`: atualização de documentação;
- `style`: ajustes de formatação;
- `refactor`: refatoração sem alteração de comportamento;
- `test`: adição ou ajuste de testes;
- `chore`: ajustes de configuração, dependências ou build.

### Exemplos
```bash
feat(alertas): adiciona integração com API de SMS
fix(mapa): corrige renderização dos pontos do Rio Una
docs(readme): atualiza instruções de instalação
chore(release): prepara versão para entrega
```

---

## Fluxo de Code Review e Pull Requests

Todo código deve ser integrado por meio de Pull Request direcionado para a branch `develop`.

### Regras
- nenhum integrante realiza commits diretamente em `main` ou `develop`;
- alterações só entram após revisão e aprovação;
- conflitos de emergência devem ser resolvidos localmente antes da aprovação do PR.

### Revisão cruzada obrigatória
- quando Alex Araújo abre um PR, Paulo revisa e aprova;
- quando Paulo abre um PR, Alex Araújo revisa e aprova.

Essa prática garante maior qualidade, colaboração e alinhamento entre os integrantes da dupla.

---

## Divisão de Papéis e Responsabilidades

### Alex Araújo
Papel: Lead Developer & Full-Stack (Backend)

Responsabilidades:
- gestão das branches `main` e `release`;
- desenvolvimento da API de telemetria;
- integração de envio de SMS;
- validação de tags de release;
- aprovação de PRs de Paulo.

### Paulo
Papel: DevOps & Full-Stack (Frontend/Docs)

Responsabilidades:
- gestão da branch `develop`;
- documentação e manutenção do README;
- desenvolvimento do painel de monitoramento;
- catálogo de abrigos;
- revisão cruzada de PRs de Alex;
- controle das mensagens de commit.

---

## Registro de Alterações (CHANGELOG)

### [v1.0.1] - 01/10/2026
#### Corrigido
- ajuste emergencial no fuso horário da emissão dos alertas preventivos da Defesa Civil.

### [v1.0.0] - 01/10/2026
#### Adicionado
- painel principal de monitoramento do nível do Rio Una em tempo real;
- catálogo interativo de abrigos e pontos de apoio públicos em Palmares;
- módulo de notificação via SMS para moradores cadastrados em áreas de risco.

### [v0.1.0] - 25/09/2026
#### Adicionado
- estrutura inicial do repositório;
- documentação e padronização das convenções Git.

---

## Script para Gerar o Histórico no Git

Abra o terminal na pasta do projeto e execute o bloco abaixo:

```bash
git init
git checkout -b main

git add README.md
git commit -m "docs: adiciona estrutura inicial da documentacao e padroes do projeto"
git tag -a v0.1.0 -m "Versao inicial de planejamento do UnaAlerta por Alex e Paulo"

git checkout -b develop

git checkout -b feature/monitoramento-rio
git add index.js monitoramento.js
git commit -m "feat(monitoramento): adiciona servico de leitura do nivel do Rio Una"
git checkout develop
git merge --no-ff feature/monitoramento-rio -m "merge: PR #1 (Alex Araújo) aprovado por Paulo - modulo de monitoramento"
git branch -d feature/monitoramento-rio

git checkout -b feature/abrigos-palmares
git add abrigos.js
git commit -m "feat(abrigos): insere catalogo de abrigos publicos de Palmares"
git checkout develop
git merge --no-ff feature/abrigos-palmares -m "merge: PR #2 (Paulo) aprovado por Alex Araújo - catalogo de abrigos"
git branch -d feature/abrigos-palmares

git checkout -b release/v1.0.0
git commit -m "chore(release): prepara versao v1.0.0 para apresentacao" --allow-empty

git checkout main
git merge --no-ff release/v1.0.0 -m "merge: publica release v1.0.0 em producao"
git tag -a v1.0.0 -m "Versao 1.0.0 - Sistema Una Alerta Palmares"
git checkout develop
git merge --no-ff release/v1.0.0 -m "merge: atualiza develop com ajustes da release v1.0.0"
git branch -d release/v1.0.0

git checkout main
git checkout -b hotfix/ajuste-fuso-horario
echo "// Correção de fuso horário aplicada" >> monitoramento.js
git add monitoramento.js
git commit -m "fix(tempo): corrige diferenca de fuso horario na emissao dos alertas"

git checkout main
git merge --no-ff hotfix/ajuste-fuso-horario -m "merge: aplica hotfix v1.0.1 em producao"
git tag -a v1.0.1 -m "Versao 1.0.1 - Correcao emergencial de fuso horario"
git checkout develop
git merge --no-ff hotfix/ajuste-fuso-horario -m "merge: sincroniza hotfix v1.0.1 com develop"
git branch -d hotfix/ajuste-fuso-horario
```

---

## Guia de Apresentação em Dupla

### Abertura e contexto
**Paulo** deve explicar o problema das enchentes do Rio Una em Palmares e apresentar a estrutura do projeto.

É importante destacar a política de Code Review, mostrando que todo código enviado por Alex passou pela revisão e aprovação de Paulo antes do merge na branch `develop`.

### Versionamento e Git Flow
**Alex Araújo** deve executar o comando abaixo para demonstrar o histórico do projeto:

```bash
git log --graph --oneline --all
```

Em seguida, deve explicar:

- uso das convenções de commits;
- gestão das branches e merges;
- criação de releases e tags;
- aplicação do hotfix em produção.

---

 Conclusão

O Una Alerta é uma solução acadêmica e prática voltada para o monitoramento preventivo do Rio Una, com foco na redução de riscos de enchentes e na melhoria da comunicação entre a população e as autoridades.

A utilização de boas práticas de versionamento, revisão de código e organização estrutural do Git torna o projeto mais profissional, confiável e alinhado com metodologias reais de desenvolvimento de software.


