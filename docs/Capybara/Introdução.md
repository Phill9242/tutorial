---
sidebar_position: 1
---

## O que é Capybara ?

Capybara é uma gem para Ruby utilizada para a criação de testes voltados para o comportamento do usuário. Isto quer dizer que ela é uma ferramenta que nos auxilia no desenvolvimento guiado por comportamento (BDD - Behavior-Driven Development), uma abordagem de desenvolvimento de software que prioriza a descrição do comportamento do sistema do ponto de vista do usuário.

:::tip Dica
O foco dos testes com Capybara está no resultado das ações do usuário, e não nos detalhes técnicos de como essas ações são processadas pelo sistema.
:::

## Como são feitos os testes com Capybara ?

Para exemplificar um pouco melhor vamos imaginar a seguinte situação: estamos desenvolvendo um aplicativo de compras e desenvolvemos uma funcionalidade que permite que o usuário remova itens de um carrinho de compras virtual. 

Para testar essa funcionalidade, criamos um teste com Capybara que emula a interação do usuário com o aplicativo no navegador. Seguiremos os passos:

* Acessar a página da loja;
* Adicionar um item carrinho de compras;
* Clicar no botão para remover o item.

Se todas as etapas foram seguidas e o item foi removido ao final, significa que a funcionalidade, do ponto de vista do usuário, está funcionando.
