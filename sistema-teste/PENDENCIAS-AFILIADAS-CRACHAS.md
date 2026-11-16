# ItaEnergyFit — Pendências de Afiliadas, Crachás e Comissões
Atualizado em 2026-11-15. Documento de planejamento; não indica que as funcionalidades abaixo já foram implementadas.

## Confirmado em testes
- Aba Crachás carrega afiliada real ELIANA (cupom ELIANA01) do Firebase.
- Existem 10 espaços; vagas não cadastradas não apresentam nomes ou vendas fictícios.
- Botões Ver frente / Ver verso funcionam.
- Foto da afiliada foi salva e aparece no crachá.
- QR Code individual abre a loja ItaEnergyFit.
- Abertura da loja por QR ainda não comprova atribuição da indicação ao pedido.

## Correções a implementar
1. **Comissão padrão configurável:** campo de porcentagem nas Configurações, sem fixar 10% no código.
2. **Comissão individual configurável:** campo Comissão (%) por afiliada na aba Afiliadas; validar valores de 0% a 100% e definir se a taxa individual substitui a padrão.
3. **Cálculo e persistência:** ao confirmar pagamento real, registrar no pedido afiliada/cupom, base de cálculo, porcentagem aplicada e valor da comissão. Mudanças posteriores na taxa não recalculam pedidos anteriores.
4. **Atribuição via QR:** capturar ?ref=ELIANA01 na loja, validar o cupom no Firebase, preservar referência durante navegação e checkout, e gravar no pedido. Mensagem opcional “Você está comprando por indicação de ELIANA”.
5. **Mercado Pago:** implementar/validar checkout e webhook com verificação de autenticidade, idempotência e confirmação do pagamento antes de lançar comissão. Não atribuir comissão só por abrir QR ou iniciar pedido.
6. **Painel de comissões:** exibir pedidos, vendas pagas, porcentagem usada, comissões estimadas/devidas e estados de liquidação.
7. **Botão Pedidos da aba Afiliadas:** mostrar lista ou mensagem “Nenhum pedido encontrado para esta afiliada”, e erros de permissão/conexão.
8. **Crachás:** testar gravação e exibição de Instagram/WhatsApp, impressão e download, e conferir QR após eventual edição do cupom.
9. **Base de cálculo:** decidir formalmente tratamento de descontos, frete, cancelamentos, estornos e devoluções antes de lançar comissões definitivas.

## Método de trabalho
- Desenvolver e testar apenas na pasta sistema-teste; preservar sistema/ e index.html oficial até aprovação.
- Revisar regras de segurança do Firebase ao final das abas.
- Não expor segredos ou credenciais no front-end.

## Decisão sobre navegação — aba Frete substitui Vendedores
- A aba **Vendedores** será removida do menu de teste, pois a gestão de indicações e comissões ficará concentrada em **Afiliadas**.
- No mesmo lugar do menu, criar a aba **Frete**, com duas áreas:
  1. **SuperFrete:** integração de cotação e acompanhamento de fretes nacionais; reutilizar a configuração/Worker de frete existente, sem expor token no navegador.
  2. **Entregas locais:** cadastrar motoboys (nome, telefone, taxa, ativo/inativo), bairros/áreas atendidos e valores de entrega no município da loja.
- Prever configurações de frete grátis e regras para seleção entre entrega local e transportadora, sujeitas a testes.
- **Status: decisão registrada, implementação ainda pendente.** Não alterar o sistema oficial nem a loja nesta fase. Aplicar primeiro em sistema-teste, validar e depois revisar regras Firebase em conjunto.

## Decisão adicional — duas abas no sistema
- O usuário confirmou que quer **Frete** e **Loja** como abas distintas no sistema integrado.
- **Frete** substitui a antiga aba **Vendedores**.
- **Loja** é uma nova aba de administração/acesso à loja online, sem substituir **Configurações** ou **Atendimento ITA**.
- Escopo inicial sugerido para Loja: link/visualização da loja publicada, acesso à vitrine e atalhos para Produtos e Configurações; validar funcionalidades específicas com o usuário antes de implementar.
- **Status: decisão registrada, implementação pendente.** Manter tudo em sistema-teste até validação.
