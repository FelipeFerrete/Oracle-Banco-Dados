# Oracle-Banco-Dados-Relacional
# Documentação do Banco de Dados Relacional

Este projeto contém o modelo de dados de um sistema relacional desenvolvido para a gestão de clientes, fornecedores, produtos, pedidos e mais. O modelo foi criado utilizando o Oracle SQL Developer Data Modeler e está preparado para rodar em um banco de dados Oracle 11g.

## Tabelas

Abaixo estão as principais tabelas criadas para o sistema:

### `clientes`
Tabela que armazena informações sobre os clientes, incluindo nome, endereço, tipo (físico ou jurídico) e situação.

- `cliente_codigo` (PK): Código único do cliente.
- `situacao_cliente` (FK): Referência à tabela `situacao_clientes`.
- `endereco_cep` (FK): Referência à tabela `enderecos_ceps`.
- `cliente_nome`: Nome do cliente.
- `cliente_tipo`: Tipo de cliente ('F' para físico e 'J' para jurídico).
  
### `clientes_telefones`
Tabela que armazena os números de telefone dos clientes.

- `cliente_codigo` (FK): Referência à tabela `clientes`.
- `ddd`: DDD do telefone.
- `numero`: Número do telefone.

### `enderecos_ceps`
Tabela que contém os dados de endereços, incluindo o CEP, rua, bairro, cidade e estado.

- `endereco_cep` (PK): Código do CEP.
- `endereco_rua`: Nome da rua.
- `endereco_bairro`: Bairro do endereço.
- `endereco_cidade`: Cidade do endereço.
- `endereco_estado`: Estado do endereço.

### `fornecedores`
Tabela que armazena informações sobre os fornecedores, incluindo nome, endereço e telefone.

- `fornecedor_codigo` (PK): Código do fornecedor.
- `fornecedor_nome`: Nome do fornecedor.
- `endereco_cep` (FK): Referência à tabela `enderecos_ceps`.
- `fornecedor_telefone`: Número de telefone do fornecedor.

### `fornecedores_produtos`
Tabela de relação entre fornecedores e produtos.

- `fornecedor_codigo` (FK): Referência à tabela `fornecedores`.
- `produto_codigo` (FK): Referência à tabela `produtos`.

### `lista_precos`
Tabela que armazena os preços dos produtos em diferentes listas de preços.

- `produto_codigo` (FK): Referência à tabela `produtos`.
- `lista_codigo` (PK): Código único da lista de preços.
- `lista_valor`: Preço do produto na lista de preços.
- `lista_data`: Data de validade da lista de preços.

### `pedidos`
Tabela que armazena os pedidos realizados pelos clientes.

- `pedido_numero` (PK): Número único do pedido.
- `cliente_codigo` (FK): Referência à tabela `clientes`.
- `vendedor_codigo` (FK): Referência à tabela `vendedores`.
- `pedido_data`: Data do pedido.
- `pedido_tipo`: Tipo de pedido.
- `pedido_situacao`: Situação do pedido.

### `pedidos_itens`
Tabela que detalha os itens de cada pedido.

- `item_codigo` (PK): Código único do item.
- `pedido_numero` (FK): Referência à tabela `pedidos`.
- `lista_precos_lista_codigo` (FK): Referência à tabela `lista_precos`.
- `item_quantidade`: Quantidade do produto no pedido.
- `item_situacao`: Situação do item (aguardando, entregue, produzido).

### `pessoa_fisica`
Tabela que armazena as informações de clientes do tipo físico.

- `cliente_codigo` (FK): Referência à tabela `clientes`.
- `data_nascimento`: Data de nascimento do cliente.

### `pessoa_juridica`
Tabela que armazena as informações de clientes do tipo jurídico.

- `cliente_codigo` (FK): Referência à tabela `clientes`.
- `inscricao_estadual`: Número de inscrição estadual.
- `cnpj`: Número do CNPJ.

### `produtos`
Tabela que contém os produtos disponíveis no sistema.

- `produto_codigo` (PK): Código do produto.
- `produto_nome`: Nome do produto.

### `situacao_clientes`
Tabela que define a situação dos clientes (ex: ativo, inativo).

- `situacao_cliente` (PK): Código da situação do cliente.
- `situacao_descricao`: Descrição da situação.

### `vendedores`
Tabela que armazena as informações dos vendedores.

- `vendedor_codigo` (PK): Código do vendedor.
- `vendedor_nome`: Nome do vendedor.
- `vendedor_valor_comissao`: Valor da comissão do vendedor.

## Relacionamentos

O banco de dados possui as seguintes relações:

- **Clientes** e **Endereços**: Cada cliente está associado a um único endereço (CEP).
- **Clientes** e **Telefones**: Um cliente pode ter múltiplos telefones.
- **Clientes** e **Pedidos**: Um cliente pode realizar múltiplos pedidos.
- **Pedidos** e **Vendedores**: Cada pedido é vinculado a um vendedor.
- **Pedidos** e **Itens de Pedido**: Cada pedido pode conter múltiplos itens.
- **Fornecedores** e **Produtos**: Um fornecedor pode fornecer múltiplos produtos.
- **Produtos** e **Listas de Preço**: Cada produto pode ter múltiplos preços em diferentes listas.

## Constraints e Triggers

- **Chaves estrangeiras (FK)**: São usadas para garantir a integridade referencial entre as tabelas.
- **Triggers**: Existem triggers que garantem que clientes do tipo 'F' (físico) só possam ser inseridos na tabela `pessoa_fisica` e clientes do tipo 'J' (jurídico) só possam ser inseridos na tabela `pessoa_juridica`.

## Considerações

Este modelo foi desenvolvido para ser utilizado em um sistema de gestão de clientes, pedidos e fornecedores. Ele permite flexibilidade para adicionar mais informações, como histórico de preços e controle de estoque, caso necessário.

## Instruções de Uso

1. Clone este repositório para o seu ambiente local.
2. Execute os scripts SQL no seu banco de dados Oracle.
3. Importe ou insira os dados conforme necessário para testar o modelo.

## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para mais detalhes.
