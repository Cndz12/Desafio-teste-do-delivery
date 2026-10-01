# Desafio-teste-do-delivery# Testes de Qualidade: Aplicativo de Delivery

**Atividade:** Desafio de testes de software
**Autor(a):** Vitor Hugo Xavier Afonso Dos Santos

---

## Desafio

Imagine que você está testando um aplicativo de delivery antes de ele ser lançado para os clientes. Quais testes você faria para verificar se o aplicativo está funcionando corretamente? Escolha três situações de teste, descreva o resultado esperado e explique por que esses testes são importantes para garantir a qualidade do sistema.

Escolhi três situações que cobrem o fluxo central do aplicativo: login, cálculo do valor e pagamento com confirmação do pedido.

## Resumo dos testes

| ID | Funcionalidade | Situação testada | Resultado esperado |
|----|----------------|------------------|--------------------|
| T1 | Cadastro e login | Credenciais válidas, senha errada e campos vazios ou inválidos | Acesso apenas com dados corretos e mensagens claras de erro |
| T2 | Cálculo do valor | Itens, quantidades, cupom de 10% e taxa de entrega | Total de R$ 62,25 e recálculo imediato a cada alteração |
| T3 | Pagamento e confirmação | Cartão aprovado, cartão recusado e queda de conexão | Pedido criado só com pagamento aprovado, sem cobrança duplicada |

---

## Teste 1: Login com credenciais válidas e inválidas

**Situação:** tentar entrar no aplicativo com e-mail e senha corretos, depois com senha errada, e depois com o campo de e-mail vazio ou com formato inválido (por exemplo, "joao@").

**Resultado esperado:**
- Com dados corretos, o usuário acessa a tela inicial com seus dados carregados.
- Com senha errada, o sistema bloqueia o acesso e mostra uma mensagem clara, sem revelar qual dos dois campos está incorreto.
- Com campos vazios ou inválidos, o sistema impede o envio e indica o que precisa ser corrigido.

**Por que é importante:** o login é a porta de entrada do sistema. Se falhar para quem tem conta, o cliente desiste do app. Se aceitar dados incorretos, expõe contas e dados pessoais, o que também é um problema de segurança e de conformidade com a LGPD.

## Teste 2: Cálculo do valor total do pedido

**Situação:** adicionar ao carrinho 2 unidades de um item de R$ 25,00 e 1 item de R$ 12,50, aplicar um cupom de 10% e somar a taxa de entrega de R$ 6,00. Depois, remover um item e alterar a quantidade.

**Resultado esperado:**
- Subtotal: R$ 62,50. Com 10% de desconto: R$ 56,25. Com a entrega: **R$ 62,25**.
- Ao remover ou alterar itens, o total é recalculado na hora, sem inconsistência entre carrinho e resumo do pedido.
- O valor é arredondado corretamente em duas casas decimais, e um cupom inválido ou expirado é recusado com aviso.

**Por que é importante:** erros de cálculo geram prejuízo direto para a empresa (cobrar a menos) ou perda de confiança do cliente (cobrar a mais). Como envolve regras de negócio combinadas (desconto, taxa, quantidade), é um ponto em que erros passam facilmente despercebidos.

## Teste 3: Pagamento e confirmação do pedido

**Situação:** finalizar um pedido com cartão válido, depois repetir com cartão recusado (saldo insuficiente) e com a conexão interrompida no meio do pagamento.

**Resultado esperado:**
- Pagamento aprovado: o cliente recebe a confirmação com número do pedido, itens, valor e previsão de entrega, e o restaurante recebe o pedido.
- Pagamento recusado: o pedido não é criado, o cliente é informado do motivo e pode tentar outra forma de pagamento sem perder o carrinho.
- Falha de conexão: não ocorre cobrança duplicada nem pedido "fantasma", e o status final fica consistente (pedido concluído ou não criado).

**Por que é importante:** envolve dinheiro e a promessa feita ao cliente. Cobrança sem pedido, pedido sem pagamento ou cobrança em duplicidade geram reclamações, estornos e danos à reputação. Testar também os cenários de falha é essencial, porque é neles que os sistemas costumam quebrar.

---

## Conclusão

Os três testes seguem a lógica de verificar tanto o caminho feliz (tudo certo) quanto os cenários de erro. Juntos, protegem a segurança do usuário, a correção financeira e a experiência de compra, que são os pilares da qualidade em um app de delivery.
