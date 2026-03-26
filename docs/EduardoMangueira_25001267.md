# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: Eduardo Mangueira de Castro Moraes
RA: 25001267
Data: 25/03/2026

---

# 1. Definição do MVP
O MVP desse projeto foca no processo de compreender a entrada do produto no estoque até a conclusão da venda para o consumidor final. O objetivo é validar
o processo desde a venda até a alteração no estoque automática.

## O que está **dentro** do MVP  
- Verificação de estoque em tempo real, pesquisa de produto no inventário pelo nome/código, registro de itens e a finalização da venda.
- Atualização automática de entrada ou saída de produtos, a partir da compra ou venda.
- Registro automático de contas a pagar e contas a receber.

## O que está **fora** do MVP  
- Inicialmente cada unidade gerência seu próprio estoque.
- Registros detalhados de todas alterações importanes, como preços, logins e contas.

## Por que você fez essas escolhas 
Pois isso priorizaria a estabilidade operacional. E também, resolver uma das maiores dores da unidade que é controle de estoque e de contas a pagar.

Exemplo de início:  
> Meu MVP gerencia os processos da venda finalizada, controle de estoque, controle de contas a pagar/receber. Um exemplo seria o clinte deseja comprar um 
produto, e o próprio cliente ou funcionário faz a verificação do produto o estoque, após confirmação, eles dão continuidade a compra e gera um comprovante
de pagamento(registrado no sistema).

---

# 2. Regras de Negócio

**RN01 Venda sem Estoque —
O sistema deve impedir de realizar uma venda se não tiver o produto em questão disponível no estoque.

**RN02 Venda sem Receita —
O sistema não deve permitir a venda de determinados produtos sem a prescrição de uma receita médica

**RN03 Pagamento Sem Comprovante—
Toda transação realizada deve gerar um comprovante de pagamento, e alterar o status no sistema para concluído.

**RN04 Alerta de Estoque —
O sistema deve gerar um alerta sempre que um produto atingir uma determinada quantidade no estoque(Exemplo: 7 Unidades Restantes ou SEM ESTOQUE!)

**RN05 Registro de Contas —
Toda venda parcelada deve ser registrada no sistema e vinculado ao perfil do cliente, com o status "Em aberto".

---

# 3. Requisitos Funcionais 
Liste os requisitos funcionais do seu MVP.

RF01 — Cadastro de Produtos —
O sistema deve permitir que realizemos os cadastros do produto utilizando de informações como: Descrição, Medidas, Preço de Venda e Fabricante.

RF02 — Cadastro de Clientes —
O sistema deve permitir que cadastremos os clientes utilizando de informações como: Nome, CPF/CNPJ, Endereço e e contato.

RF03 — Pesquisa de Produtos —
O sistema deve permitir que os funcionários pesquisem os produos por nome, código de barra.

RF04 — Pesquisa por Clientes —
O sistema deve permitir que o gerente realize pesquisas dos clientes, a partir de dados como Nome e CPF.

RF05 Contas a pagar "Concluídas" —
O sistema deve permitir que seja alterado o status de alguma conta para Concluídas apenas com o comprovante de pagamento.

RF06 — Alteração Manual do estoque —
O sistema deve permitir apenas a alteração manual do estoque sob confirmação do gerente.

RF07 — Controle por Acesso —
O sistema deve impossibilitar certos cargos de realizar determinadas ações, por exemplo, funcionário entrar na região de pegamentos.

RF08 — Listagem de estoque —
O sistema deve listar em um local específico, todos os produtos que estão com baixo estoque.

RF09 — Atualização de estoque —
O sistema deve atualizar automáticamente, após registrar uma compra ou venda de produtos.


# 🛡 4. Requisitos Não Funcionais 
Liste os RNFs do sistema conforme seu MVP.

RNF01 — Tempo de Resposta —
O sistema deve processar a consulta de estoque e a inclusão de itens no carrinho de compras em menos de 2 segundos.

RNF02 —  Criptografia de Dados —
Os dados sensíveis dos clientes (como CPF e histórico de medicamentos) e as senhas de usuários devem ser armazenados utilizando criptografia.

RNF03 —  Disponibilidade —
O sistema deve estar disponível para operação de vendas em pelo menos 99% do tempo durante o horário comercial das farmácias.

RNF04 —  Usabilidade - 
A interface deve ser otimizada para uso rápido, permitindo que a maioria das operações de venda seja realizada apenas via teclado.

---

# 5. Casos de Uso (mínimo: 10)
### Inserir **diagrama de casos de uso geral**, demonstrando claramente:
- os 10 casos
- relação entre eles e atores
- pelo menos 3 includes
- pelo menos 3 extends

---

# 6. Documentação dos Casos de Uso
Para **cada caso de uso**, utilize o template abaixo:
---

- Diagrama Geral:

  <img width="748" height="664" alt="image" src="https://github.com/user-attachments/assets/edfcb665-311d-474a-a225-33a22b5a75fe" />

