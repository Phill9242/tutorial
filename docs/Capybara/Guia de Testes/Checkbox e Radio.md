---
sidebar_position: 4
---

## Checkbox

### Método ***check***

Marcar checkboxes não é uma tarefa complicada com Capybara. Depois de individualizar o elemento, basta utilizar o método ***check***. Coloque dentro de seu arquivo **checkbox_and_radio_test.rb** o exemplo abaixo:

```
test "testar checkbox com duas seleções" do
  visit checkbox_path
  check "check2"
  check "check3"
  click_button "botaocheckbox"
  total_messages = all('.alert').count
  assert_equal total_messages, 2
end

```
**Analisando o teste:**

* O método ***check*** marca uma caixa de seleção disponível;

* após, o método ***click_button*** é utilizado para poder enviar o formulário;

* aqui o ***all*** retorna todos os elementos que contém a classe **.alert**;

* o número total de elementos é contado com o ***count*** e depois salvo dentro da variável;

* por fim, faz-se a verificação se o número de mensagens total é igual a 2 (que é o número de mensagens esperado, já que dois checkboxes foram selecionados antes do envio).

### Método ***uncheck***

Diferente da interação real do usuário, ao interagir diversas vezes com o mesmo campo de um checkbox ele não será selecionado e desselecionado a cada vez que você utilizar o método ***check***. Caso um campo já esteja selecionado, ao utilizar este método nada acontecerá. Para remover a marcação de um campo você deve utilizar o método ***uncheck***. Confira no exemplo abaixo:

```
test "testar checkbox depois de selecionar e remover a seleção" do
  visit checkbox_path
  check "check2"
  uncheck "check2"
  click_button "botaocheckbox"
  total_messages = all('.alert').count
  assert_equal total_messages, 0
end

```

O exemplo acima parece muito com o anterior, mas ao invés de esperar 2 mensagens, nenhuma mensagem é esperada, pois o campo foi marcado com ***uncheck*** após a seleção inicial. Como o ***uncheck*** veio depois, ele irá se sobrepor ao ***check***.

## Radio Button

Para *radio buttons* o Capybara tem algo muito semelhante ao que disponível para *checkboxes*. O método ***choose*** irá procurar por um elemento do tipo *radio button* e irá marcá-lo. Confira no exemplo abaixo:

```
test "Radio button com botão marcado" do
  visit checkbox_path
  choose "radio1"
  click_button "botaoRadio"
  assert_selector ".alert"
end
```

Sempre que utilizar o método ***choose*** para escolher uma opção, as outras são desmarcadas automaticamente, já que o *radio button* só aceita uma opção. Além disso, diferentemente do método ***check***, não é possível desmarcar uma opção sem selecionar outra; assim como acontece com a interação do usuário em um cenário real, depois que um campo é selecionado a única forma de desmarcá-lo e marcando algum outro campo.

