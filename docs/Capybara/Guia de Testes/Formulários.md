---
sidebar_position: 6
---

Formulários podem se tornar confusos ao criar testes de interface. Antes de pensar em quais testes realizar para sua página de formulário é preciso entender o objetivo daquele formulário, seus campos e no resultado gerado ao enviar o formulário de maneira correta.

Como já foi dito: o capybara simula o comportamento do usuário, então ao criar os testes para formulários é necessário entender do ponto de vista do usuário interagindo com aquilo e por qual motivo ele iria preenchê-lo. 

É claro que testes podem apenas focar no comportamento esperado. Por se tratar de uma ferramenta de BDD, muitas vezes não será necessário pensar no comportamento esperado com Capybara, pois outro time (em geral ligado ao produto) irá pensar quais serão os testes necessários para cada cenário, o desenvolvedor precisará apenas os escrever. No entanto, como vimos nas diretrizes para [escrever bons testes](/docs/Capybara/Escrevendo%20bons%20testes), entender a aplicação é uma tarefa essencial para que você não escreva testes inúteis, para não deixar de escrever testes essenciais e muitas vezes também possibilita a reestruturação do código, pois você percebe que algo escrito não faz sentido do ponto de vista do cliente.


## Indo além do especificado

Pense na seguinte situação: você está desenvolvendo uma *feature* em uma API que realiza um calcula de orçamentos fazendo uma busca por preços mais baixos na região, mas para isso ela precisa realizar requisições para outras APIS. Ao descrever como o produto se comporta o time de produtos descreve um cenário que ao preencher todos os valores de forma correta os valores são exibidos com uma mensagem de sucesso. Ao fazer uma requisição, no entanto, a tela demora alguns segundos para responder antes de mostrar a mensagem de sucesso. Isso pode levar a dois problemas: 

* O primeiro implica na experiência do usuário. Talvez não seja possível diminuir o tempo de requisição, então o ideal é que durante a espera uma mensagem seja mostrada até que a resposta esteja disponível. Lembre-se: o time de produto nem sempre sabe qual o fluxo da aplicação, e não é comum que ele saibam sobre o tempo de resposta de uma requisição, então esse cenário pode não ter sido previsto. Colocar algum tipo de aviso durante esse tempo melhora a experiência do usuário.

* O segundo decorre do problema gerado pelo primeiro: já que a requisição demora um tempo apra ser processada, se o usuário não vir uma mensagem ele pode acabar clicando diversas vezes no botão e fazer muitas requisições seguidas, sobrecarregando o servidor de maneira desnecessária. Mais uma vez: o time de produto pode não pensar neste cenário, pois se trata de algo que decorre em razão de como a aplicação foi desenvolvida, então cabe a um desenvolvedor atento olhar para este cenário e pensar em formas de contornar o problema, como desabilitar o botão enquanto a requisição está sendo processada, e só ativá-lo após a resposta.

Essas implementações não devem ser feitas à revelia do setor de produto, mas sim integrando-o para que seja possível atualizar as especificações e manter tudo bem documentado, além de ajudá-los a identificar pontos de melhoria. Toda mudança no projeto sempre deve ser realizada comunicando as partes envolvidas.

:::tip Dica
Busque se tornar um desenvolvedor que consegue construir uma aplicação indo além de apenas escrever as instruções dadas, mas sugerindo mudanças críticas, reestruturando partes inúteis ou obsoletas e entendendo como aperfeiçoar o produto em que está trabalhando.
:::

## Interagindo com um formulário

É possível interagir com formulários utilizando muitos dos elementos mostrados anteriormente. Formulários podem conter *checkboxes*, botões, *links*, entre outros elementos menos comuns. Além disso, formulários em geral possuem um campo para preencher informações que serão processadas, como um nome. A forma mais comum de interagir com estes campos com Capybara é utilizando o método ***fill_in***. 

Dentro arquivo **formulario1_test.rb** adicione o próximo teste:

```
  test "preencher o formulário 1 com informações corretas" do
    visit "/formulario1/new"
    fill_in "formulario1_first_name", with: "José"
    fill_in "formulario1_last_name", with: "Silva"
    fill_in "formulario1_email", with: "josesilva@meuemail.com"
    fill_in "formulario1_address", with: "Rua dos bobos, nº 0"
    fill_in "formulario1_phone", with: "1199999999"
    click_button "enviar"
    assert_selector (".alert.alert-success")
  end
```

