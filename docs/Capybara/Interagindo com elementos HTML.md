---
sidebar_position: 5
---

Os testes automatizados, especialmente os testes de interface do usuário, envolvem interações com elementos da página, como links, botões, formulários e outros. No Capybara, existem muitas maneiras de interagir com esses elementos. Vamos explorar como você pode identificar, selecionar e interagir com os elementos HTML em suas páginas web.

### Identificando Elementos HTML

Para poder interagir com um elemento HTML, é necessário localizá-lo. Para localizar elementos na página, o Capybara fornece uma série de métodos, que permitem selecionar elementos por suas tags, texto, valor, ID, classe CSS e muito mais.

Antes de aprofundar mais neste tópico, é necessário fazer uma pequena recapitulação: **a boa prática recomenda que elementos HTML tenham ID's únicos para facilitar sua identificação e manipulação**. O mesmo não ocorre com outros seus atributos. Diante disto, é uma boa prática que se utilize o ID ao identificá-los. Isto se dá principalmente pela forma como o Capybara lida ao encontrar mais de um elemento com o mesmo parâmetro de identificação.

Inclua o exemplo abaixo dentro do seu arquivo de teste **teste_spec.rb** dentro do escopo do * **describe** *:



