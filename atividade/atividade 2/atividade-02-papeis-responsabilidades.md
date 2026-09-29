# Atividade 2: Organização da Qualidade no LocalEats

## 1. Identificação

**Turma:** ADS5N26-2C  
**Equipe:** Individual  
**Data:** 29/09/2026

### Integrantes

| Nome | Usuário no GitHub |
|---|---|
| Leandro Quevedo | @ljquevedo |

**Elemento de Competência:** Identificar papéis, responsabilidades e competências relacionadas às atividades de qualidade e testes.

---

## 2. Tarefa 1: Diagnóstico da situação

### 2.1 Problemas organizacionais

| Problema identificado | Possível consequência para o produto ou para a equipe |
|---|---|
| **Não existem critérios claros para considerar uma funcionalidade pronta** (sem critérios de aceitação nem *Definition of Done*). | Cada pessoa entende "pronto" de um jeito: o desenvolvedor entrega quando o código compila, e o QA ou o usuário descobre depois que o comportamento não era o esperado. O resultado são funcionalidades que chegam aos usuários com defeitos, retrabalho e discussões sobre o que deveria ter sido entregue. Exemplo observado na Atividade 1: a pesquisa existe, mas não retorna resultados por especialidade. |
| **Parte da equipe acredita que somente o QA deve testar.** | O desenvolvedor não cria testes unitários nem verifica a própria entrega, e o QA vira um gargalo no fim do ciclo. Os defeitos são encontrados tarde, quando corrigir custa mais, e parte deles passa para produção. A qualidade deixa de ser construída e passa a ser apenas "inspecionada" no final. |
| **Defeitos não são registrados nem acompanhados, e não há responsável definido pela liberação de versões.** | Defeitos conhecidos são esquecidos ou reaparecem, não há histórico para priorizar correções e ninguém responde pela decisão de publicar. Uma versão pode ser disponibilizada com defeitos críticos em aberto, e, quando algo dá errado, não fica claro quem decidiu nem com base em quê. |

### 2.2 Responsabilidade pela qualidade

**A qualidade do LocalEats deve ser responsabilidade exclusiva do profissional de QA? Justifiquem.**

Não. O QA ajuda a planejar, medir e dar visibilidade à qualidade, mas não consegue "colocar" qualidade no produto sozinho. Ela depende de requisitos e critérios de aceitação claros (responsável pelo produto), de código bem feito, revisado e com testes unitários (desenvolvedores e liderança técnica) e de decisões conscientes de liberação. No LocalEats, um requisito ambíguo sobre a pesquisa gera um defeito que nenhum teste no final evita por completo. A qualidade é responsabilidade compartilhada ao longo de todo o desenvolvimento.

---

## 3. Tarefa 2: Papéis e competências

> Como a atividade é individual, analisei os quatro papéis usados na matriz RACI. Não incluí um papel de DevOps separado porque, em uma equipe pequena como a do LocalEats, a publicação pode ficar com a liderança técnica; essa decisão é discutida na seção 4.1.

| Integrante | Papel analisado | Responsabilidades relacionadas à qualidade | Competências técnicas | Competências comportamentais |
|---|---|---|---|---|
| Leandro Quevedo | **Responsável pelo produto** (Product Owner) | Definir e priorizar as funcionalidades a partir das necessidades dos usuários e restaurantes; escrever critérios de aceitação claros e verificáveis; priorizar a correção de defeitos junto com o restante do backlog; aprovar a disponibilização de uma versão com base nos testes e nos defeitos em aberto. | Levantamento e escrita de requisitos e histórias de usuário; escrita de critérios de aceitação (por exemplo, no formato Dado/Quando/Então); conhecimento do negócio de delivery e restaurantes locais; noções de métricas de produto e de priorização. | Comunicação com usuários e equipe; capacidade de negociação e de tomar decisões; visão de negócio; disponibilidade para esclarecer dúvidas durante o desenvolvimento. |
| Leandro Quevedo | **Desenvolvedor** | Implementar as funcionalidades de acordo com os critérios de aceitação; criar e manter testes unitários; revisar o código de colegas (*code review*); corrigir defeitos registrados; testar a própria entrega antes de enviá-la para o QA. | Linguagem e frameworks do projeto (por exemplo, TypeScript/Node.js e API REST); banco de dados e ORM; testes unitários e de integração; versionamento com Git e *pull requests*; boas práticas de código limpo. | Colaboração com QA e PO; atenção a detalhes; abertura para receber críticas no *code review*; responsabilidade sobre a qualidade do que entrega; pensamento crítico para questionar requisitos ambíguos. |
| Leandro Quevedo | **QA / Analista de qualidade** | Revisar requisitos e critérios de aceitação antes do desenvolvimento, apontando ambiguidades; planejar e executar os testes de sistema; registrar e acompanhar defeitos até a correção; informar a situação da qualidade (testes executados, defeitos em aberto) para apoiar a decisão de liberação; incentivar boas práticas de teste na equipe. | Fundamentos e técnicas de teste (caixa-preta, particionamento de equivalência, valor-limite); modelo de qualidade ISO/IEC 25010; elaboração de casos e planos de teste; uso de ferramentas de registro de defeitos; noções de automação de testes. A certificação CTFL (ISTQB/BSTQB) pode ser um caminho de desenvolvimento, mas não substitui a experiência prática. | Pensamento crítico e curiosidade; comunicação clara e objetiva ao relatar defeitos, sem culpar pessoas; organização; colaboração com desenvolvedores e PO; persistência para acompanhar os defeitos até o fim. |
| Leandro Quevedo | **Liderança técnica** | Definir padrões de código e de testes da equipe; aprovar o resultado das revisões de código; garantir que existam testes unitários; avaliar a viabilidade técnica das correções e apoiar a priorização; executar a publicação da versão no ambiente de produção (por exemplo, na Vercel) após a aprovação. | Arquitetura de software; experiência com a pilha tecnológica do projeto; *code review*; integração e entrega contínua (CI/CD); monitoramento da aplicação em produção. | Liderança e mentoria; capacidade de mediar conflitos técnicos; tomada de decisão; visão de conjunto; saber delegar para não concentrar todas as decisões. |

