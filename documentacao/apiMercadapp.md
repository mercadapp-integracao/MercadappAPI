[comentário]: # (Habilitar visualização em Markdown para ter uma melhor experiência)

# API de Integração Mercadapp


# 00001 Autenticação de sessão

## Rota 1.1
##### - Autenticar sessão

        POST - {{base_url}}/oauth/token

### Headers

    Accept: application/json
    Content-Type: application/json

### Body - RAW

    {
        "client_id":"111111111111111aaaaaaaaaaaaBBBBBBBBBccccc22222",
        "grant_type":"password",
        "username": "****",
        "password": "****",
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

# 00002 Dados referentes a Venda

## Rota 2.1
##### - Consulta de pedidos prontos para importar

        GET - {{base_url}}/apicli/v2/orders

### Headers

    Content-Type: application/json
    Accept: application/json
    Authorization: Bearer {{access_token}}

### Responses

Retorno de JSON completo de todos os pedidos prontos a serem importados. 

**Exemplo:**
https://github.com/mercadapp-integracao/MercadappAPI/tree/main/arquivosExemplos

Detalhamento dos campos: 


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

# 00003 Envio de arquivos Batches

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
        
        Exemplo de Arquivo:

        codigo_de_barras,preço,market_system_code
        78928503,11.45,12452
        7896014192922,8.99,1104
        420,16.90,13759
        437,31.90,11048

- **csv_stock**

        Cabeçalho: codigo_de_barras,estoque
        Corpo: código de barras do produto acompanhado pelo seu estoque atual, separados
        por vírgula

        Padronizações:
        Código de barras não deve conter zeros a esquerda nem quaisquer caracteres
        adicionais.
        Estoque deve ter gramaturas em até três casas decimais, separadas por “.” e não
        deve conter zeros a esquerda.
        
        Exemplo de Arquivo:

        codigo_de_barras,estoque
        7891150038578,3
        7891150038585,3
        4529,0
        4531,0

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
        
        Exemplo de Arquivo:

        codigo_de_barras,oferta,data_inicio,data_fim
        7891152301168,5.59,2019-01-15,2019-02-28
        7891152300116,4.19,2019-01-15,2019-02-28
        7500435115353,25.89,2019-01-15,2019-02-28
        7891152222081,6.99,2019-01-15,2019-02-28 

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
        
        Exemplo de Arquivo:

        codigo_de_barras,oferta,data_inicio,data_fim
        7891152301168,5.59,2019-01-15,2019-02-28
        7891152300116,4.19,2019-01-15,2019-02-28
        7500435115353,25.89,2019-01-15,2019-02-28
        7891152222081,6.99,2019-01-15,2019-02-28 

- **csv_create_products**

        Cabeçalho: codigo_de_barras,descricao
        Corpo: código de barras do produto acompanhado pela descrição, separados por
        vírgula

        Padronizações: Código de barras não deve conter zeros a esquerda nem quaisquer caracteres adicionais. 
        Descrição completa do produto
        
        Exemplo de Arquivo:

        codigo_de_barras,descricao
        7896108300165,MOLHO INGLES REGINA GF 500ML
        7898200380069,MANTEIGA VALEMILK COM SAL 500G
        
**Obs.:** Por padrão, arquivos CSV enviados com mais de 15000 linhas só serão processados entre 22h00 e 06h00 da manhã, para garantir um alto nível de estabilidade da ferramenta.

