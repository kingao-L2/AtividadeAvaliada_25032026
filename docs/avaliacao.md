Avaliação — Engenharia de Software
Sistema Integrado de Gestão de Farmácia — Saúde & Vida
Aluno: KAYKY JUAN TAVARES DOS REIS
RA: 25000079
Dados: 25/03/2026

1. Definição do MVP
Meu MVP cobre o núcleo operacional de vendas e controle de estoque, garantindo que a farmácia possa transacionar produtos com segurança e integridade financeira.

O que está dentro do MVP: Cadastro de produtos e clientes, realização de vendas (à vista e a prazo), consulta e baixa automática de estoque, validação de receitas para controlados e emissão de comprovantes.

O que está fora do MVP: Módulo de compras com fornecedores, transferências entre unidades, relatórios de auditoria internacional e gestão de contas a pagar (despesas administrativas).

Escolhas: Foquei em resolver o problema imediato de "estoques divergentes" e "falhas no registro de vendas", que são os gargalos que afetam diretamente o faturamento e o atendimento ao cliente.

2. Regras de Negócio 
RN01 — Bloqueio de Estoque Negativo: O sistema impede a finalização de vendas de produtos cuja quantidade solicitada seja superior ao saldo atual da unidade.

RN02 — Retenção de Receita: Medicamentos classificados como "Controlados" só podem ter a venda concluída mediante inserção dos dados do CRM do médico e autorização do Farmacêutico.

RN03 — Limite de Crédito: Vendas a prazo (Contas a Receber) só são permitidas para clientes com cadastro ativo e sem parcelas vencidas há mais de 15 dias.

RN04 — Unicidade de Lote: Cada movimentação de saída deve estar vinculada ao lote do produto para garantir rastreabilidade em caso de perda.

RN05 — Desconto Máximo: Atendentes podem aplicar descontos de até 5%. Descontos superiores exigem a liberação por senha do Gerente.

3. Requisitos Funcionais 
RF01 — Manter Cadastro de Produtos: O sistema deve permitir incluir, alterar e excluir produtos (Descrição, Preço, Fabricante).

RF02 — Consultar Estoque: O sistema deve exibir a quantidade disponível de um produto em tempo real por unidade.

RF03 — Registrar Venda: O sistema deve processar a venda de múltiplos itens e calcular o valor total.

RF04 — Cadastrar Cliente: O sistema deve permitir o registro rápido de clientes para histórico de compras.

RF05 — Validar Receita: O sistema deve disponibilizar campos para registro de dados de receitas médicas.

RF06 — Gerenciar Contas a Receber: O sistema deve permitir dar baixa em pagamentos de clientes recorrentes/conveniados.

RF07 — Alerta de Reposição: O sistema deve notificar quando o estoque atingir o nível mínimo configurado.

RF08 — Emitir Comprovante: O sistema deve gerar um resumo da venda para impressão ou envio digital.

4. Requisitos Não Funcionais 
RNF01 — Segurança: O sistema deve exigir autenticação (Login/Senha) para qualquer operação.

RNF02 — Performance: A consulta de preços e estoque não deve exceder 2 segundos de resposta.

RNF03 — Disponibilidade: O sistema deve operar em modo offline sincronizado para vendas em caso de queda de internet.

RNF04 — Integridade: Toda transação financeira deve seguir o padrão ACID para evitar corrupção de dados.

5. Casos de Uso
Diagrama Sugerido (Descrição Lógica):

Atores: Atendente, Farmacêutico, Gerente.

Casos de Uso: UC01 (Efetuar Venda), UC02 (Consultar Produto), UC03 (Identificar Cliente), UC04 (Validar Receita), UC05 (Registrar Conta a Receber), UC06 (Emitir Comprovante), UC07 (Ajustar Estoque), UC08 (Cadastrar Produto), UC09 (Aplicar Desconto Especial), UC10 (Efetuar Login).

6. Documentação dos Casos de Uso
UC01 — Efetuar Venda
Ator(es): Atendente.

Descrição: Registrar a saída de produtos e o recebimento de valores.

Pré-condições: Atendente autenticado; Produtos com estoque disponível.

Pós-condições: Estoque atualizado; Comprovante emitido.

Fluxo Principal:

Atendente inicia a venda.

Atendente consulta os produtos (UC02).

Atendente identifica o cliente (UC03).

Atendente confirma itens e quantidades.

Atendente seleciona forma de pagamento.

Sistema emite comprovante (UC06).

Fluxos Alternativos / Exceções:

FA01 — Item Controlado: Se o produto for controlado, executa-se a validação (UC04).

FA02 — Pagamento a Prazo: Se o pagamento for faturado, registra-se no financeiro (UC05).

Relacionamentos:

Incluir: UC02 (Consultar Produto), UC03 (Identificar Cliente), UC06 (Emitir Comprovante).

Estender: UC04 (Validar Receita), UC05 (Registrar Conta a Receber).

UC04 — Validar Receita
Ator(es): Farmacêutico.

Descrição: Validar os dados técnicos de uma receita para venda de controlados.

Fluxo Principal:

Farmacêutico confere a receita física.

Farmacêutico insere o CRM do médico e data da receita no sistema.

Farmacêutico autoriza a liberação do item na venda.

Relacionamentos: Estende UC01.

UC05 — Registrar Conta a Receber
Ator(es): Atendente.

Descrição: Criar um lançamento financeiro para cobrança futura.

Fluxo Principal:

Sistema verifica o limite de crédito do cliente.

Sistema registra a parcela com data de vencimento.

Status da conta é definido como "Aberta".

Relacionamentos: Estende UC01.


