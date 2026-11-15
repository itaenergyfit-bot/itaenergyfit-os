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
