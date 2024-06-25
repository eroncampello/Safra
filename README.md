Para enviar a mensagem "InformGiveUpPendingApproval" (bvmf.019.02, MsgType=n), é necessário seguir um fluxo específico com a preparação e envio de mensagens anteriores. Aqui está uma visão geral das mensagens envolvidas e a estrutura necessária para enviar a mensagem final.

### 1. NewOrderSingle (MsgType=D)

Esta mensagem é utilizada para iniciar o processo de ordem. Aqui está um exemplo:

```
8=FIX.4.4|9=200|35=D|34=1|49=YOUR_SENDER_COMP_ID|52=20240621-18:29:07.632|56=ICVM35|11=BV000343202406210000000000000000001|21=1|38=100|40=2|44=22.29|54=1|59=0|10=220|
```

### 2. ExecutionReport (MsgType=8)

Após o envio de uma nova ordem, um relatório de execução é gerado para confirmar a ordem. Aqui está um exemplo de mensagem de relatório de execução:

```
8=FIX.4.4|9=300|35=8|34=2|49=ICVM35|52=20240621-18:30:07.632|56=YOUR_SENDER_COMP_ID|37=ORDERID123|11=BV000343202406210000000000000000001|17=EXECDID123|150=0|39=0|55=SYM|54=1|38=100|44=22.29|32=100|31=22.29|6=22.29|14=100|151=0|60=20240621-18:29:07.632|10=123|
```

### 3. GiveUpInformation (MsgType=U8 - exemplo ilustrativo, verificar a tag correta no contexto)

Esta mensagem seria enviada para informar os detalhes do "Give-Up". Aqui está um exemplo de como poderia ser formatada:

```
8=FIX.4.4|9=250|35=U8|34=3|49=YOUR_SENDER_COMP_ID|52=20240621-18:35:07.632|56=ICVM35|128=ICVM35|11=BV000343202406210000000000000000001|60=20240621-18:35:07.632|20001=BV000343202406210000000000000000001bvmf.019.022024-06-17T16:55:20.0Z|10=200|
```

### 4. InformGiveUpPendingApproval (MsgType=n)

Finalmente, enviamos a mensagem "InformGiveUpPendingApproval" com o tipo de mensagem `n`.

```
8=FIX.4.4|9=2314|35=n|34=9|49=ICVM35TAR|52=20240621-18:29:07.632|56=ICVM35|128=ICVM35|11=BV000343202406210000000000000000001|60=20240621-18:29:07.632|447=D|448=000999|452=7|453=1|9225=bvmf.019.02|20001=BV000343202406210000000000000000001bvmf.019.022024-06-17T16:55:20.0ZBVMF39403-5939403-11440395201503-594039999951002000014512268BVMFBRMULTACNOR5MULT3138110146490SELL1MESPC178411993723870DHJ002024-06-17T13:55:20.02822.29|20002=2117|10=<CheckSum>|
```

### Estrutura da Mensagem bvmf.019.02

A mensagem `bvmf.019.02` inclui vários campos essenciais, como identificadores de parte, detalhes de transação, e campos específicos de identificação proprietária.

#### Campos Específicos da Mensagem bvmf.019.02:

- **MsgType (35=n)**: Define o tipo de mensagem como "InformGiveUpPendingApproval".
- **ClOrdID (11)**: Identificador único da ordem.
- **TransactTime (60)**: Hora da transação.
- **NoPartyIDs (453)**: Grupo de partes envolvidas na transação.
- **PartyID (448)** e **PartyRole (452)**: Identificação e papel das partes.
- **ProprietaryInformation (20001)** e **InformationType (9225)**: Informações proprietárias e tipo de informação.

### Tipos de Mensagens FIX

O padrão FIX define vários tipos de mensagens que são usadas para diferentes propósitos, incluindo:

- **D (New Order - Single)**: Para enviar novas ordens.
- **8 (Execution Report)**: Para relatar execuções de ordens.
- **U8 (Give Up)**: Para informar detalhes de "give-up".
- **n (Inform GiveUpPendingApproval)**: Para informar a aprovação pendente de "give-up".

Este é um resumo dos passos e exemplos de mensagens necessárias para enviar a mensagem `bvmf.019.02`. Certifique-se de adaptar os campos e valores conforme necessário para o seu ambiente específico.
