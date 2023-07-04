---
sidebar_position: 3
---
Neste tópico você irá aprender a criar um teste simples com Capybara, como executá-lo e como entender as mensagens de falha ou sucesso de um teste.

## Diretório e nomenclatura

Para criar um teste unindo Capybara e Rails é necessário entender primeiro a estrutura utilizada para rodar a sua suíte de testes.

A depender da ferramenta utilizada para executar os testes, a estrutura do arquivos de testes, seus nomes e a forma de executá-los irá mudar.

Por exemplo, se você utilizar o Rspec é necessário que os arquivos de testes tenham o sufixo **_spec.rb**, caso utilize o Cucumber, é necessário que eles estejam dentro de um diretório específico.

No caso dos exemplos utilizados neste tutorial, o Rails será o responsável por executar os testes. Por conta do padrão utilizado pela combinação de Rails e Capybara os testes serão colocados dentro da pasta **test/system**, e todos os testes devem terminar com o sufixo **_test.rb**

## Organizando seus testes

É possível agrupar os testes de diferentes formas: por funcionalidade, objetivo, páginas testadas, controllers, etc. Neste projeto os testes foram divididos de forma a facilitar a navegação pelas seções presentes no [guia de testes](/docs/category/guia-de-testes), pois era o que fazia mais sentido dentro deste projeto específico. 

Lembre-se que a forma como você dividirá os testes depende dos padrões adotados pela sua equipe e pela sua facilidade de organização.

## Estrutura dos testes

É necessário que um teste tenha uma finalidade bem definida, como por exemplo testar o botão "Enviar" na página "Formulário de Cobrança". Mas além disso é necessário também que a forma como ele foi escrito tenha clareza e objetividade. Diante disto, a estrutura de um teste é fundamental para facilitar sua compreensão por outros desenvolvedores e mesmo para nos ajudar a organizar melhor a parte lógica. Este tutorial seguirá o modelo de **A**rrange **A**ct **A**ssert, ou AAA

### Arrange

Esta é a primeira etapa na escrita de um teste. Nesta etapa, você configura os objetos que serão testados. Você cria os objetos e configura seus estados iniciais, bem como quaisquer dependências externas que esses objetos precisam para funcionar corretamente. Isso pode envolver a criação de objetos fictícios (também conhecidos como mocks ou stubs), a preparação de entradas para o código que está sendo testado e a configuração de quaisquer condições prévias para o teste.

**Exemplo:** Adicionar um usuário ao banco de dados para testar a funcionalidade de deletar um usuário. O objetivo do teste é apagar uma entrada de dados, mas antes de apagar essa entrada nós precisamos criá-la.

### Act

Esta é a etapa onde você interage com o objeto que está sendo testado. Você realiza uma ação ou chama um método e armazena o resultado para testar na próxima etapa. O foco aqui é sobre o código que está realmente sendo testado. Pode ser que mais de uma ação ou método seja chamado, já que alguns testes dependem de múltiplas interações, como o preenchimento de um formulário.

**Exemplo:** Deletar o usuário. Enquanto os passos do **arrange** "preparam o terreno", a ação ocorre nesta segunda parte.

### Assert 

Nesta última etapa, você verifica se o resultado da ação (**Act**) é o que você esperava. Isto é onde você realmente "testa" o seu código. Enbora a ação tenha ocorrido na etapa anterior, é aqui que se torna possível verificar os resultados produzidos por aquela ação. Se o resultado não for o que você esperava, então o teste falha. 

**Exemplo:** Checar se o usuário ainda está presente. Caso após apagar a entrada do usuário ele continua presente o teste falhou. Aqui não há nenhuma outra ação que interaja com a aplicação de forma direta, mas sim realiza testes a respeito do seu estado após a etapa de **act**

Essa separação clara do que está sendo preparado, o que está sendo testado e o que está sendo verificado torna os testes mais fáceis de ler e entender. É também uma maneira útil de garantir que você está apenas testando uma coisa de cada vez.

## Executando seu primeiro teste

Siga os próximos passos para adicionar um teste à sua aplicação e depois executá-lo:

### Crie um arquivo

Conforme mencionado acima, os arquivos precisam estar dentro da pasta **test/system** e devem terminar com o sufixo **_test.rb**. 
É possível colocar dentro de uma subpasta a fim de organizar melhor os testes. Por exemplo, se eu tenho diversos testes de navegação, posso criar uma pasta com o nome **testenavegacao** e adicioná-la no diretório **test/system**, e todos os testes relacionados agora ficarão no diretório **test/system/testenavegacao**

:::info Arquivos já estão criados!
A fim de facilitar a estruturação, todos os arquivos que serão utilizados já estão disponíveis dentro dos diretórios.
:::

### Crie a estrutura básica do arquivo de teste

Em primeiro lugar, todos os arquivos de testes precisam de um *require* das nossas configurações definidas dentro de **application_system_test_case**. Além disso, é necessário que os testes estejam dentro de uma classe, e que essa classe herde a classe **ApplicationSystemTestCase**. A estrutura ficará parecida com este exemplo:

```
require "application_system_test_case"

class PrimeiroTeste < ApplicationSystemTestCase
  # TESTES REALIZADOS
end
```

O nome da classe e do arquivo normalmente são expressivos o suficiente para entender o que aquele conjunto de teste está verificando ou qual seu escopo geral.
___

### Adicione um teste dentro da sua classe

