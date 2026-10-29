# Plano de ataque comercial: Fortaleza e Região Metropolitana

Produtos: água desmineralizada, aditivo para radiador (concentrado e pronto uso) e linha automotiva.
Canais-alvo: lojas de autopeças, postos de combustível, oficinas mecânicas e redes de supermercados.
Ferramenta: o `index.html` desta pasta (mapa de clientes). Todo o plano abaixo é executado e medido nele.

---

## 1. Objetivo e metas (primeiros 90 dias)

| Indicador | Meta 30 dias | Meta 60 dias | Meta 90 dias |
|---|---|---|---|
| Estabelecimentos mapeados no sistema | 600 | 1.000 | 1.400 |
| Visitados pela primeira vez | 150 | 350 | 550 |
| Clientes com 1º pedido (status Ativo) | 30 | 80 | 140 |
| Clientes Fidelizados (3 pedidos seguidos) | 0 | 20 | 60 |
| Redes de supermercado com cadastro aberto | 1 | 2 | 3 |
| Taxa de conversão visita para pedido | 20% | 22% | 25% |

Ajuste os números ao tamanho da equipe. A referência é **1 vendedor externo fazendo 12 a 15 visitas por dia**, 5 dias por semana.

## 2. Como os status funcionam (regra única para toda a equipe)

| Status | Quando usar | Próximo passo obrigatório |
|---|---|---|
| **Potencial** | Mapeado, nunca abordado | Agendar a 1ª visita |
| **Em negociação** | Já houve visita, amostra ou proposta, sem pedido | Data de retorno em até 7 dias |
| **Ativo (não fidelizado)** | Fez 1 ou 2 pedidos, compra esporádica ou divide com concorrente | Rota de reposição a cada 15 ou 30 dias |
| **Fidelizado** | 3 pedidos seguidos, somos o fornecedor principal da categoria | Visita de manutenção e venda de mix |
| **Descartado** | Não compra agora. **Sempre preencher o motivo** | Retomar conforme a tabela da seção 9 |

Outros tipos podem ser criados na aba **Dados > Tipos de status** (ex.: *Inadimplente*, *Concorrente direto*, *Distribuidor parceiro*). Na importação de planilha, um status que não existe vira automaticamente um tipo novo.

Regra de ouro: **nenhum cliente fica sem "Próxima ação" e data**, exceto os descartados. A lista em vermelho ("Atrasado") é a primeira coisa que o vendedor olha de manhã.

## 3. Montagem do mapa (semana 1)

1. **Base automática:** na aba *Dados*, use "Prospecção automática" bairro a bairro (aproxime o mapa, clique em buscar). Ela importa do OpenStreetMap postos, autopeças, oficinas, auto elétricas, lava-jatos e supermercados como *Potencial*.
2. **Complete o que o OSM não tem:** o OpenStreetMap é incompleto em oficinas de bairro. Complete com:
   - Google Maps ("autopeças", "oficina mecânica", "radiador", "auto elétrica" por bairro);
   - lista de clientes antigos e notas fiscais já emitidas (importe pela planilha `modelo-importacao.csv`);
   - indicação dos próprios clientes ("de quem o senhor compra peça? quem mais aqui perto vende?");
   - observação em campo: cada visita deve render ao menos 2 novos pontos cadastrados por clique direito no mapa.
3. **Fábrica/depósito:** marque em *Dados* para que as rotas partam dela.

## 4. Território: dividir para conquistar

Divida a região em setores e fixe um dia da semana para cada um. O cliente passa a esperar o vendedor naquele dia, o que reduz custo de rota e aumenta a reposição.

| Dia | Setor | Bairros / eixos de referência |
|---|---|---|
| Segunda | Oeste e Centro | Centro, Jacarecanga, Álvaro Weyne, Barra do Ceará, Antônio Bezerra, eixo Av. Bezerra de Menezes e Av. Leste-Oeste |
| Terça | Sudoeste | Parangaba, Montese, Maraponga, Mondubim, Bom Jardim, Siqueira, eixo Av. Augusto dos Anjos e Av. Godofredo Maciel |
| Quarta | Sul / BR-116 | Messejana, Cajazeiras, Passaré, Jangurussu, Barroso, eixo BR-116 |
| Quinta | Leste e Sudeste | Aldeota, Papicu, Cocó, Edson Queiroz, Água Fria, Cambeba, eixo Av. Washington Soares e CE-040 |
| Sexta | RMF (alternar) | Semana A: Caucaia e Maracanaú (Distrito Industrial, Anel Viário). Semana B: Eusébio, Aquiraz, Itaitinga, Horizonte |

