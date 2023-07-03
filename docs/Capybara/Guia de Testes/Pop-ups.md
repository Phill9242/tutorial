---
sidebar_position: 5
---

Os pop-ups são considerados como janelas. Sempre que interagir com um elemento que abra uma nova janela a melhor forma de lidar com ele é utilizando o método ***window_opened_by*** ensinado no tópico sobre [botões que abrem novas janelas](Botões#botão-nova-janela).

Testes realizados na janela  retornada pelo método ***window_opened_by*** funcionarão da mesma forma que qualquer outro teste. Imagine que você está realizando um teste dentro de um teste.

Para fins didáticos vamos analisar mais uma vez como funciona. Coloque o teste abaixo dentro do arquivo **popup_test.rb**:

```
test "testar janela de popup" do
  visit botoes_path

  janela_aberta = window_opened_by do
    click_button "botaonovajanela"      
  end

  within_window janela_aberta  do
    visit checkbox_path
    check "check2"
    click_button "botaocheckbox"
    total_messages = all('.alert').count
    assert_equal total_messages, 1
  end
end
```

* O método ***window_opened_by*** pega a janela aberta ao clicar no botão **botaonovajanela** e retorna-a;

* Essa janela é salva dentro da variável janela_aberta;

* Ao utilizar método ***within_window*** passando como parâmetro a janela_aberta, é possível interagir com essa janela dentro do bloco entre "do ... end";

* Dentro deste bloco realize os testes normalmente;

Claro que este exemplo utiliza de fato uma nova janela aberta, mas um popup segue o mesmo princípio, e utilizar esse método para realizar os testes funcionará corretamente.

:::note Recapitulação
Ao abrir uma nova janela ou popup com o método ***window_opened_by***, é possível mudar o contexto do teste com o método ***within_window***. Assim, é possível realizar os testes normalmente dentro deste bloco de código
:::