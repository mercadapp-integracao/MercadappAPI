# ARQUIVO DE PEDIDO COMENTADO      
      
        {
            "orders": [                                                         //orders -> Array de pedidos
                {
                    "2021430933846": {                                          //2021430933846 -> Objeto pedido
                        "id": 933846,                                           // id do pedido no merconnect
                        "service_tax": "0.0",                                   // taxa de serviço
                        "custom_bag": "0.0",                                    //valor de embalagem customizada
                        "delivery_tax": "10.0",                                 // taxa de entrega
                        "total_taxes": "10.0",                                  // soma taxa de serviço e entrega
                        "delivery_type": "delivery",                            // tipo de entrega
                        "delivery_tax_calculation_method": null,                // calcula por método de entrega
                        "drivethru_method": "default",                          // método de retirada
                        "delivered_at": "01/05/2021",                           // data de entrega
                        "created_at": "30/04/2021 15:02:29",                    // data da criação do pedido
                        "number_of_times_sent_to_pdv": 0,                       // tentativas de envio para o pdv
                        "client": {                                             // dados do cliente    
                            "id": 933945,                                           // id do cliente no merconnect
                            "phone_number": "85999999999",                          // número de telefone do cliente
                            "second_phone_number": "",                              // número de telefone 2    
                            "email": "MERCADAPPTESTE@MERCADAPP.COM",                // e-mail do cliente
                            "preferences": "NAO SEPARAR TESTE MERCADAPP",           // mensagem para a loja
                            "state_registration": "",                               //
                            "exempted_from_state_registration": true,               // 
                            "name": "MERCADAPP TESTE",                              // nome do cliente
                            "cpf": "99999999999",                                   // cpf do cliente
                            "address": {                                            // dados de endereço de entrega
                                "cep": "99999-999",                                     // cep do endereço
                                "street": "RUA TESTE DO PEDIDO",                        // logradouro
                                "number": "500",                                        // número da residência
                                "complement": "",                                       // complemento
                                "neighborhood": "CENTRO",                               // bairro
                                "city": "FORTALEZA",                                    // cidade    
                                "state": "SP",                                          // UF
                                "reference_spot": ""                                    // ponto de referência    
                            }
                        },
                        "items": [                                                      // Array de itens do pedido
                            {
                                "market_system_code": "59876",                          // código interno do produto
                                "bar_code": "07898366000139",                           // código de barras do produto
                                "amount": "00000000001.000",                            // quantidade de itens
                                "price": "00000000006.010",                             // preço unitário
                                "unitary_price_with_discount": "00000000006.010",       // preço unitário com desconto
                                "total_price": "00000000006.010",                       // preço total (amount x unitary_price_with_discount)
                                "promotional_relative_discount": "00000000000.000",     // desconto no item    
                                "total_discount": "00000000000.000"                     // total de descontos
                            },
                            {
                                "market_system_code": "95678",
                                "bar_code": "07896010400861",
                                "amount": "00000000003.000",
                                "price": "00000000010.050",
                                "unitary_price_with_discount": "00000000010.050",
                                "total_price": "00000000030.150",
                                "promotional_relative_discount": "00000000000.000",
                                "total_discount": "00000000000.000"
                            }
                        ],
                        "payment_type_market_system_code": 1,                   // código do pagamento cadastrado no merconnect
                        "subtotal": "00000000036.160",                          // valor total dos itens
                        "total_price": "00000000046.160",                       // valor total do pedido
                        "total_discounts": "00000000000.000"                    // valor total dos descontos
                    }
                }
            ]
        }