Os eixos acima são ponto de partida. Depois de 2 semanas, use o filtro por segmento no mapa para ver **onde os pontos se concentram de verdade** e redesenhe os setores para equilibrar o número de visitas por dia.

Prioridade de entrada: **corredores de rodovia e grandes avenidas** (BR-116, BR-222, BR-020, CE-040, Anel Viário). Ali estão postos com alto fluxo, oficinas de caminhão e frotas, que consomem aditivo e água desmineralizada em volume.

## 5. Priorização: quem visitar primeiro

O sistema calcula a prioridade (A, B, C) somando:

- **Peso do segmento:** distribuidor 35, autopeças 30, supermercado 30, posto 25, frota 25, auto elétrica 22, oficina 20, lava-jato 12;
- **Status:** em negociação pesa mais que potencial (já está quente); descartado vai para o fim;
- **Potencial em R$/mês** informado pelo vendedor (até 30 pontos);
- **Faz parte de rede:** +10 (um "sim" abre várias lojas);
- **Ação vencida ou do dia:** +10.

Na aba *Rota*, "Usar prioridade A do filtro atual" monta a rota do dia com os melhores leads do setor, e "Otimizar ordem" encurta o trajeto.

## 6. Estratégia por canal

### 6.1 Lojas de autopeças (canal principal de giro)
- **Por que compram:** margem, giro rápido, produto que o cliente pede pelo nome, entrega sem pedido mínimo alto.
- **Oferta de entrada:** kit de entrada com mix curto (aditivo concentrado 1 L, pronto uso 1 L e 5 L, água desmineralizada 1 L e 5 L), **display de balcão grátis** e prazo de 28 dias no 1º pedido.
- **Argumentos:** preço de fábrica local (sem frete de outro estado), reposição semanal na rota do setor, troca de produto avariado sem burocracia.
- **Meta de visita:** sair com pedido teste ou, no mínimo, amostra deixada e retorno agendado.
- **Venda casada:** quem compra aditivo leva água desmineralizada (para diluir o concentrado e completar bateria).

### 6.2 Postos de combustível
- **Duas portas de entrada:** a loja de conveniência (gôndola) e a pista (frentista oferecendo completar o radiador).
- **Oferta:** expositor de pista, campanha de incentivo para frentista (ex.: bonificação por unidade vendida no mês), produto pronto uso em embalagem pequena.
- **Redes de postos:** cadastrar a rede como "Rede" no sistema e negociar com o comprador central; postos bandeira branca decidem no próprio posto e são mais rápidos de fechar.
- **Extra:** postos de rodovia e com troca de óleo vendem volume maior. Pergunte quem faz a troca de óleo ali: geralmente é um parceiro que também compra.

### 6.3 Oficinas mecânicas, auto elétricas e radiadores
- **Perfil de consumo:** uso profissional, embalagens grandes (galão 5 L, bombona 20 L), aditivo concentrado e água desmineralizada para bateria e arrefecimento.
- **Oferta:** preço por volume, entrega programada, **programa de fidelidade do mecânico** (pontos ou brindes a cada X litros).
- **Por que importa:** o mecânico **indica a marca** para o cliente final e para a autopeças vizinha. Uma oficina fidelizada puxa a loja do bairro.
- **Oficinas de caminhão e frotas** (Maracanaú, Caucaia, BR-116): ticket alto, compra recorrente; trate como conta especial.

### 6.4 Redes de supermercados e atacarejos
- **Ciclo de venda longo** (cadastro de fornecedor, código de barras EAN, tabela, logística, às vezes verba de enxoval). Comece já na semana 1 para colher no mês 2 ou 3.
- **Mapeie no sistema** as redes regionais e atacarejos presentes na região (por exemplo, redes locais de mercadinhos e supermercados de bairro, além dos atacarejos nacionais). Confirme em visita **quais lojas têm gôndola automotiva** e quem é o comprador da categoria.
- **Kit para o comprador:** ficha técnica, fotos, tabela de preço, EAN, laudos, prazos de entrega, proposta de exposição (ponta de gôndola em datas como férias e feriados prolongados, quando as pessoas pegam estrada).
- **Comece pelos mercadinhos e redes pequenas** (decisão no dono, sem cadastro pesado) para ter cases e giro comprovado antes de sentar com a rede grande.

### 6.5 Canais complementares (já previstos no mapa)
- **Lava-jatos e estética automotiva:** água desmineralizada para enxágue sem manchas.
- **Distribuidores / atacado:** para chegar ao interior do Ceará sem frota própria; cuidar para não canibalizar a rota direta da capital.
- **Frotas e transportadoras:** venda direta de volume.

## 7. Cadência de contato (funil)

