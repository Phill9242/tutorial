---
sidebar_position: 2
---

### Criando sua Gemfile

Para começar, crie uma pasta e dentro desta pasta crie o seu arquivo Gemfile.

```
mkdir tutorialcapybara
cd tutorialcapybara
touch Gemfile

```

Vamos adicionar dentro do Gemfile as seguintes gems:

```
gem 'rspec'
gem 'capybara'
gem 'selenium-webdriver'
gem 'webdrivers'
```

**rspec**:

Esta é a gem principal para a criação de testes em Ruby. É uma gem membro da família [xUnit](http://xunitpatterns.com/xUnit.html) apesar de algumas diferenças com a escrita clássica do xUnit.

Seu objetivo é tornar a escrita de testes mais fácil, utilizando uma linguagem muito próxima da natural, ou seja, a forma como nos comunicamos. Também será a responsável por construir a "fundação" da nossa versão simplificada de testes, com os arquivos e pastas necessários.

**capybara**:

Capybara - foco dos nossos estudos - será utilizada para realizar a interação com as páginas. Através de sua DSL ela oferece diversos métodos que são capazes de interagir com o DOM e imitar o comportamento de um usuário.

**selenium-webdriver**:

A gem Selenium WebDriver é uma ferramenta de automação de navegador. A capybara utiliza a selenium para interagir com nosso nevagador.

**webdrivers**:

A gem Webdrivers simplifica o gerenciamento dos drivers necessários para a Selenium WebDriver se comunicar com diferentes navegadores.


### Configurando o Rspec

Vamos começar instalando as gems através do comando:
```
bundle install
```

Após instalar todas as dependências, configure o projeto com o comando abaixo:

``` 
rspec --init
```

Um arquivo chamado *spec_helper.rb* deve ter sido criado dentro da pasta *spec*.

Para configurar nosso arquivo, vamos inicialmente fazer um require no topo dele, adicionando

```
require 'capybara/rspec'
```

Agora adicionaremos abaixo do laço ```RSpec.configure do |config|``` a seguinte configuração:
```
config.include Capybara::DSL
```

Por fim, adicionaremos à linha final:

```
Capybara.run_server = false
Capybara.default_driver = :selenium
```

Ao fim, nosso arquivo de configuração ficará parecido com o exemplo abaixo:

```
require 'capybara/rspec
# código suprimido

RSpec.configure do |config|
  config.include Capybara::DSL
# código suprimido
end

# código suprimido
Capybara.run_server = false
Capybara.default_driver = :selenium
```
:::tip TO DO
  colocar link que aponta para configurar webdriver headless
:::