---

## 4. Tarefa 3: Matriz de responsabilidades

- **R:** responsável por executar a atividade;
- **A:** aprovador ou responsável final;
- **C:** consultado antes da execução ou decisão;
- **I:** informado sobre o resultado.

| Atividade de qualidade | Responsável pelo produto | Desenvolvedor | QA | Liderança técnica |
|---|:---:|:---:|:---:|:---:|
| Definir critérios de aceitação | R/A | C | C | I |
| Revisar requisitos | A | C | R | C |
| Implementar a funcionalidade | I | R | C | A |
| Revisar o código | — | R | I | A |
| Criar testes unitários | — | R | C | A |
| Planejar e executar testes do sistema | C | C | R/A | I |
| Registrar e acompanhar defeitos | I | R | R/A | I |
| Priorizar a correção dos defeitos | R/A | I | C | C |
| Aprovar a disponibilização da versão | A | I | C | R |

**Decisões principais:**

- **Critérios de aceitação:** quem define é o responsável pelo produto (R/A), porque ele representa a necessidade do usuário. Desenvolvedor e QA são consultados antes, para garantir que os critérios sejam viáveis e testáveis.
- **Revisar requisitos:** o QA executa, porque procura ambiguidades e casos não previstos (como o que fazer quando a pesquisa não encontra resultados). O responsável pelo produto aprova as correções.
- **Testes:** os testes unitários são do desenvolvedor, e o QA fica com os testes de sistema. Assim, testar não é exclusividade do QA.
- **Registrar defeitos:** tem dois R, porque quem encontrar um defeito deve registrá-lo. O QA é o A e garante o acompanhamento até o fechamento.
- **Aprovar a disponibilização:** o único A é o responsável pelo produto, o que resolve a dúvida sobre quem autoriza a publicação. O QA é consultado sobre a situação dos testes, e a liderança técnica executa a publicação.

### 4.1 Lacuna ou conflito encontrado

**Lacuna ou conflito:**  
Há **concentração na liderança técnica**. Ela é A em implementar a funcionalidade, revisar o código e criar testes unitários, e ainda é R na disponibilização da versão, já que a equipe não tem um papel de DevOps. Existe também um possível **conflito na revisão de código**: se a liderança técnica também programa, ela pode acabar aprovando o próprio código.

**Consequência:**  
A liderança técnica vira um gargalo. Se estiver ausente ou sobrecarregada, as revisões ficam paradas ou são feitas às pressas, e nenhuma versão é publicada. Quando ela aprova o próprio código, a revisão perde o objetivo, que é ter um segundo olhar, e defeitos passam para produção. Uma solução seria exigir que a revisão seja feita por outra pessoa (outro desenvolvedor) e automatizar a publicação em um *pipeline*, reduzindo a dependência de uma única pessoa.

### 4.2 Práticas de QA recomendadas

| Prática recomendada | Problema que ajuda a resolver | Papéis envolvidos |
|---|---|---|
| **Definition of Done e critérios de aceitação definidos em conjunto** ("três amigos"): antes de cada funcionalidade, PO, desenvolvedor e QA se reúnem para escrever os critérios de aceitação. A funcionalidade só é considerada pronta quando atende aos critérios, tem testes unitários, passou por revisão de código e foi testada pelo QA. | Critérios de pronto pouco claros; funcionalidades que chegam com defeitos; a ideia de que só o QA testa, porque a DoD inclui testes feitos pelo desenvolvedor. | Responsável pelo produto, Desenvolvedor, QA (liderança técnica consultada sobre os padrões técnicos da DoD). |
| **Registro e triagem de defeitos em uma ferramenta única** (por exemplo, GitHub Issues), com um modelo padrão (passos para reproduzir, resultado esperado, resultado obtido, evidência, severidade) e uma reunião curta de triagem para priorizar. Uma versão só pode ser liberada se não houver defeitos críticos em aberto. | Defeitos identificados e não acompanhados; falta de critério e de responsável na decisão de liberar uma versão. | QA (registra e acompanha), Desenvolvedor (registra e corrige), Responsável pelo produto (prioriza e aprova a liberação), Liderança técnica (avalia o impacto técnico). |

---

## 5. Uso de inteligência artificial

**Ferramenta utilizada:**  
Claude (Anthropic), no modo Cowork.

**Como foi utilizada:**  
Para organizar o diagnóstico a partir do contexto da atividade, sugerir responsabilidades e competências de cada papel, montar uma primeira versão da matriz RACI e propor práticas de QA.

**Como as respostas foram verificadas:**  
Conferi a matriz com as regras da atividade (pelo menos um R e um único A por atividade) e revisei cada atribuição, verificando se eu conseguiria justificá-la. Comparei os papéis e as práticas com o material da Aula 3 (Papéis, Responsabilidades e Práticas de QA; Certificações em teste de software) e ajustei o texto ao contexto do LocalEats.
