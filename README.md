ï»¿> **Uso defensivo:** sêÂ³ teste aplicativos que sêÂ£o SEUS ou que vocêÂª tem permissêÂ£o escrita para testar, sempre numa cêÂ³pia de teste (staging/sandbox), nunca em produêÂ§êÂ£o com clientes. Este kit êÂ© para PROTEGER, nêÂ£o para invadir os outros.

# Invada seu prêÂ³prio app ê¢â¬â kit defensivo

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![Invada seu prêÂ³prio app](guia/assets/banner.jpg)](https://linnoff88-dev.github.io/arckhe-/guia/)

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## O que êÂ©

Invada seu prêÂ³prio app êÂ© um kit de revisêÂ£o defensiva com um verificador, cinco guias de brechas e prompts para organizar os resultados. êâ° para quem construiu um app com IA e consegue editar o projeto, mas nêÂ£o trabalha com seguranêÂ§a todos os dias. Ele ajuda a procurar sinais de falhas, corrigir as regras do app e conferir o resultado antes de publicar. Para usar, vocêÂª precisa de uma cêÂ³pia isolada do seu app, dados inventados, duas contas fictêÂ­cias e Python 3.

## ê°Å¸ââ Guia de uso

https://linnoff88-dev.github.io/arckhe-/guia/

Construiu um app com IA e quer conferir o que ficou exposto? Este kit ajuda a procurar sinais, corrigir decisêÂµes inseguras no servidor e repetir os testes antes de publicar. Foi escrito para quem consegue editar o app, mas nêÂ£o trabalha com seguranêÂ§a todos os dias.

## As cinco brechas

1. [Reset de senha](kit/brechas/01-reset-de-senha.md): um identificador vindo do navegador permite trocar a senha da conta errada.
2. [AvaliaêÂ§êÂµes e comentêÂ¡rios](kit/brechas/02-avaliacoes-e-comentarios.md): conteêÂºdo salvo êÂ© interpretado como cêÂ³digo no navegador de quem lêÂª.
3. [Chatbot do site](kit/brechas/03-chatbot-do-site.md): pedidos fora do negêÂ³cio consomem a sua cota de inferêÂªncia.
4. [Checkout e preêÂ§o](kit/brechas/04-checkout-e-preco.md): o servidor aceita o valor que o comprador enviou.
5. [E-mail e agente](kit/brechas/05-email-e-agente.md): o agente trata instruêÂ§êÂµes recebidas em uma mensagem como ordens do dono.

## Como usar

Siga [COMECE AQUI](kit/COMECE-AQUI.md). Prepare duas contas fictêÂ­cias e dados descartêÂ¡veis em staging. Execute:

```sh
python3 kit/scripts/checa.py --url https://staging.seu-app.test --eu-tenho-permissao
python3 kit/testes/run.py
```

O endereêÂ§o acima ilustra o formato: substitua pelo endereêÂ§o da sua cêÂ³pia de teste. A flag declara sua autorizaêÂ§êÂ£o e o uso de staging; o script nêÂ£o consegue verificar a propriedade ou o ambiente.

O verificador faz um êÂºnico GET, sem seguir redirecionamentos, sem login e sem enviar formulêÂ¡rios. Analisa somente o HTML e o JavaScript inline recebidos: nêÂ£o baixa scripts externos nem visita outras rotas. IndêÂ­cios nêÂ£o comprovam exploraêÂ§êÂ£o; ausêÂªncia de indêÂ­cios nêÂ£o comprova seguranêÂ§a. AutorizaêÂ§êÂ£o, valores no banco, consumo do chatbot e ferramentas do agente exigem conferêÂªncia manual.

Use os [prompts de teste simulado e relatêÂ³rio visual](kit/prompts/pentest-do-seu-app.md) para organizar a revisêÂ£o. Os [exemplos locais](kit/exemplos/) sêÂ£o demonstrativos e nêÂ£o têÂªm backend. O exemplo vulnerêÂ¡vel nêÂ£o executa scripts recebidos nem envia dados.

[EndereêÂ§o do guia](https://linnoff88-dev.github.io/arckhe-/guia/) ê¢â¬â referêÂªncia de publicaêÂ§êÂ£o; a pêÂ¡gina do guia nêÂ£o faz parte deste kit.

Python 3, sem dependêÂªncias adicionais. ConteêÂºdo autoral. LicenêÂ§a [MIT](LICENSE).

## VêÂ­deo

[Assista no YouTube](https://www.youtube.com/watch?v=UDAJ66IITq0) êÂ· [Short 9:16](https://youtube.com/shorts/FeB3cM4KULo) êÂ· [Player com legendas e capêÂ­tulos](https://linnoff88-dev.github.io/arckhe-/videos/)

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>