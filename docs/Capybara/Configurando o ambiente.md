---
sidebar_position: 2
---
Antes da criação do primeiro teste é necessário que o ambiente esteja configurado da maneira correta. Este tópico irá lhe auxiliar a configurar de uma maneira simples e direta o Capybara com seu projeto rails para que trabalhem em conjunto.

## Projeto modelo

Para fazer a maior parte dos testes será utilizado um aplicativo simplificado criado com Ruby 3.0.1 e Rails 7.0.5. Como diversos testes irão envolver o envio de informação de formulários, não é uma boa prática utilizar sites ou aplicações que estão em operação, pois podemos acabar "sujando" a base de dados com informações falsas ou inúteis.

:::info Download projeto:
Baixe o projeto neste [link](https://github.com/Phill9242/capybara-test.git). 
:::

### Utilizando diferentes versões de Ruby e Ruby on Rails com ASDF

Projetos em Ruby e em Rails, assim como em diversas outras linguagens, nem sempre são escritos utilizando as mesmas versões da linguagem ou do framework. Isso significa que o ambiente em que você está programando precisa ter a mesma versão do projeto Ruby.

O ASDF é um gerenciador de versões que permite que você gerencie várias versões de diferentes linguagens de programação, como Ruby, Node.js, Python e muito mais. Ele fornece uma maneira fácil de instalar diferentes versões dessas linguagens e alternar entre elas.

Para instalar o ASDF, siga os passos abaixo.

* Clone o repositório do ASDF na sua máquina:

```
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.8.1
```
___
* Adicione o seguinte no seu arquivo **~/.bashrc** ou **~/.zshrc**:

```
. $HOME/.asdf/asdf.sh
```
___
* Instale o plugin Ruby no ASDF:
```
asdf plugin-add ruby https://github.com/asdf-vm/asdf-ruby.git
```
___
* Agora instale a versão do Ruby que deseja (3.0.1 para este projeto):
```
asdf install ruby 3.0.1
```
___
* Defina a versão 3.0.1 como a versão padrão:
```
asdf global ruby 3.0.1
```
___
* Por fim, instale o rails na versão 7.0.5:
```
gem install rails -v 7.0.5
```
___

:::tip Dica:
Caso tenha problemas ao utilizar o comando asdf após sua instalação, tente reiniciar seu terminal. Isso pode ocorrer pela forma como o terminal carrega as variáveis de ambiente durante sua inicialização.
:::

## Criando seu próprio projeto

Caso queira criar uma aplicação Rails com Capybara para realizar seus próprios testes, siga os passos abaixo.

Para começar, crie um novo projeto rails:

:::caution Atenção:
É necessário utilizar versão 2.7.0 ou superior de Ruby!
:::

```
rails new "nome do projeto"
```

Pronto, isto é tudo o que você precisa!

Ao abrir sua Gemfile poderá perceber que o capybara foi adicionado automaticamente. Isto porque a partir da versão 5 do Rails o capybara é instalado por padrão em conjunto com estas outras duas gems. Caso sua versão do Rails seja anterior, você deverá adicionar o capybara manualmente adicionando as gems descritas acima.

## Gems necessárias

Depois de baixar o projeto (ou iniciar o seu), abra a Gemfile e olhe o grupo de testes. Você verá algo parecido com isto:

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

## Criando um banco de dados para teste