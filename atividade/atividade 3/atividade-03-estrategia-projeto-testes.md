# Atividade 3: Estratégia e Projeto de Testes do LocalEats

## 1. Identificação

**Turma:** ADS5N26-2C  
**Equipe:** Individual  
**Data:** 29/09/2026

### Integrantes

| Nome | Usuário no GitHub |
|---|---|
| Leandro Quevedo | @ljquevedo |

**Elemento de Competência:** Planejar e projetar testes selecionando técnicas adequadas.

**Aplicação:** <https://local-eats-unisenac.vercel.app/>

---

## 2. Tarefa 1: Planejamento dos testes

### 2.1 Objetivo dos testes

Verificar se a pesquisa do LocalEats retorna exatamente os restaurantes cuja especialidade **ou** localização corresponde ao termo informado, sem depender de maiúsculas e minúsculas, e se o sistema informa claramente quando nenhum restaurante corresponde à pesquisa.

### 2.2 Escopo

#### Funcionalidades incluídas

| Integrante | Funcionalidade incluída | O que será verificado |
|---|---|---|
| Leandro Quevedo | Pesquisar restaurantes por especialidade ou localização | Resultados da pesquisa por especialidade, por localização, com variação de maiúsculas/minúsculas e com termo sem correspondência. |

#### Funcionalidade não incluída

| Funcionalidade não incluída | Justificativa |
|---|---|
| Fazer pedido | Não faz parte do fluxo de pesquisa escolhido para os testes. Envolve itens, valores e confirmação de pedido, o que exigiria outros riscos e técnicas (por exemplo, valor limite para quantidades). |
| Filtrar restaurantes por especialidade (botões) | É uma funcionalidade diferente da pesquisa por texto. Foi deixada de fora para manter o escopo viável em um trabalho individual. |

### 2.3 Abordagem

| Item | Decisão | Justificativa |
|---|---|---|
| Níveis de teste | Sistema | A pesquisa será verificada pela interface, do campo de busca até a lista de restaurantes exibida, como o usuário a utiliza. |
| Tipos de teste | Funcional | O objetivo é verificar a regra da pesquisa (quais restaurantes devem aparecer), e não desempenho ou aparência. |
| Perspectiva caixa-preta ou caixa-branca | Caixa-preta | Serão consideradas apenas as entradas (termo pesquisado) e os resultados exibidos, sem acesso ao código. |
| Técnicas de teste | Particionamento de equivalência | Os termos que podem ser digitados são infinitos, mas se agrupam em poucas classes com o mesmo comportamento esperado (localização existente, especialidade existente, termo sem correspondência etc.). Um valor representativo de cada classe basta. |

### 2.4 Ambiente e responsabilidades

| Item | Definição |
|---|---|
| Ambiente necessário | Aplicação em <https://local-eats-unisenac.vercel.app/>; navegador Google Chrome atualizado em computador com Windows; conexão com a internet; uma conta de teste (sem dados pessoais reais); base com os 15 restaurantes atualmente exibidos na página Explorar (Restaurante Sabor 0 a 14). |
| Responsáveis pelo planejamento | Leandro Quevedo |
| Responsáveis pela especificação dos casos | Leandro Quevedo |
| Responsáveis pela futura execução | Leandro Quevedo |

### 2.5 Critérios

| Critério | Definição |
|---|---|
| Entrada | Aplicação disponível, conta de teste com acesso à página Explorar e listagem completa com os 15 restaurantes carregada, para servir de referência dos resultados esperados. |
| Saída | Os três casos planejados executados, com resultado obtido e evidência registrados, e cada defeito encontrado registrado com passos para reproduzir. |
| Suspensão | Aplicação indisponível, página Explorar sem carregar a listagem de restaurantes ou base de restaurantes alterada (o que invalida os resultados esperados). |

---

## 3. Tarefa 2: Riscos e técnicas de teste

**Relação:** Pesquisar restaurantes → R01 / R02 → Particionamento de equivalência → CT01, CT02, CT03

### 3.1 Análise dos riscos

| ID | Integrante | Funcionalidade | Risco | Consequência | Probabilidade | Impacto | Prioridade | Justificativa |
|---|---|---|---|---|:---:|:---:|:---:|---|
| R01 | Leandro Quevedo | Pesquisar restaurantes | A pesquisa não retornar os restaurantes corretos para um termo válido, por exemplo, ignorar a especialidade ou depender da grafia exata (maiúsculas e minúsculas). | O usuário acredita que não existe restaurante daquele tipo ou região e desiste do app; os restaurantes locais perdem visibilidade e pedidos. | Alta | Alto | Alta | A pesquisa é o principal meio de encontrar restaurantes, função central do LocalEats. A probabilidade é alta porque, na exploração da Atividade 1, a pesquisa por "Japonesa" não retornou resultados, embora existam restaurantes com essa especialidade. |
| R02 | Leandro Quevedo | Pesquisar restaurantes | Com um termo sem correspondência, o sistema exibir restaurantes não relacionados, ficar sem nenhum retorno visível ou apresentar erro. | O usuário fica confuso sem saber se a busca funcionou e pode escolher um restaurante que não atende ao que procurava. | Baixa | Médio | Baixa | O impacto é médio: atrapalha a experiência, mas não gera prejuízo direto. A probabilidade é baixa porque, na Atividade 1, "Churrasco" exibiu "Nenhum restaurante encontrado.". Mesmo assim, merece um caso para confirmar que o comportamento se mantém. |

### 3.2 Aplicação da técnica

**Integrante:** Leandro Quevedo  
**Funcionalidade:** Pesquisar restaurantes por especialidade ou localização  
**Risco relacionado:** R01 e R02  
**Técnica escolhida:** Particionamento de equivalência

**Por que a técnica foi escolhida:**  
A entrada da pesquisa é um texto livre, e seria impossível testar todos os termos. No entanto, termos diferentes da mesma classe devem ter o mesmo comportamento: pesquisar "Zona Sul" ou "Centro" exercita a mesma regra (busca por localização). Dividir as entradas em classes permite cobrir as regras que interessam aos riscos (especialidade, localização, maiúsculas/minúsculas e termo sem correspondência) com poucos casos representativos. Análise de valor limite não foi usada porque a pesquisa não tem uma regra numérica ou de tamanho documentada.

**Aplicação da técnica:**

Regra: *o sistema deve retornar todos os restaurantes cuja especialidade ou localização corresponda ao termo, e somente eles, sem diferenciar maiúsculas de minúsculas; se nenhum corresponder, deve informar que nada foi encontrado.*

| Classe | Tipo | Situação | Valor representativo | Resultado esperado | Risco | Caso |
|---|---|---|---|---|---|---|
| C1 | Válida | Termo igual a uma especialidade existente | "Japonesa" | Restaurantes com essa especialidade | R01 | CT01 |
| C2 | Válida | Termo igual a uma localização existente, com maiúsculas/minúsculas diferentes | "zona sul" | Restaurantes dessa localização | R01 | CT02 |
| C3 | Válida | Termo igual a uma localização existente, com a grafia exibida | "Zona Sul" | Restaurantes dessa localização | R01 | — |
| C4 | Inválida | Termo sem correspondência em especialidade nem em localização | "Churrasco" | Nenhum restaurante e mensagem informativa | R02 | CT03 |
| C5 | Inválida | Campo vazio | "" | Listagem completa ou orientação para digitar um termo | R02 | — |

As classes C3 e C5 não foram transformadas em casos, para respeitar o limite de três casos do trabalho individual. A C3 foi considerada coberta pela C2, que é mais exigente (a mesma regra de localização com variação de caixa). A C5 fica como candidata a um próximo caso (CT04).

**Casos derivados:** CT01, CT02 e CT03

---

## 4. Tarefa 3: Casos de teste e rastreabilidade

### 4.1 Casos de teste

### CT01: Pesquisar por uma especialidade existente

**Integrante responsável:** Leandro Quevedo  
**Funcionalidade:** Pesquisar restaurantes por especialidade ou localização  
**Risco ou requisito relacionado:** R01  
**Técnica utilizada:** Particionamento de equivalência (classe C1, válida)

**Pré-condição:**  
Usuário autenticado com a conta de teste, na página Explorar, com a listagem completa dos 15 restaurantes, dos quais 5 possuem a especialidade Japonesa (Restaurante Sabor 1, 2, 11, 13 e 14).

