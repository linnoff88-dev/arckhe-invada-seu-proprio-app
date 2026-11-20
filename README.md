> **Uso defensivo:** sÃ³ teste aplicativos que sÃ£o SEUS ou que vocÃª tem permissÃ£o escrita para testar, sempre numa cÃ³pia de teste (staging/sandbox), nunca em produÃ§Ã£o com clientes. Este kit Ã© para PROTEGER, nÃ£o para invadir os outros.

# Invada seu prÃ³prio app â€” kit defensivo

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![Invada seu prÃ³prio app](guia/assets/banner.jpg)](https://inematds.github.io/invada-seu-proprio-app/guia/)

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

Invada seu prÃ³prio app Ã© um kit de revisÃ£o defensiva com um verificador, cinco guias de brechas e prompts para organizar os resultados. Ã‰ para quem construiu um app com IA e consegue editar o projeto, mas nÃ£o trabalha com seguranÃ§a todos os dias. Ele ajuda a procurar sinais de falhas, corrigir as regras do app e conferir o resultado antes de publicar. Para usar, vocÃª precisa de uma cÃ³pia isolada do seu app, dados inventados, duas contas fictÃ­cias e Python 3.

## ðŸ“– Guia de uso

https://inematds.github.io/invada-seu-proprio-app/guia/

Construiu um app com IA e quer conferir o que ficou exposto? Este kit ajuda a procurar sinais, corrigir decisÃµes inseguras no servidor e repetir os testes antes de publicar. Foi escrito para quem consegue editar o app, mas nÃ£o trabalha com seguranÃ§a todos os dias.

## As cinco brechas

1. [Reset de senha](kit/brechas/01-reset-de-senha.md): um identificador vindo do navegador permite trocar a senha da conta errada.
2. [AvaliaÃ§Ãµes e comentÃ¡rios](kit/brechas/02-avaliacoes-e-comentarios.md): conteÃºdo salvo Ã© interpretado como cÃ³digo no navegador de quem lÃª.
3. [Chatbot do site](kit/brechas/03-chatbot-do-site.md): pedidos fora do negÃ³cio consomem a sua cota de inferÃªncia.
4. [Checkout e preÃ§o](kit/brechas/04-checkout-e-preco.md): o servidor aceita o valor que o comprador enviou.
5. [E-mail e agente](kit/brechas/05-email-e-agente.md): o agente trata instruÃ§Ãµes recebidas em uma mensagem como ordens do dono.

## Como usar

Siga [COMECE AQUI](kit/COMECE-AQUI.md). Prepare duas contas fictÃ­cias e dados descartÃ¡veis em staging. Execute:

```sh
python3 kit/scripts/checa.py --url https://staging.seu-app.test --eu-tenho-permissao
python3 kit/testes/run.py
```

O endereÃ§o acima ilustra o formato: substitua pelo endereÃ§o da sua cÃ³pia de teste. A flag declara sua autorizaÃ§Ã£o e o uso de staging; o script nÃ£o consegue verificar a propriedade ou o ambiente.

O verificador faz um Ãºnico GET, sem seguir redirecionamentos, sem login e sem enviar formulÃ¡rios. Analisa somente o HTML e o JavaScript inline recebidos: nÃ£o baixa scripts externos nem visita outras rotas. IndÃ­cios nÃ£o comprovam exploraÃ§Ã£o; ausÃªncia de indÃ­cios nÃ£o comprova seguranÃ§a. AutorizaÃ§Ã£o, valores no banco, consumo do chatbot e ferramentas do agente exigem conferÃªncia manual.

Use os [prompts de teste simulado e relatÃ³rio visual](kit/prompts/pentest-do-seu-app.md) para organizar a revisÃ£o. Os [exemplos locais](kit/exemplos/) sÃ£o demonstrativos e nÃ£o tÃªm backend. O exemplo vulnerÃ¡vel nÃ£o executa scripts recebidos nem envia dados.

[EndereÃ§o do guia](https://inematds.github.io/invada-seu-proprio-app/guia/) â€” referÃªncia de publicaÃ§Ã£o; a pÃ¡gina do guia nÃ£o faz parte deste kit.

Python 3, sem dependÃªncias adicionais. ConteÃºdo autoral. LicenÃ§a [MIT](LICENSE).

## VÃ­deo

[Assista no YouTube](https://www.youtube.com/watch?v=UDAJ66IITq0) Â· [Short 9:16](https://youtube.com/shorts/FeB3cM4KULo) Â· [Player com legendas e capÃ­tulos](https://inematds.github.io/invada-seu-proprio-app/videos/)

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>