------------------------------------------------------------------------------------------------------------------------------------------------------------

UC01 — Realizar Venda de Produto
Ator: Atendente

Descrição: Processo de venda de itens de conveniência ou medicamentos comuns ao cliente

Pré-condições: Usuário logado no sistema e Produto com estoque disponível

Pós-condições: Venda registrada, estoque atualizado e comprovante gerado

Fluxo Principal
- Atendente inicia uma nova venda

- Atendente pesquisa e adiciona o produto ao carrinho (RF03)

- Sistema verifica disponibilidade de estoque em tempo real (RF04/RN01)

- Atendente seleciona a forma de pagamento e finaliza a operação

Fluxos Alternativos / Exceções
- FA01 — Estoque Insuficiente: O sistema bloqueia a adição do item e emite alerta (RN01)

- FA02 — Produto Controlado: O sistema exige a validação do Farmacêutico (Extend UC02)

Relacionamentos
- Include: UC09 

- Extend: UC02, UC05

<img width="472" height="743" alt="image" src="https://github.com/user-attachments/assets/22693f39-9465-4483-8ddb-5b37fec8028a" />


------------------------------------------------------------------------------------------------------------------------------------------------------------

UC02 — Validar Receita Médica
Ator: Farmacêutico

Descrição: Autorização obrigatória para venda de medicamentos controlados ou antibióticos

Pré-condições: Venda em andamento com item controlado no carrinho

Pós-condições: Item liberado para venda e dados da receita vinculados à transação

Fluxo Principal
- Sistema solicita credenciais do Farmacêutico

- Farmacêutico insere login e senha

- Farmacêutico registra dados da receita (CRM, nome do médico, data)

- Sistema libera o item para o fechamento do caixa

Fluxos Alternativos / Exceções
- FA01 — Receita Vencida/Inválida: Farmacêutico recusa a venda e o item é removido do carrinho

Relacionamentos
- Extend: UC01 

<img width="422" height="422" alt="image" src="https://github.com/user-attachments/assets/879a6658-ab84-430d-be2e-aa72310cb922" />


------------------------------------------------------------------------------------------------------------------------------------------------------------

UC03 — Cadastrar/Atualizar Cliente
Atorse: Atendente ou Gerente

Descrição: Registro de dados do cliente no banco de dados

Pré-condições: CPF/CNPJ do cliente não deve estar duplicado

Pós-condições: Cliente habilitado para compras a prazo e histórico

Fluxo Principal
- Usuário acessa o módulo de clientes

- Insere Nome, CPF/CNPJ, Endereço e Contato (RF02)

- Sistema valida o formato dos documentos

- Sistema salva o registro com sucesso

Fluxos Alternativos / Exceções
- FA01 — Cliente já cadastrado: Sistema sugere a edição do cadastro existente.

Relacionamentos
- Extend: UC01

<img width="446" height="477" alt="image" src="https://github.com/user-attachments/assets/d9acf1d2-b5c2-43f9-bb0c-6017b569622f" />

  
------------------------------------------------------------------------------------------------------------------------------------------------------------

UC04 — Consultar Estoque em Tempo Real
Ator: Atendente ou Gerente

Descrição: Verificação rápida de saldo e localização de produtos

Pré-condições: Nenhuma

Pós-condições: Informação exibida em tela

Fluxo Principal
- Usuário digita o nome ou lê o código de barras do produto

- Sistema busca no inventário da unidade

- Sistema exibe quantidade disponível e preço de venda

Fluxos Alternativos / Exceções
- FA01 — Produto não localizado: Sistema sugere busca por fabricante ou parte do nome

Relacionamento:
- Dentro da UC01, mas independente.

<img width="517" height="367" alt="image" src="https://github.com/user-attachments/assets/8ce0c609-da3c-4680-bc04-58ae7c201cab" />


------------------------------------------------------------------------------------------------------------------------------------------------------------

UC05 — Registrar Venda a Prazo
Ator: Atendente

Descrição: Geração de dívida para clientes conveniados ou parcelados

Pré-condições: Venda em andamento e cliente cadastrado (UC03)

Pós-condições: Registro criado no Contas a Receber com status "Em Aberto" (RN05)

Fluxo Principal
- Atendente seleciona forma de pagamento "A Prazo" ou "Convênio"

- Atendente vincula o CPF do cliente à venda

- Sistema registra o valor total e data de vencimento

Fluxos Alternativos / Exceções
- FA01 — Cliente não localizado: Sistema exige a execução do UC03 antes de prosseguir

Relacionamento:
- Extend: UC01

<img width="261" height="413" alt="image" src="https://github.com/user-attachments/assets/5cf28f44-2114-4b81-be9f-352dea3422ff" />


------------------------------------------------------------------------------------------------------------------------------------------------------------

UC06 — Dar Entrada em Mercadoria (Compra)
Ator: Gerente

