# Mapa de Clientes: Fortaleza e RMF

Sistema web para mapear e trabalhar a carteira de clientes de produtos automotivos
(água desmineralizada, aditivo para radiador e linha automotiva) em Fortaleza e
Região Metropolitana.

O plano comercial que usa este mapa está em [`PLANO_DE_ATAQUE.md`](PLANO_DE_ATAQUE.md).

## Como abrir

É um único arquivo, sem instalação: abra `index.html` no navegador (computador ou
celular). Precisa de internet para carregar o mapa.

Para usar no celular da equipe, publique a pasta em qualquer hospedagem estática
(GitHub Pages, Netlify etc.) ou envie o arquivo e abra no navegador.

## O que faz

- **Mapa por status:** cada cliente é um pino colorido pelo status e com a letra
  do segmento (Pç autopeças, P posto, O oficina, S supermercado, E auto elétrica,
  L lava-jato, D distribuidor, F frota).
- **Status:** Potencial, Em negociação, Ativo (não fidelizado), Fidelizado,
  Descartado (com motivo obrigatório) e quantos tipos novos você criar.
- **Cadastro completo:** rede, endereço com busca no mapa, contato, WhatsApp,
  produtos de interesse, potencial em R$/mês, concorrente, próxima ação e data,
  histórico de contatos.
- **Prioridade A/B/C automática**, puxada principalmente pelo tamanho da conta:
  potencial em R$/mês, porte da loja, fluxo e número de lojas da rede. As
  contas A aparecem com pino grande e destacado, sempre visíveis; as C, com pino
  pequeno.
- **Prospecção automática:** importa do OpenStreetMap postos, autopeças, oficinas,
  auto elétricas, lava-jatos e supermercados da área visível como leads.
- **Rota do dia:** escolhe agendados ou as maiores contas, ordena pelo caminho mais curto e
  abre no Google Maps.
- **Filtros** por status, segmento, cidade, prioridade e busca livre.
- **Importação e exportação:** CSV (abre no Excel) e backup JSON.

## Atalhos

- Clique direito (ou toque longo no celular) no mapa: novo cliente naquele ponto.
- Duplo clique num filtro de status ou segmento: mostra só aquele.

## Importar planilha

Use `modelo-importacao.csv` (separador `;`). As colunas `segmento`, `status`,
`porte` (Grande, Médio, Pequeno) e `fluxo` (Alto, Médio, Baixo)
aceitam os nomes por extenso ("Posto de combustível", "Fidelizado"). Um status
desconhecido vira um tipo novo automaticamente. Produtos separados por `|`.
Linhas sem `lat`/`lng` entram na lista marcadas "Sem localização": abra o
cliente e use "Localizar" ou "Marcar ponto no mapa".

## Onde ficam os dados

Sem configuração, no armazenamento do navegador (`localStorage`): cada navegador
tem a sua base. Use **Dados > Backup JSON** para guardar ou passar a base para
outra pessoa.

Com a **base compartilhada da equipe** ligada, os clientes ficam no Firebase
(Google) e todos os vendedores liberados veem e editam a mesma base em tempo
real, cada um com a própria conta Google. Como ligar:
[`BASE_COMPARTILHADA.md`](BASE_COMPARTILHADA.md).
