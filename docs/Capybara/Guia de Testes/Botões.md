---
sidebar_position: 3
---

Os botões são uma das principais formas de interação com páginas WEB. São responsáveis por submeter formulários, abrir pop up e modais, redirecionar para outras páginas, entre outras coisas. Essa seção irá lhe ensinar como interagir com os botões mais comuns.

## *click_button*

Utilize o arquivo **botao_test** para adicionar os seus testes.

Navegue até a página **Botões** e clique em cada botão para entender o que eles fazem. Depois volte a este tutorial para testar cada um deles.

Estes testes serão feitos com todos os botões, da esquerda para a direita.

### Botão "Exibir Flash de Sucesso"

Comece com um teste que verifica se a mensagem foi mostrada na tela:

```
test "testar botão com mensagem de sucesso em flash" do
  visit botoes_path
  click_button "botaoflashsucesso"
  assert_text "Sucesso!"
end
```

* Este teste começará visitando a página de **Botões** utilizando o método ***visit***, que você já conhece;

* Após, ele chamará o método ***click_button***. Este método procura por um botão na página e clica nele. Neste caso estamos procurando pelo botão utilizando seu ID **botaoflashsucesso**;

* Por fim, um novo método, o ***assert_text***. Este método procura por um texto EXATO, ou seja, ele diferenciará maiúsculas de minúsculas e irá comparar também os símbolos. O texto que procuramos é **"Sucesso!"**, que é exibido na forma de uma mensagem *flash*;

* Como o texto foi encontrado, o teste é finalizado sem erros e com 1 assertion.

:::info flash e assert_text
Para mais informações sobre ***assert_text***, consulte (TO DO).

As mensagens flash são uma maneira conveniente de exibir mensagens temporárias entre as requisições na sua aplicação Rails. Elas são armazenadas em uma sessão de cookie especial, que é apagada depois da próxima requisição. Caso não esteja familiarizado com o conceito, consulte a [documentação sobre flash](https://api.rubyonrails.org/classes/ActionDispatch/Flash.html) para aprender o que são e como criar suas próprias mensagens *flash* personalizadas.
:::

Como você pôde perceber, ao testar botões é necessário checar o estado da página após clicar no botão. Por isso, a verificação se mensagem foi exibida ocorre somente depois de clicar nele. É possível fazer um teste para verificar se a mensagem não é exibida antes, para garantir que não há mensagens sendo exibidas de forma displicente na página, mas isso vai da necessidade da aplicação que você está testando.

Há um pequeno problema com esse teste que foi comentado no tópico [escrevendo bons testes](/docs/Capybara/Escrevendo%20bons%20testes). Antes de prosseguir, você consegue identificar qual é? Pense um pouco ou mesmo retorne para a seção para tentar descrobrir...

.

.

.

.

.

.

.

**Conseguiu descobrir ?**

.

.

.

.

.

.

Existe uma diretriz que nos pede para [evitar testes frágeis](/docs/Capybara/Escrevendo%20bons%20testes#evite-testes-fr%C3%A1geis). Pense na seguinte hipótese: ao invés de escrever "Sucesso!" a página agora irá começar a exibir uma mensagem mais clara para o usuário, como "O botão de sucesso está funcionando!". Diante dessa hipótese o teste irá falhar, mesmo que a aplicação ainda esteja funcionando corretamente.

Pensa da seguinte forma: neste caso, o objetivo ao clicar no botão não é exibir uma mensagem escrito "X" ou "Y", mas sim exibir alguma mensagem de sucesso, seja ela qual for, para que termos certeza de que a solicitação foi atendida de forma correta.

Acompanhe o próximo exemplo para entender como lidar com este problema.

### Botão "Exibir Flash de Erro"

Adicione um novo teste dentro de sua classe de testes de botão

```
test "testar botão com mensagem de erro em flash" do
  visit botoes_path
  click_button "botaoflasherro"
  assert_selector('.alert.alert-danger')
end
```
Esse teste se assemelha muito ao anterior, a única diferença importante é quanto ao método ***assert_selector***. Este método procura se há algum elemento que possui os parâmetros passados. Então ao invés de verificar a mensagem exata de erro, nós verificamos se há algum elemento com as classes *alert* e *alert-danger* passadas como parâmetro.

Três pontos importantes merecem nossa atenção aqui:

* Primeiro, o uso de uma classe em vez de um ID para localizar um elemento na página. Este tutorial já destacou a importância de usar IDs para individualizar os elementos HTML, então, por que agora sugerimos o uso de uma classe? Isso se deve à maneira como as mensagens flash são geradas no Rails. É raro que cada mensagem flash tenha um ID personalizado. Mesmo que os IDs sejam gerados, provavelmente seriam feitos de maneira dinâmica e aleatória, que é como os desenvolvedores Rails geralmente criam mensagens flash. Dado esse cenário, é mais apropriado procurar a presença da classe do alerta na tela, pois isso indica que alguma mensagem está sendo exibida. Além disso, se é uma "alert-danger", podemos inferir que é uma mensagem de erro.

* Em segundo lugar, a questão de determinar qual tipo de alerta é exibido para cada mensagem. O Rails oferece algumas convenções, como criar mensagens flash com :notice para sucesso ou :alert para erros. No entanto, nesta aplicação usamos :success e :danger para estilização com Bootstrap, uma abordagem comum para desenvolvedores que usam Rails com Bootstrap. Então, como saber qual das duas abordagens usar? Isso depende muito da arquitetura do software e das decisões do time de desenvolvimento. É essencial que o time defina uma regra para ser seguida por todos, a fim de facilitar a leitura e manutenção do código, bem como a criação de testes. Portanto, antes de escolher qual abordagem usar, você precisa entender como a aplicação está sendo construída.

* Por último, até agora você  utilizou aspas simples ou aspas duplas e colocou o parâmetro entre elas, e assim o próprio Capybara inferiu se tratava-se de um ID, uma classe, um placeholder, ou algum outro atributo do elemento HTML. Desta vez, além das aspas utilizamos o ponto (**.**). Isto diz ao Capybara que estamos procurando por uma classe. Ao invés de permitir que ele procure entre todos os atributos o ponto o força a procurar por uma classe com o nome. Como colocamos uma classe atrás da outra ligada por dois pontos estamos dizendo que é necessário que estas classes estejam nessa ordem no mesmo elemento HTML. 

:::danger Cuidado!
Alguns métodos do Capybara não são capazes de inferir o tipo de atributo do elemento procurado! Por exemplo, o método find_field consegue identificar o tipo de campo independentemente de como você passa o argumento. No entanto, para o método assert_selector e outros semelhantes, é necessário passar um seletor que identifique explicitamente o atributo que estamos procurando. Por exemplo, .alert para uma classe ou #myID para um ID. Certifique-se de sempre verificar a documentação e entender como os métodos que você está utilizando lidam com argumentos.
:::