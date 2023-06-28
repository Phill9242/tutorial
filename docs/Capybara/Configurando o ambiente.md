---
sidebar_position: 2
---
Antes da criação do primeiro teste é necessário que o ambiente esteja configurado da maneira correta. Este tópico irá lhe auxiliar a configurar de uma maneira simples e direta o Capybara com seu projeto rails para que trabalhem em conjunto.

:::caution Atenção
Este tutorial parte do pressuposto que seu sistema operacional é Unix-like.
:::

### Projeto modelo

Para fazer a maior parte dos testes será utilizado um aplicativo simplificado criado com Ruby 3.0.1 e Rails 7.0.5. Como diversos testes irão envolver o envio de informação de formulários, não é uma boa prática utilizar sites ou aplicações que estão em operação, pois podemos acabar "sujando" a base de dados com informações falsas ou inúteis.

:::info Download projeto:
Baixe o projeto neste [link](https://github.com/Phill9242/capybara-tests.git). 
:::

### Gems necessárias

Abra a Gemfile do projeto e olhe o grupo de testes. Você verá algo parecido com isto:

```
group :test do
  gem "capybara"
  gem "selenium-webdriver"
  gem "webdrivers"
end
```

**capybara**:

Capybara - foco deste tutorial - será utilizada para realizar a interação com as páginas. Através de sua DSL ela oferece diversos métodos que são capazes de interagir com o DOM e imitar o comportamento de um usuário.

**selenium-webdriver**:

A gem Selenium WebDriver é uma ferramenta de automação de navegador. A capybara utiliza a selenium para interagir com o nevagador.

**webdrivers**:

A gem Webdrivers simplifica o gerenciamento dos drivers necessários para a Selenium WebDriver se comunicar com diferentes navegadores.



### Criando seu próprio projeto

Caso queira criar uma aplicação Rails com Capybara para realizar seus próprios testes, siga os passos abaixo.

Para começar, crie um novo projeto rails:

:::caution Atenção:
É necessário utilizar versão 2.7.0 ou superior de Ruby!
:::

```
rails new **"nome do projeto"**
```

Pronto, isto é tudo o que você precisa!

Ao abrir sua gemfile poderá perceber que o capybara foi adicionado automaticamente. Isto porque a partir da versão 5 do Rails o capybara é instalado por padrão em conjunto com estas outras duas gems. Caso sua versão do Rails seja anterior, você deverá adicionar o capybara manualmente.

