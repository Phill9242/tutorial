---
sidebar_position: 2
---

## Configurando seu ambiente


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

Ao fim, nosso arquivo de configuração ficará parecido com isso

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
:::info TO DO
  colocar link que aponta para configurar webdriver headless
:::

## Nossos primeiros testes

### Regras gerais para uso do Rspec

Em primeiro lugar, é necessário que todos os testes criados utilizando o Capybara em conjunto com o Rspec estejam dentro da pasta **spec**. Isto porque, por convenção, o Rspec procura por testes no diretório **spec** quando executado

Além disto, devemos nomear os nossos testes com o final **_spec.rb**: 
* **_spec** sinaliza para o Rspec que aquele arquivo contém uma suíte de testes a ser executada;
* **.rb** determina que a extensão do arquivo é Ruby. 

### Criando o primeiro arquivo de teste

Seguindo as regras acima, vamos criar nosso primeiro teste dentro da pasta spec com o nome **teste_spec.rb**

```
touch spec/teste_spec.rb

```

