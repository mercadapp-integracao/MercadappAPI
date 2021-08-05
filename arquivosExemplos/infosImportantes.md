<h1 align="center">Informações Importantes</h1>

Baseado em nossas experiências e com o intuito de manter a ferramenta sempre com um processamento satisfatório, estaremos listando algumas recomendações que colhemos ao longo das nossas integrações realizadas.

## Sobre o Envio de Cargas (arquivos CSV)

### csv_create_products

- Enviar um arquivo semanalmente, preferencialemnte às quintas entre 06h00 e 07h00, com todos os produtos cadastrados nos últimos sete dias.

### csv_price

- Enviar arquivos diariamente com início entre 06h00 e 07h00, a cada três horas com produtos que tiveram alteração de preço no dia corrente;
- Enviar um arquivo semanalmente entre 00h00 e 06h00, com todos os produtos, aplicando filtros que permitam trazer apenas os ativos e que a loja efetivamente trabalhe, para cobrir algum produto que não tenha sido enviado nas diárias.

**Obs.:** Essa carga é responsável por associar os produtos da loja aos da nossa base pelo EAN caso seja o primeiro envio do produto.

### csv_stock

- Enviar arquivos diariamente com início entre 06h00 e 07h00, a cada oito horas com produtos que tiveram alteração de estoque no dia corrente;
- Enviar um arquivo semanalmente com o estoque de todos os produtos para cobrir algum produto que não tenha sido enviado nas diárias.

### csv_offer_schedule
- Enviar arquivos diariamente com início entre 06h00 e 07h00, a cada oito horas com as ofertas vigentes no dia corrente.

### csv_club_offer_schedule
- Enviar arquivos diariamente com início entre 06h00 e 07h00, a cada oito horas com as ofertas de clube/CRM vigentes no dia corrente.

### Observações gerais

**Sempre buscar aplicar filtros que permitam trazer dados apenas para os produtos ativos e que a loja efetivamente trabalhe. Levar em consideração as movimentações de estoque por períodos é uma das maneiras que aplicamos, geralmente o range de 180 dias atende bem.**

**Enviar cargas semanais sugeridas anteriormente com uma diferença de pelo menos 30 minutos de uma para outra, para evitar que sejam processadas duas cargas grandes ao mesmo tempo.**

**Por padrão, arquivos CSV enviados com mais de 15000 linhas só serão processados entre 22h00 e 06h00 da manhã, para garantir um alto nível de estabilidade da ferramenta.**

## Sobre a Consulta de Pedidos

Por padrão recomendamos realizar a consulta se tem novos pedidos a cada 5 minutos iniciando a partir do horário que a loja abre, até o horário que a loja fecha.

---

[:house:](https://github.com/mercadapp-integracao/MercadappAPI)
