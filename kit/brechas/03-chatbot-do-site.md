> **Uso defensivo:** só teste aplicativos que sêo SEUS ou que você tem permissêo escrita para testar, sempre numa cópia de teste (staging/sandbox), nunca em produçêo com clientes. Este kit é para PROTEGER, nêo para invadir os outros.

# Chatbot do site

## O que é

O chatbot usa sua cota para responder às mensagens dos visitantes.
Sem controle de assunto e consumo, ele pode virar um assistente particular de terceiros.
Uma instruçêo no pedido pode tentar desviar a conversa das tarefas do seu negócio.
Um prompt de sistema ajuda, mas nêo é uma barreira suficiente nem uma garantia de isolamento.

## Como saber se o seu app tem

1. Defina por escrito o que o chatbot deve atender e selecione três perguntas legítimas.
2. Em staging, envie uma pergunta fora do negócio, como pedir uma história sobre um planeta imaginário. Faça só poucas tentativas, dentro da cota de teste.
3. Confira se há recusa curta e se a pergunta foi barrada antes da geraçêo principal. Veja consumo e decisêo no registro de teste, sem guardar dados sensíveis.
4. Revise se os limites sêo aplicados no servidor, incluindo visitantes anônimos e chamadas diretas à rota. Nêo faça teste de carga.

## Como corrigir

Classifique pertinência antes da resposta principal, com saída estruturada `sim/nêo` e confiança validada. O classificador também pode errar ou sofrer manipulaçêo; avalie-o com casos locais e aplique limites independentes do modelo. Confiança declarada nêo é uma probabilidade calibrada. O limiar abaixo é uma decisêo inicial a validar.

```text
responder(sessao, mensagem):
    exigir tamanho(mensagem) <= 2000
    reservar_cota_atomica(sessao, origem, orcamento_global)
    decisao = classificar_assunto(
        politica_fixa_do_negocio,
        dados_nao_confiaveis=mensagem,
        limite_de_saida=80)
    se formato_invalido(decisao) ou decisao.assunto != "sim"
       ou decisao.confianca < 0.9:
        retornar "Posso ajudar apenas com assuntos deste serviço."
    resposta = gerar(
        sistema=politica_fixa_sem_segredos,
        mensagem_como_dado=mensagem,
        ferramentas=nenhuma,
        limite_de_saida=300)
    contabilizar_custo_real_incluindo_classificador()
    retornar resposta
```

Nêo permita ao cliente editar a política. Separe instruções de dados, limite tamanho e tempo, imponha cotas por sessêo/conta/origem e teto global. Falha do classificador deve recusar com segurança. Caso ferramentas sejam necessárias, autorize cada açêo no servidor.

## Como confirmar que corrigiu

- Perguntas legítimas recebem respostas úteis; perguntas externas recebem recusa curta.
- Saída inválida, confiança baixa ou indisponibilidade do classificador nêo acionam a geraçêo principal.
- Uma cota de teste pequena bloqueia o próximo pedido no limite, inclusive com chamadas concorrentes.
- A mediçêo inclui classificaçêo, geraçêo e tentativas recusadas; nenhuma regra depende apenas do prompt.
