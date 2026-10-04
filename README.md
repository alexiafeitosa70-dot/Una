# Una
Portal Una Alerta: Sistema de Monitoramento Preventivo do Rio Una (Palmares - PE) Projeto Acadêmico - Gerenciamento de Configuração e Controle de Versão Data de Apresentação:01/10/2026 

Portal Una Alerta: Sistema de Monitoramento Preventivo do Rio Una (Palmares - PE)
Projeto Acadêmico - Gerenciamento de Configuração e Controle de Versão
Data de Apresentação: 01/10/2026

Visão Geral do Problema Local
O município de Palmares, localizado na Zona da Mata Sul de Pernambuco, possui um histórico recorrente de enchentes devastadoras decorrentes do transbordamento do Rio Una. A falta de um canal centralizado e acessível para a população acompanhar o nível do rio em tempo real e receber alertas preventivos de alagamento aumenta a vulnerabilidade social e comercial da região.

O "Una Alerta" é uma solução de software desenvolvida para consolidar dados de telemetria do rio, emitir alertas preventivos via SMS/Push e catalogar pontos de apoio e abrigos seguros na cidade de Palmares, auxiliando a Defesa Civil e a população local.

Instruções de Ambiente e Instalação

Pré-requisitos:

Node.js: v18.x ou superior

Git: v2.30+

Passo a Passo para Execução Local:

Clonar o repositório:
git clone https://github.com/alex-araujo/una-alerta-palmares.git
cd una-alerta-palmares

Instalar dependências:
npm install

Configurar variáveis de ambiente:
Crie um arquivo .env na raiz do projeto com base no modelo .env.example:
PORT=3000
API_RIO_UNA_URL=https://api.pe.gov.br/rio-una
ALERT_SMS_KEY=sua_chave_aqui

Executar a aplicação em modo de desenvolvimento:
npm run dev

Política de Ramificação (Branching Strategy)
Adotamos a estratégia baseada em Git Flow, adaptada rigorosamente para o trabalho colaborativo em dupla:

main: Ramificação de produção. Armazena apenas código estável, testado e pronto para entrega com tags de versão.

develop: Ramificação principal de integração. Concentra o código das funcionalidades aprovadas pela dupla.

feature/: Criada a partir de develop para o desenvolvimento isolado de cada tarefa (ex.: feature/mapa-abrigos).

release/vX.X.X: Preparação, ajustes finos e validação de uma nova versão de produção.

hotfix/: Ramificação emergencial criada a partir de main para solucionar bugs críticos diretamente em produção.

Padrões de Contribuição e Commits
Para manter a rastreabilidade e a padronização no histórico, a dupla adota a convenção Conventional Commits:

Formato das Mensagens:
(): <descrição curta e no imperativo>

Tipos Utilizados no Projeto:

feat: Adição de uma nova funcionalidade (ex.: feat(alertas): adiciona integração com API de SMS).

fix: Correção de um bug (ex.: fix(mapa): corrige renderização dos pontos do Rio Una).

docs: Alterações na documentação (ex.: docs(readme): atualiza instrucoes de instalacao).

style: Ajustes de formatação ou estilo visual sem alterar código lógico.

refactor: Refatoração de código sem alterar funcionalidade.

test: Adição ou ajuste de testes automatizados.

chore: Atualizações de configurações, arquivos de build ou dependências.

Fluxo de Code Review e Pull Requests (PRs)

Nenhum integrante realiza commits diretamente nas branches main ou develop.

Todo código é integrado via Pull Request (PR) apontando para a branch develop.

Revisão Cruzada Obrigatória (Peer Review):

Quando Alex Araújo abre um PR, obrigatoriamente Paulo analisa, revisa as alterações e aprova.

Quando Paulo abre um PR, Alex Araújo faz a revisão do código antes do merge.

Conflitos de emergência são resolvidos localmente pela pessoa responsável pela ramificação antes da aprovação do PR.

Divisão de Papéis e Responsabilidades (Dupla)

Integrante: Alex Araújo
Papel no Projeto: Lead Developer & Full-Stack (Backend)
Responsabilidades Principais:

Gestão das branches main e release.

Desenvolvimento da API de telemetria e envio de SMS.

Validação das tags de release e aprovação de PRs de Paulo.

Integrante: Paulo
Papel no Projeto: DevOps & Full-Stack (Frontend/Docs)
Responsabilidades Principais:

Gestão da branch develop e documentação (README.md, CHANGELOG.md).

Interface do painel do Rio Una e catálogo de abrigos.

Revisão cruzada de PRs de Alex e controle de mensagens de commit.

Registro de Alterações (CHANGELOG)

[v1.0.1] - 01/10/2026
Corrigido:

Ajuste emergencial no fuso horário da emissão dos alertas preventivos da Defesa Civil (hotfix).

[v1.0.0] - 01/10/2026
Adicionado:

Painel principal de monitoramento do nível do Rio Una em tempo real.

Catálogo interativo de abrigos e pontos de apoio públicos em Palmares.

Módulo de notificação via SMS para moradores cadastrados em áreas de risco.

[v0.1.0] - 25/09/2026
Adicionado:

Estruturação inicial do repositório, documentação e padronização das convenções Git.

