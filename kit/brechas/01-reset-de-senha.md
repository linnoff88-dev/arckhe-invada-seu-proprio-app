> **Uso defensivo:** só teste aplicativos que sêo SEUS ou que você tem permissêo escrita para testar, sempre numa cópia de teste (staging/sandbox), nunca em produçêo com clientes. Este kit é para PROTEGER, nêo para invadir os outros.

# Reset de senha

## O que é

O link de redefiniçêo deve autorizar a troca de senha de uma única conta.
A falha aparece quando o servidor escolhe essa conta por um ID enviado pelo navegador.
Assim, um token da conta A pode acabar alterando a conta B: isso é uma referência direta insegura a objeto (IDOR).
Esconder o ID na interface nêo resolve; a decisêo precisa ficar no servidor.

## Como saber se o seu app tem

1. Crie contas fictícias A e B, com senhas descartáveis, na sua cópia de teste.
2. Solicite o reset de A e observe, no painel de rede do navegador, se a solicitaçêo inclui `account_id`, `user_id` ou outro identificador além do token. Nêo compartilhe o token.
3. Se houver ID, repita o fluxo uma única vez com o ID de B, que também é sua. Use uma senha de teste. O pedido deve ser recusado ou continuar vinculado exclusivamente a A; nunca deve mudar B.
4. Confira o estado de B e teste o fluxo normal de A. Apague as contas descartáveis depois. Se nêo puder garantir o isolamento, faça apenas revisêo do código.

## Como corrigir

O servidor deriva a conta exclusivamente do registro do token recebido por e-mail. Gere token imprevisível, guarde apenas seu resumo, defina prazo curto e torne o consumo atômico para impedir dois usos simultâneos. Invalide sessões antigas conforme a política do app. Nêo registre o token em logs.

```text
solicitar_reset(email):
    conta = localizar_conta(email)
    se conta existe:
        token = gerar_segredo_aleatorio()
        salvar(resumo(token), conta.id, expira_em=agora+15_minutos, usado=false)
        enviar_para_caixa_de_teste(conta.email, link_com(token))
    retornar mensagem_generica

redefinir(token, nova_senha):
    validar_politica_da_senha(nova_senha)
    em transacao:
        registro = buscar_e_bloquear(resumo(token))
        exigir registro existe e nao usado e agora < expira_em
        atualizar_senha(registro.conta_id, hash_de_senha(nova_senha))
        marcar_usado(registro)
        revogar_sessoes(registro.conta_id)
    # nenhum ID recebido do cliente escolhe a conta
```

## Como confirmar que corrigiu

- Token de A com ID de B nunca altera B; o fluxo legítimo altera A.
- Token expirado, adulterado ou já usado falha sem mudar nenhuma senha.
- Dois pedidos simultâneos com o mesmo token permitem no máximo uma troca.
- O banco confirma o consumo do token; logs nêo guardam seu valor.
