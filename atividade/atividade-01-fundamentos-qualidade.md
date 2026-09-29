# Atividade 1: Fundamentos e Características da Qualidade no LocalEats

## 1. Identificação

**Turma:** ADS5N26-2C  
**Equipe:** Individual  
**Data:** 29/09/2026

### Integrantes

| Nome | Usuário no GitHub |
|---|---|
| Leandro Quevedo | @ljquevedo |

**Elemento de Competência:** Compreender os fundamentos de qualidade de software e sua aplicação no desenvolvimento de sistemas.

**Aplicação:** <https://local-eats-unisenac.vercel.app/>

---

## 2. Tarefa 1: Fundamentos da qualidade

### 2.1 Necessidades explícitas e implícitas

| Tipo | Necessidade | Interessado | Consequência se não for atendida |
|---|---|---|---|
| Explícita | Pesquisar restaurantes por especialidade ou por localização (declarada na lista de funcionalidades e no campo "Buscar por culinária ou localização..."). | Usuário (cliente) | O usuário não encontra restaurantes do tipo ou da região que procura e desiste do app; os restaurantes locais perdem visibilidade e vendas. |
| Explícita | Fazer um pedido e consultá-lo depois em "Meus Pedidos". | Usuário (cliente) e restaurante | O cliente não tem confirmação nem acompanhamento do que comprou; o restaurante pode não receber ou não conseguir comprovar o pedido, gerando reclamações e perda de confiança. |
| Implícita | Os dados da conta e o histórico de pedidos devem ser protegidos: a senha não deve ficar visível e cada usuário só pode ver os próprios pedidos e favoritos. | Usuário e negócio (LocalEats) | Exposição de dados pessoais, risco de uso indevido da conta e problemas legais com a LGPD, além de dano à reputação da plataforma. |
| Implícita | A pesquisa deve tolerar variações comuns de digitação (maiúsculas/minúsculas, acentos) e retornar resultados coerentes com o que está exibido na tela. | Usuário (cliente) | O usuário digita um termo que existe na listagem, recebe "nenhum resultado" e conclui que não há restaurantes, mesmo havendo; a função existe, mas não cumpre seu objetivo. |

### 2.2 Questão sobre os fundamentos da qualidade

**Um sistema que implementa todas as funcionalidades explicitamente solicitadas pode, ainda assim, apresentar baixa qualidade? Justifiquem utilizando pelo menos uma necessidade implícita identificada pela equipe.**

Sim. Qualidade é o atendimento às necessidades explícitas **e** implícitas (ISO/IEC 25010; Pressman). O LocalEats possui a pesquisa, que é uma funcionalidade explícita, mas se ela só funcionar com a grafia exata ou não retornar restaurantes que aparecem na própria listagem, a necessidade implícita de uma busca tolerante e coerente não é atendida. Da mesma forma, um sistema de pedidos que funcione, mas exponha dados de outros usuários, tem baixa qualidade. A funcionalidade existir não garante que ela seja correta, segura ou fácil de usar.

---

## 3. Tarefa 2: Exploração da aplicação

| Integrante | Funcionalidade | O que foi realizado | O que foi observado | Evidência |
|---|---|---|---|---|
| Leandro Quevedo | Pesquisar restaurantes por especialidade ou localização | **Uso esperado:** pesquisa pela localização "Zona Sul" e, em seguida, "zona sul" (minúsculas). **Uso alternativo:** pesquisa por um termo inexistente ("Churrasco") e por especialidades que aparecem nos cards ("Japonesa" e "Italiana"). | "Zona Sul" e "zona sul" retornaram os mesmos 5 restaurantes (Sabor 0, 2, 5, 13 e 14), todos da Zona Sul. "Churrasco" exibiu a mensagem "Nenhum restaurante encontrado.". "Japonesa" e "Italiana" também exibiram "Nenhum restaurante encontrado.", embora a listagem completa mostre 5 restaurantes com a especialidade Japonesa e 3 com Italiana. Na aba Rede do navegador, as requisições enviadas foram `/restaurants/?location=Japonesa` e `/restaurants/?location=Italiana`, ou seja, o termo foi enviado como localização. A pesquisa por localização se comportou como esperado; a pesquisa por especialidade não retornou resultados. | [localização válida](evidencias/leandro-pesquisa-localizacao-zona-sul.png) · [especialidade sem resultado](evidencias/leandro-pesquisa-especialidade-japonesa-sem-resultado.png) |

---

## 4. Tarefa 3: Requisitos e características de qualidade

| Integrante | Requisito de Qualidade | Característica ou subcaracterística | Justificativa | Como avaliar |
|---|---|---|---|---|
| Leandro Quevedo | Ao pesquisar um termo que corresponda à especialidade **ou** à localização de um restaurante, o sistema deve retornar todos os restaurantes correspondentes, e somente eles, sem diferenciar maiúsculas de minúsculas. | Adequação Funcional → **Corretude Funcional** | O problema no LocalEats não é a pesquisa faltar (completude) nem ser difícil de usar (usabilidade): o campo existe e é simples, mas o resultado entregue está errado para especialidades, pois "Japonesa" retorna zero resultados quando há 5 restaurantes com essa especialidade na tela. O requisito trata da precisão do resultado, por isso a subcaracterística predominante é a corretude. Usabilidade (proteção contra erros do usuário) seria secundária, ligada apenas à tolerância a maiúsculas/minúsculas. | Montar uma lista com todas as especialidades e localizações exibidas na listagem completa, com variações de caixa. Para cada termo, **comparar** a quantidade e os nomes dos restaurantes retornados com os esperados, contados a partir da listagem. **Medir** a proporção de pesquisas com resultado correto (pesquisas corretas ÷ pesquisas realizadas). |

---

## 5. Uso de inteligência artificial

**Ferramenta utilizada:**  
Claude (Anthropic), no modo Cowork.

**Como foi utilizada:**  
Para organizar a análise da atividade a partir do material da disciplina (ISO/IEC 25010, Introdução à Qualidade de Software), sugerir necessidades explícitas/implícitas e o requisito de qualidade, e apoiar a exploração da funcionalidade de pesquisa no navegador.

**Como as respostas foram verificadas:**  
As pesquisas da Tarefa 2 foram refeitas manualmente no LocalEats, conferindo a quantidade de restaurantes retornados com a listagem completa, e as capturas de tela foram feitas por mim. A característica escolhida foi conferida com o documento "Modelo de Qualidade de Software ISO/IEC 25010" da Aula 2.