Descrição: Entrada manual de novos produtos adquiridos de fornecedores

Pré-condições: Fornecedor cadastrado; NF em mãos

Pós-condições: Estoque incrementado; Registro no Contas a Pagar criado

Fluxo Principal
- Gerente acessa a região de Compras/Entradas

- Seleciona o produto e informa a quantidade recebida

- Sistema atualiza o saldo do estoque automaticamente (RF09)

- Sistema gera lançamento automático no Contas a Pagar

Fluxos Alternativos / Exceções
- FA01 — Produto Novo: Gerente deve realizar o RF01 (Cadastro de Produto) primeiro

Relacionamento:
Include: UC09

<img width="270" height="358" alt="image" src="https://github.com/user-attachments/assets/41db4158-51a3-4a46-9fba-d19a1c9e4da0" />

------------------------------------------------------------------------------------------------------------------------------------------------------------

UC07 — Ajustar Estoque Manualmente
Ator: Gerente

Descrição: Ajustes por perdas, quebras ou erros de contagem

Pré-condições: Perfil de Gerente verificado (RF06)

Pós-condições: Saldo de estoque corrigido e justificativa registrada

Fluxo Principal
- Gerente seleciona o produto no inventário

- Informa a nova quantidade real

- Gerente seleciona o motivo (Perda, Avaria, Erro)

- Sistema salva a alteração após confirmação de senha

Fluxos Alternativos / Exceções
- FA01 — Tentativa de ajuste por Atendente: Sistema bloqueia a ação (RF07)

Relacionamento:
- Indenpendente

<img width="306" height="496" alt="image" src="https://github.com/user-attachments/assets/fa16e943-f4a8-4a73-8ee0-f2dd3491ad62" />


------------------------------------------------------------------------------------------------------------------------------------------------------------

UC08 — Baixar Conta a Pagar
Atores: Gerente ou Financeiro

Descrição: Registro do pagamento de uma dívida com fornecedor

Pré-condições: Existência de um título "Em Aberto"

Pós-condições: Status da conta alterado para "Concluída"

Fluxo Principal
- Usuário pesquisa o título no módulo financeiro

- Seleciona a opção de realizar pagamento

- Sistema solicita o documento ou número do comprovante (RF05)

- Sistema altera o status para "Concluída"

Fluxos Alternativos / Exceções:
- FA01 — Comprovante Não Anexado: O sistema impede a conclusão da baixa, conforme a RF05.

- FA02 — Conta Já Paga: O sistema exibe aviso de que o título já foi liquidado e bloqueia nova alteração.

Relacionamentos:
- Independente
<img width="412" height="477" alt="image" src="https://github.com/user-attachments/assets/7553e1a0-3dc7-4a58-a92a-821ce9feb57f" />

- 
------------------------------------------------------------------------------------------------------------------------------------------------------------

UC09 — Emitir Comprovante de Venda
Ator: Sistema

Descrição: Geração automática do comprovante de transação (RN03)

Pré-condições: Venda finalizada com sucesso

Pós-condições: Comprovante disponível para impressão ou envio digital

Fluxo Principal
- Sistema agrupa dados da venda (Produtos, Total, Atendente)

- Sistema gera o documento com status "Concluído"

- Sistema envia o comando para a impressora térmica ou exibe PDF

Fluxos Alternativos / Exceções:
- FA01 — Falha na Impressora: O sistema permite salvar o comprovante em formato digital (PDF) para envio posterior.

- FA02 — Dados Incompletos: O sistema gera um alerta de erro e impede a finalização da transação até que os dados obrigatórios apareçam.

Relacionamento:
- Include: UC01, UC06 e UC08

<img width="407" height="363" alt="image" src="https://github.com/user-attachments/assets/cffe1e60-23a9-4a9b-9598-b9af724180fc" />

  
------------------------------------------------------------------------------------------------------------------------------------------------------------

UC10 — Monitorar Produtos com Baixo Estoque
Ator: Gerente

Descrição: Visualização de itens que precisam de reposição urgente

Pré-condições: Nível de estoque mínimo configurado nos produtos

Pós-condições: Lista de reposição gerada

Fluxo Principal
- Gerente acessa o relatório de Estoque Crítico (RF08)

- Sistema filtra todos os produtos com quantidade ≤ Estoque Mínimo

- Sistema exibe a lista com alertas visuais (RN04)

- O Gerente exporta a lista para o setor de compras

Fluxos Alternativos / Exceções:
- FA01 — Nenhum Produto Abaixo do Mínimo: O sistema exibe a mensagem "Estoque em conformidade".

- FA02 — Produto sem Configuração de Mínimo: O sistema ignora o produto no relatório de alerta, mesmo que esteja zerado (Exceção de cadastro).

Relacionamentos:
- Include: UC01, UC06 e UC07

<img width="320" height="475" alt="image" src="https://github.com/user-attachments/assets/84d5096f-5771-486b-9f97-21150b476cd4" />