| Quando | Ação | Status no sistema |
|---|---|---|
| Dia 0 | 1ª visita: apresentar, deixar amostra e tabela, cadastrar contato e potencial | Potencial para Em negociação |
| Dia 2 | WhatsApp: "conseguiu ver o produto?" + foto do display | Em negociação |
| Dia 7 | 2ª visita na rota do setor: fechar pedido teste | Em negociação para Ativo |
| Dia 21 a 30 | Reposição: checar giro, repor, ampliar mix | Ativo |
| 3º pedido seguido | Promover a Fidelizado e oferecer condição de parceiro | Fidelizado |
| Mensal | Visita de manutenção, novos itens, ação de exposição | Fidelizado |

Registre **cada contato** no histórico do cliente (botão "Registrar contato"). Mudanças de status ficam registradas automaticamente.

## 8. Objeções comuns e respostas

| Objeção | Resposta sugerida |
|---|---|
| "Já tenho fornecedor." | "Ótimo, não precisa trocar. Deixa eu colocar um display pequeno ao lado e comparar o giro em 30 dias. Se não vender, eu recolho." |
| "Está caro." | Compare o **preço por litro diluído** (aditivo concentrado rende mais) e a margem do lojista, não só o preço da embalagem. |
| "Não tenho espaço." | Display de balcão ou de pista ocupa pouco; ofereça o mix mínimo de 3 itens. |
| "Ninguém pede essa marca." | Oferecer material de ponto de venda e incentivo para balconista e frentista; o produto local com entrega rápida vira hábito. |
| "Compro só quando falta." | Propor reposição fixa no dia do setor: ele nunca fica sem e não precisa lembrar de pedir. |

## 9. Descartados: não é "não", é "agora não"

| Motivo | Quando voltar | Como voltar |
|---|---|---|
| Preço | 60 dias | Nova condição, promoção de volume ou produto de entrada |
| Fornecedor exclusivo / contrato | Ao fim do contrato (perguntar a data) | Proposta pronta antes do vencimento |
| Não trabalha com o produto | 90 dias | Mostrar giro de vizinhos que passaram a vender |
| Baixo volume | 90 dias | Incluir em rota de distribuidor parceiro |
| Inadimplência / crédito | Só à vista | Pedido à vista ou antecipado |
| Estabelecimento fechou | Não volta | Manter no mapa para ver quem abriu no lugar |
| Fora da área de entrega | Quando a rota chegar lá | Avaliar distribuidor |

Use o filtro de status **Descartado** e a busca por motivo para montar a lista de retomada todo mês.

## 10. Cronograma de 12 semanas

| Semanas | Foco |
|---|---|
| 1 | Montar a base no mapa (OSM + clientes antigos + Google Maps). Definir setores e dia de cada um. Preparar kit de entrada, displays, tabela e material para rede de supermercado. |
| 2 a 4 | Blitz de 1ª visita em autopeças e oficinas dos setores com maior densidade. Iniciar contato com compradores de redes de supermercado e de postos. |
| 5 a 8 | Rota de reposição dos ativos + novas visitas. Programa do mecânico e incentivo de frentista no ar. Primeiras lojas de rede. |
| 9 a 12 | Converter ativos em fidelizados (3º pedido). Expandir para RMF completa. Revisar setores com o mapa e retomar descartados por preço. |

## 11. Rotina semanal de gestão

- **Segunda de manhã (30 min):** filtrar no mapa os atrasados e a prioridade A de cada setor; montar as rotas da semana.
- **Diariamente:** o vendedor atualiza status, próxima ação e histórico no próprio celular ao sair de cada cliente.
- **Sexta à tarde:** exportar o CSV e revisar: visitas feitas, pedidos novos, conversão por segmento (aba *Dados > Resumo por segmento*), motivos de descarte mais frequentes.
- **Mensal:** ajustar preço, oferta e setores conforme os motivos de descarte e o giro real.

## 12. Cuidados

- Confirme as exigências de rotulagem, ficha de segurança e registros aplicáveis a cada produto antes de entrar em redes grandes, que costumam exigir essa documentação no cadastro.
- Na água desmineralizada, deixe claro no rótulo o uso automotivo / industrial.
- Os dados do mapa ficam no navegador. **Faça backup JSON toda semana** e mantenha uma cópia em local seguro.

## 13. Próximos passos sugeridos

1. Abrir o `index.html`, marcar a fábrica e rodar a prospecção automática bairro a bairro.
2. Importar a lista atual de clientes pelo `modelo-importacao.csv`.
3. Definir os setores e o dia de cada um com a equipe.
4. Fechar o kit de entrada (mix, display, condição do 1º pedido).
5. Quando houver mais de um vendedor usando ao mesmo tempo, migrar a base para um servidor compartilhado (o formato JSON exportado já serve de ponto de partida).