A estrutura do teste se assemelha muito ao que foi feito até agora: visitar uma página, realizar as ações necessárias e ao fim verificar um elemento para garantir que ele está presente na tela. A única mudança relevante foi com o método ***fill_in***. Aqui dois parâmetros foram passados: o primeiro é o identificador do campo que será preenchido; neste caso utilizamos os IDs únicos gerados automaticamente pelo rails. O segundo parâmetro é um hash, com a palavra *with* seguido do valor que queremos colocar dentro do campo. Basicamente estamos dizendo: preencha o campo "X" com o valor "Y".

## Formulário com informações erradas

Para além do [caminho feliz](/docs/Capybara/Escrevendo%20bons%20testes#saia-do-caminho-feliz), os formulários precisam sempre verificar se os campos foram preenchidos com valores válidos. Validações de informações são essenciais para prevenir que coloquemos dados falsos ou inválidos e também comportamentos maliciosos, como ataques ao banco de dados. Todavia, o usuário comum não sabe porquê ou como essas validações ocorrem (e de fato ele nem se importa com isso); para o usuário é necessário apenas entender o que ele deve fazer quando um erro ocorrer. Diante deste cenário mensagens que avisem que os dados não foram enviados, e também o motivo, são essenciais. 

No formulário falso que criamos para testar há alguns requisitos:

* Endereço não pode estar em branco;
* Nome e o sobrenome devem ter ao menos 3 caracteres;
* E-mail deve seguir o padrão da constante *URI::MailTo::EMAIL_REGEXP*;
* Telefone deve conter 10 ou 11 números.

:::info URI::MailTo::EMAIL_REGEXP
É uma constante de um regex comumente usando em rails para validar e-mails. Embora não aborde todos os casos possíveis de e-mails (como e-mails que possuem aspas), ela é suficiente para a maior parte dos casos. Para mais informações consulte a documentação da [RFC](https://datatracker.ietf.org/doc/html/rfc5321#section-2.3.5) e a documentação da [biblioteca URI](https://ruby-doc.org/stdlib-3.0.1/libdoc/uri/rdoc/URI/MailTo.html)
:::

O teste abaixo preenche os campos email, telefone e endereço, mas deixa em branco os campos nome e sobrenome. Em seguida verifica se há duas mensagens de erro (já que dois campos estão errados):

```
test "preencher o formulário 1 com nome e sobrenome em branco" do
  visit "/formulario1/new"
  fill_in "formulario1_email", with: "josesilva@meuemail.com"
  fill_in "formulario1_address", with: "Rua dos bobos, nº 0"
  fill_in "formulario1_phone", with: "1199999999"
  click_button "enviar"
  erros = all(".alert.alert-danger").count
  assert_equal 2, erros
end
```

## Evite a Armadilha dos Testes Excessivos

Embora possa parecer contraintuitivo à primeira vista, nem sempre é vantajoso escrever um teste para cada possível cenário. Considere o caso de um formulário com cinco campos: os possíveis cenários de teste - como ter apenas o campo de nome em branco com todos os outros campos preenchidos corretamente, ou ter apenas um caractere no nome, dois caracteres no nome e assim por diante - passam à casa dos 120 testes (5 fatorial). Agora, imagine a explosão de complexidade para um formulário mais robusto com 10 campos - estamos falando de mais de 3 milhões de possíveis testes!

Na prática, muitos desses testes podem ser irrelevantes. Apesar de cobrirem todas as possíveis variantes, o ganho pode ser muito pequeno comparado ao esforço de escrita e manutenção desses testes. Lembre-se que os testes de UI são computacionalmente custosos e podem acabar drenando recursos que seriam melhor empregados em outros lugares.

Portanto, ao projetar testes para formulários, é essencial ponderar o valor real de cada teste. Pergunte-se: Qual é a importância de testar o campo "X" ou "Y"? É fundamental garantir que um campo de e-mail rejeite entradas inválidas, como "@@@.com", e que o campo de telefone aceite apenas números. No entanto, pode ser menos relevante verificar a ordem em que as mensagens são exibidas, ou verificar se um campo aceita zero ou uma letra após confirmar que ele não aceita menos que três.

Testes são vitais, mas devemos evitá-los quando são muito extensos, cobrindo cenários de falha de baixo impacto na experiência do usuário ou presumivelmente impossíveis de ocorrer. A economia de tempo e recursos pode ser direcionada para melhorar outras partes do seu projeto.