**Dados de entrada:**  
Termo de pesquisa: "Japonesa"

**Passos:**

1. Acessar a página Explorar.
2. Digitar "Japonesa" no campo "Buscar por culinária ou localização...".
3. Clicar em "Buscar".

**Resultado esperado:**  
São exibidos exatamente 5 restaurantes (Restaurante Sabor 1, 2, 11, 13 e 14), todos com a especialidade Japonesa. Nenhum restaurante de outra especialidade aparece.

---

### CT02: Pesquisar por localização com maiúsculas e minúsculas diferentes

**Integrante responsável:** Leandro Quevedo  
**Funcionalidade:** Pesquisar restaurantes por especialidade ou localização  
**Risco ou requisito relacionado:** R01  
**Técnica utilizada:** Particionamento de equivalência (classe C2, válida)

**Pré-condição:**  
Usuário autenticado com a conta de teste, na página Explorar, com a listagem completa, na qual 5 restaurantes estão na localização Zona Sul (Restaurante Sabor 0, 2, 5, 13 e 14).

**Dados de entrada:**  
Termo de pesquisa: "zona sul" (todo em minúsculas)

**Passos:**

1. Acessar a página Explorar.
2. Digitar "zona sul" no campo de pesquisa.
3. Clicar em "Buscar".

**Resultado esperado:**  
São exibidos exatamente 5 restaurantes (Restaurante Sabor 0, 2, 5, 13 e 14), todos com a localização Zona Sul, o mesmo resultado da pesquisa por "Zona Sul".

---

### CT03: Pesquisar por um termo sem correspondência

**Integrante responsável:** Leandro Quevedo  
**Funcionalidade:** Pesquisar restaurantes por especialidade ou localização  
**Risco ou requisito relacionado:** R02  
**Técnica utilizada:** Particionamento de equivalência (classe C4, inválida)

**Pré-condição:**  
Usuário autenticado com a conta de teste, na página Explorar. Nenhum restaurante da listagem possui especialidade ou localização "Churrasco".

**Dados de entrada:**  
Termo de pesquisa: "Churrasco"

**Passos:**

1. Acessar a página Explorar.
2. Digitar "Churrasco" no campo de pesquisa.
3. Clicar em "Buscar".

**Resultado esperado:**  
Nenhum restaurante é exibido e o sistema apresenta uma mensagem informando que nenhum restaurante foi encontrado. Não aparece mensagem de erro e a página continua utilizável para uma nova pesquisa.

---

### 4.2 Matriz de rastreabilidade

| Integrante | Funcionalidade | Risco ou requisito | Técnica utilizada | Casos de teste |
|---|---|---|---|---|
| Leandro Quevedo | Pesquisar restaurantes por especialidade ou localização | R01: pesquisa não retorna os restaurantes corretos para termo válido | Particionamento de equivalência (C1, C2) | CT01 e CT02 |
| Leandro Quevedo | Pesquisar restaurantes por especialidade ou localização | R02: termo sem correspondência sem retorno adequado | Particionamento de equivalência (C4) | CT03 |

Todos os riscos possuem pelo menos um caso de teste. O risco de maior prioridade (R01) recebeu dois casos.

---

## 5. Uso de inteligência artificial

**Ferramenta utilizada:**  
Claude (Anthropic), no modo Cowork.

**Como foi utilizada:**  
Para sugerir riscos da funcionalidade de pesquisa, comparar as técnicas estudadas, montar as classes de equivalência e revisar a clareza dos passos e dos resultados esperados.

**Uma sugestão que precisou ser alterada ou rejeitada:**  
Foi considerado usar análise de valor limite para o tamanho do termo pesquisado (por exemplo, 0, 1 e muitos caracteres). A ideia foi rejeitada porque o LocalEats não tem uma regra documentada de tamanho mínimo ou máximo para a pesquisa, e sem regra não há limite a verificar.

**Como as respostas foram verificadas:**  
Os resultados esperados foram conferidos com a listagem real da página Explorar (quais restaurantes são Japonesa e quais são da Zona Sul) e com a exploração feita na Atividade 1. Verifiquei que cada caso está ligado a um risco e a uma classe de equivalência e que todos os riscos têm casos na matriz de rastreabilidade.