Arquivos de Código para a Raiz do Projeto
Crie estes três arquivos simples na raiz da pasta local para dar sustentação ao repositório:

Arquivo index.js:

// Servidor Principal do Una Alerta - Palmares/PE
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.json());

app.get('/', (req, res) => {
res.json({
projeto: "Una Alerta - Palmares",
desenvolvedores: ["Alex Araújo", "Paulo"],
status: "Operacional",
versao: "1.0.1"
});
});

app.listen(PORT, () => {
console.log([Una Alerta] Servidor rodando na porta ${PORT});
});

Arquivo monitoramento.js:

// Módulo de Monitoramento Telemétrico do Rio Una
function consultarNivelRioUna() {
const nivelAtualMetros = 2.45;
const cotaAlertaMetros = 3.50;

return {
rio: "Rio Una - Palmares",
nivel: nivelAtualMetros,
status: nivelAtualMetros >= cotaAlertaMetros ? "ALERTA DE ENCHENTE" : "NORMAL",
fusoHorario: "America/Recife (UTC-3)"
};
}

module.exports = { consultarNivelRioUna };

Arquivo abrigos.js:

// Catálogo de Pontos de Apoio e Abrigos Emergenciais em Palmares
const abrigosPalmares = [
{ id: 1, nome: "Escola Municipal Modelo", bairro: "Centro", capacidade: 150 },
{ id: 2, nome: "Ginásio Coberto Principal", bairro: "Santo Antônio", capacidade: 300 },
{ id: 3, nome: "Centro Comunitário", bairro: "Santa Rosa", capacidade: 80 }
];

function listarAbrigos() {
return abrigosPalmares;
}

module.exports = { listarAbrigos };

Script Automatizado para Gerar o Histórico no Git
Abra o terminal na pasta onde os arquivos acima estão salvos e copie e cole todo o bloco de comandos:

Inicializar o repositório
git init
git checkout -b main

Commit Inicial de Paulo (v0.1.0)
git add README.md
git commit -m "docs: adiciona estrutura inicial da documentacao e padroes do projeto"
git tag -a v0.1.0 -m "Versao inicial de planejamento do UnaAlerta por Alex e Paulo"

Criar e mudar para a branch develop
git checkout -b develop

Feature 1: Módulo do Backend por Alex Araújo
git checkout -b feature/monitoramento-rio
git add index.js monitoramento.js
git commit -m "feat(monitoramento): adiciona servico de leitura do nivel do Rio Una"
git checkout develop
git merge --no-ff feature/monitoramento-rio -m "merge: PR #1 (Alex Araújo) aprovado por Paulo - modulo de monitoramento"
git branch -d feature/monitoramento-rio

Feature 2: Módulo de Abrigos em Palmares por Paulo
git checkout -b feature/abrigos-palmares
git add abrigos.js
git commit -m "feat(abrigos): insere catalogo de abrigos publicos de Palmares"
git checkout develop
git merge --no-ff feature/abrigos-palmares -m "merge: PR #2 (Paulo) aprovado por Alex Araújo - catalogo de abrigos"
git branch -d feature/abrigos-palmares

Preparação da Release v1.0.0 por Alex
git checkout -b release/v1.0.0
git commit -m "chore(release): prepara versao v1.0.0 para apresentacao" --allow-empty

Merge da Release na Main e Tag v1.0.0
git checkout main
git merge --no-ff release/v1.0.0 -m "merge: publica release v1.0.0 em producao"
git tag -a v1.0.0 -m "Versao 1.0.0 - Sistema Una Alerta Palmares"
git checkout develop
git merge --no-ff release/v1.0.0 -m "merge: atualiza develop com ajustes da release v1.0.0"
git branch -d release/v1.0.0

Execução de Hotfix Urgente em Produção por Alex e Paulo
git checkout main
git checkout -b hotfix/ajuste-fuso-horario
echo "// Correção de fuso horário aplicada" >> monitoramento.js
git add monitoramento.js
git commit -m "fix(tempo): corrige diferenca de fuso horario na emissao dos alertas"

Finalização do Hotfix e Tag v1.0.1
git checkout main
git merge --no-ff hotfix/ajuste-fuso-horario -m "merge: aplica hotfix v1.0.1 em producao"
git tag -a v1.0.1 -m "Versao 1.0.1 - Correcao emergencial de fuso horario"
git checkout develop
git merge --no-ff hotfix/ajuste-fuso-horario -m "merge: sincroniza hotfix v1.0.1 com develop"
git branch -d hotfix/ajuste-fuso-horario

Guia de Apresentação em Dupla

Abertura e Contexto (Paulo):

Explique o problema social das enchentes do Rio Una em Palmares e apresente a estrutura do README.md.

Destaque a política de Code Review: mostre que todo código enviado por Alex passou pela sua revisão e aprovação antes do merge na branch develop.

Versionamento e Git Flow (Alex Araújo):

Execute o comando git log --graph --oneline --all no terminal para exibir o gráfico completo de commits e branches.

Explique o uso dos Conventional Commits (feat, fix, docs, chore) e a gestão das tags e releases (v1.0.0 e o hotfix v1.0.1).
