# PLANO — inemaSEO 7 · Sistemas: monte o seu Semrush aberto (v7.2)

Curso 7 de 7 da Formação inemaSEO (os cursos 1–6 dizem "de 6"; este nasceu depois, quando o núcleo de ferramentas existiu). Público: quem usa terminal e quer medir e auditar o próprio site (ou de clientes) sem ferramenta paga.

Fontes (não alteradas): `~/projetos/inemaseo-sistemas` (README, `docs/ESPEC.md`, `ferramentas/*/README.md`, código, `exemplos/` com entradas e saídas reais de 19/10/2026), `wifi/longrun/2026-10-19-formacao-inemaseo-v72/SISTEMAS-SEO-FERRAMENTAS.md` (mercado, grátis × pago, open-seo, Firecrawl, Apify), `TENDENCIAS-SEO-GEO-2026-10.md` (régua de 2026), `inemaseo-metodo/docs/METODO.md` (cadência e "máquina com agentes"). Todo comando mostrado foi rodado em 19/10/2026 (só GET em sites públicos do INEMA e arquivos de `exemplos/`); modos que chamam API (gsc `puxar`, `--rdns`) só como modelo.

## As 8 aulas

| # | slug | aula | objetivo (≤ 160) | diagrama | prática ("pronto quando") | fonte |
|---|---|---|---|---|---|---|
| 1 | `semrush-mapa` | O que um "Semrush" faz e de onde vem cada dado | separar, função por função, o que o seu site dá de graça e o que só existe com dado pago | camadas: desempenho, IA oficial, auditoria, quem lê, (pago) volume/concorrente | 1) clonar o repo e rodar os testes; 2) tabela "minhas perguntas × fonte × grátis/pago" | README raiz; SISTEMAS §2, §D |
| 2 | `auditor` | auditor: o raio-x do site inteiro | rodar o auditor no seu site e ordenar os achados por prioridade com a linha de correção | URL → robots (RFC 9309) → sitemap + links → cada página → CDN → relatório | 1) `--max 50` rodado e `relatorio.html` aberto; 2) 3 achados críticos/importantes com a correção | `ferramentas/auditor/README.md`; exemplos/auditor |
| 3 | `agente-ready` | agente-ready: nota 0–100 com pesos públicos | tirar a nota de prontidão do seu site e mudar um peso do pesos.json para ver a nota mudar | 6 categorias → peso → ok/parcial/falha → nota (fora o que não se aplica) | 1) nota + 3 critérios que mais pesam; 2) cópia do pesos.json com 1 peso mudado e a nota nova | `ferramentas/agente-ready/README.md`, `pesos.json` |
| 4 | `gsc-historico` | gsc-historico: o Search Console para sempre | importar os CSV semanais num banco que não apaga e ler marca × sem marca × anônimas | CSV semanal → SQLite → série + subiu/caiu + pauta + sem clique | 1) importar + relatório do exemplo; 2) 3 consultas da pauta com a página que você faria | `ferramentas/gsc-historico/README.md`; exemplos (casos §2.1) |
| 5 | `bing-ia` | bing-ia: citações da IA da Microsoft × Google | cruzar o export do Bing AI Performance com o Google e tirar ideias de conteúdo das grounding queries | painel Bing → CSV → SQLite → cruza com gsc-historico → 4 listas | 1) relatório do exemplo fictício; 2) export do seu Bing importado (ou `--colunas` anotado) | `ferramentas/bing-ia/README.md`; exemplos (fictício, rotulado) |
| 6 | `botlog` | botlog: quem lê o seu site de verdade | separar no log os robôs de IA por finalidade, achar os falsos e filtrar o log antes de guardar | log → UA → finalidade → IP na lista oficial → verdadeiro/falso → relatório | 1) análise da amostra montada; 2) seu log `filtrar` → contagem antes/depois | `ferramentas/botlog/README.md`; exemplos (real filtrado + montado) |
| 7 | `rotina-agente` | Ligando tudo: a rotina com um agente | montar a rotina semanal e mensal das 5 ferramentas e um agente que lê os relatórios e só propõe | semana / mês → ferramentas → JSON → agente lê → portão humano → mudança | 1) `rotina.sh` rodando as ferramentas locais; 2) uma leitura do agente com 3 propostas e a sua decisão | METODO §10 e "máquina com agentes"; READMEs (saídas JSON) |
| 8 | `quando-pagar` | Quando pagar: DataForSEO, Firecrawl, Apify, Semrush | decidir se e quando pagar por dado, com critério, teto e preço conferido, e montar seu plano de ferramentas | pergunta → o grátis responde? → que dado falta → quem vende → teste de 1 mês com teto | 1) tabela de decisão; 2) plano datado pelo gerador | SISTEMAS §1, §C, §D, acréscimo A; README raiz |

Aula 8 fecha com `mapa` (4 degraus: auditor, gsc-historico, bing-ia + botlog, rotina) + `gerador` (8 aulas).

## Simconversa da aula 8 — "o cliente quer assinar Semrush + 3 ferramentas de IA"

Personagem: Carla, dona de uma loja on-line pequena (ficção rotulada). O que ensina vem de SISTEMAS §1, §3, §D e da régua (share of voice não é nota oficial; Ollama não mede; volume exato não existe grátis).

| fala | cliente | opções (nota → destino) |
|---|---|---|
| `abre` | quer assinar Semrush + 3 monitores de IA | assinar já (0 → `fim-caro`) · perguntar que decisão o dado vai mudar (2 → `pergunta`) · "pago não presta, faço tudo grátis" (1 → `radical`) |
| `radical` (desvio) | "então nunca vou saber volume de busca?" | admitir: volume exato só pago (1 → `pergunta`) · "Trends dá o volume" (0 → `fim-errado`) |
| `pergunta` | quer saber se aparece no ChatGPT e quanta gente busca o produto | núcleo grátis + pago só para volume (2 → `monitor`) · só Search Console resolve tudo (1 → `monitor`) · monitor pago dá a nota oficial (0 → `fim-sov`) |
| `monitor` | "a ferramenta mostrou share of voice de 34%" | amostra de prompts, oficial é o Bing; bateria fixa mensal (2 → `piloto`) · confiar (0 → `fim-sov`) · Ollama mede igual (0 → `fim-ollama`) |
| `piloto` | "e quando pagar?" | 1 mês, pergunta definida, teto, preço conferido (2 → `fim-bom`) · plano anual pelo desconto (0 → `fim-caro`) · DataForSEO por chamada sem teto (1 → `fim-bom`) |

Somas à mão: direto 2+2+2+2 = 8; pelo desvio 1+1+2+2+2 = 8 (empata, não passa). Máximo = 8.

## Decisões tomadas sozinho
- "curso 7 de 7" no `sub`/`kicker`; os cursos 1–6 dizem "de 6" (anotado no retorno).
- `lado_card` volta para a área inemaSEO (último curso); `inicio.blocos` lista os 7 cursos.
- Números do INEMA no texto só da lista "Casos reais"; o resto (notas do agente-ready, achados do auditor, contagens do botlog) fica dentro de `saida` com selo real e data.
- bing-ia: exemplo é FICTÍCIO (rotulado assim no repo e na aula); colunas do export são palpite [a confirmar].
- Preços (Firecrawl, Apify, Semrush) só com data e "confira no site"; nenhum serviço pago chamado.
