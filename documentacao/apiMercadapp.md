# API de Integração Mercadapp


# 00001 Autenticação de sessão (Utilizado para Retaguarda e PDV)

## Rota 1.1
##### - Autenticar sessão

        POST - {{base_url}}/oauth/token

### Headers

    Accept: application/json
    Content-Type: application/json

### Body - RAW

    {
        "client_id":"111111111111111aaaaaaaaaaaaBBBBBBBBBccccc22222",   //Solicitar a Mercadapp
        "grant_type":"password",
        "username": "****",                                             //Solicitar a Mercadapp
        "password": "****",                                             //Solicitar a Mercadapp
        "scope": "api_cli"
    }

### Responses

- JSON de autenticação de sessão do usuário, deve-se armazenar o valor do atributo access_token para que seja utilizado nas novas requisições.

        {
            "access_token": "00000000000aaaaaaaaaaaaaaaaaBBBBBBBBBBBB111111111111111111",
            "token_type": "Bearer",
            "expires_in": 3600,
            "refresh_token": "00000000000aaaaaaaaaaaaaaaaaBBBBBBBBBBBB22222222222222222",
            "scope": "api_cli",
            "created_at": 1620135135
        }

**Obs.:** o access_token gerado pode ser utilizado pelo período de uma hora, após esse tempo deve ser gerado um novo.

# 00002 Dados referentes a Venda (Utilizado para PDV)

## Rota 2.1
##### - Consulta de pedidos prontos para importar

        GET - {{base_url}}/apicli/v2/orders

### Headers

    Content-Type: application/json
    Accept: application/json
    Authorization: Bearer {{access_token}}

### Responses

Retorno de JSON completo de todos os pedidos prontos a serem importados. 

**Exemplo:** exemploPedido.json

[ARQUIVOS DE EXEMPLO](https://github.com/mercadapp-integracao/MercadappAPI/tree/main/arquivosExemplos)

**Detalhamento dos campos:**

[PEDIDO DETALHADO](https://github.com/mercadapp-integracao/MercadappAPI/blob/main/arquivosExemplos/camposPedido.md)

## Rota 2.2
##### - Envio do número do PDV para o Merconnect após o processamento do pedido pelo ERP (será usado para puxar o pedido em questão no caixa da loja)

        PATCH - {{base_url}}/apicli/v2/orders/{{id}}

### Headers

    Content-Type: application/json
    Authorization: Bearer {{access_token}}

### Body - RAW

- **pdv_number**: Numero do PDV
- **pdv_note**: Mensagem - opcional

        {
            "order": {
                "pdv_number": "1234",
                "pdv_note": "Nota"
            }
        }

# 00003 Envio de arquivos Batches (Utilizado para Retaguarda)

## Rota 3.1
##### - Atualização de dados dos produtos (preços, ofertas, estoques, etc)

        POST - {{base_url}}/apicli/v2/batches

### Headers

    Authorization: Bearer {{access_token}}


### Body - form-data

    batch[kind]: {{tipo_arquivo}}
    batch[attachment]: {{arquivo_csv}}

### Kind's existentes

- **csv_price**: Atualiza Preços
- **csv_stock**: Atualiza Estoques
- **csv_offer_schedule**: Atualiza Ofertas Normais
- **csv_club_offer_schedule:** Atualiza Ofertas Clube
- **csv_create_products**: Sobe Produtos Novos Para Cadastro

Cada tipo de CSV tem que seguir um padrão de cabeçalho e dados, segue abaixo cada um dos tipos de Kind's:

- **csv_price**

        Cabeçalho: codigo_de_barras,preço,market_system_code
        Corpo: código de barras do produto acompanhado pelo preço e pelo código interno, separados por vírgula

        Padronizações:
        Código de barras não deve conter zeros a esquerda nem quaisquer caracteres
        adicionais.
        Preço deve ter o valor dos centavos em duas casas decimais, separados por “.” e
        não deve conter zeros a esquerda.
        Código interno do produto sem caracteres adicionais.

- **csv_stock**

        Cabeçalho: codigo_de_barras,estoque
        Corpo: código de barras do produto acompanhado pelo seu estoque atual, separados
        por vírgula

        Padronizações:
        Código de barras não deve conter zeros a esquerda nem quaisquer caracteres
        adicionais.
        Estoque deve ter gramaturas em até três casas decimais, separadas por “.” e não
        deve conter zeros a esquerda.

- **csv_offer_schedule**

        Cabeçalho: codigo_de_barras,oferta,data_inicio,data_fim
        Corpo: código de barras do produto acompanhado pelo preço da oferta, data de inicio
        da oferta e data de fim, separados por vírgula

        Padronizações:
        Código de barras não deve conter zeros a esquerda nem quaisquer caracteres
        adicionais.
        Preço de oferta deve ter o valor dos centavos em duas casas decimais, separados
        por “.” e não deve conter zeros a esquerda.
        As datas devem ser dispostas no formato Ano-Mês-Dia. Ex: 31 de janeiro de 2018
        ficaria 2018-01-31.

- **csv_club_offer_schedule**

        Cabeçalho: codigo_de_barras,oferta,data_inicio,data_fim
        Corpo: código de barras do produto acompanhado pelo preço da oferta do clube, data de inicio
        da oferta e data de fim, separados por vírgula

        Padronizações:
        Código de barras não deve conter zeros a esquerda nem quaisquer caracteres
        adicionais.
        Preço de oferta do clube deve ter o valor dos centavos em duas casas decimais, separados
        por “.” e não deve conter zeros a esquerda.
        As datas devem ser dispostas no formato Ano-Mês-Dia. Ex: 31 de janeiro de 2018
        ficaria 2018-01-31.

- **csv_create_products**

        Cabeçalho: codigo_de_barras,descricao
        Corpo: código de barras do produto acompanhado pela descrição, separados por
        vírgula

        Padronizações: Código de barras não deve conter zeros a esquerda nem quaisquer caracteres adicionais. 
        Descrição completa do produto
        
**No link abaixo tem exemplos dos arquivos como devem ser formatados:**

[ARQUIVOS DE EXEMPLO](https://github.com/mercadapp-integracao/MercadappAPI/tree/main/arquivosExemplos)

