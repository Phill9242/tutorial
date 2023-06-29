---
sidebar_position: 4
---

Escrever testes automatizados é uma prática indispensável no desenvolvimento de software, mas a elaboração de testes de qualidade pode se tornar um desafio. Quando mencionamos testes de qualidade, falamos de testes que são claros, concisos, confiáveis e, acima de tudo, úteis. A seguir, estão algumas práticas recomendadas que ajudarão a atingir esse objetivo ao escrever testes com qualquer ferramenta, não apenas com Capybara.

### Testes devem ser descritivos

Nomeie seus testes de modo a descrever o que estão verificando. Assim, ao ler o nome do teste, qualquer pessoa (inclusive você no futuro) poderá compreender rapidamente a sua finalidade. Isso é especialmente importante quando um teste falha, pois um nome descritivo pode ajudar a identificar mais rapidamente a causa do problema.

Não tenha receio de que os nomes dos seus testes sejam longos, o importante é que eles sejam autoexplicativos e específicos. Por exemplo, se o seu teste preenche um formulário, ao invés de dar um nome genérico como **preencher formulário**, o melhor é que ele especifique qual formulário está preenchido, como **preenche o formulário de cadastro de novos clientes de forma válida**.

### Testes devem ser isolados

Cada teste deve poder ser executado de forma independente de qualquer outro. Isso significa que o resultado de um teste não deve depender do resultado de outro. Essa prática é essencial para a confiabilidade dos testes e para evitar falhas intermitentes.

Por exemplo, suponha que existe um teste que remove uma entrada no banco de dados e um segundo teste que verifica se essa entrada existe. Dependendo da ordem em que os testes são realizados, eles podem passar ou falhar. Esse é um problema, pois os testes devem ser previsíveis e consistentes. Portanto, é necessário garantir que cada teste seja configurado para ser executado de forma isolada.

:::note Contornando o problema acima:
A criação do ambientes de teste e mock de dados será abordada em um ponto futuro deste tutorial. (TO DO)
:::

### Testes devem ser atômicos

Idealmente, cada teste deve verificar uma única funcionalidade ou aspecto do software. Quando um teste falha, saber exatamente qual aspecto do software está com problemas facilita a identificação e a correção do problema. 

Portanto, nunca crie testes que tem muitas *responsabilidades*, um teste ideal verifica o menor número possível de aspectos ou funcionalidades por vez. Por exemplo: se seu teste faz uma checagem em uma página, e verifica se todos os botões estão funcionando e ainda testa o preenchimento de formulário de forma válida e inválida ele está acumulando responsabilidades demais. O ideal é dividí-lo em outros testes e torná-los mais concisos. Lembre-se: o teste deve ser **descritivo**, porém **específico**.

### Mantenha os testes DRY

:::info DRY:
DRY é uma sigla para * **D**on't **R**epeat **Y**ourself*.
:::

Assim como em qualquer outro código, evite a repetição nos testes. Se estiver repetindo as mesmas configurações em vários testes, talvez seja possível extrair esse código comum para um método ou função auxiliar. Isso não só torna os testes mais limpos e fáceis de ler, mas também facilita a manutenção, pois qualquer mudança no código comum só precisa ser feita em um lugar.

Essa prática também será abordada neste tutorial em um ponto futuro. (TO DO)

### Entenda a aplicação que você está testando

Antes de começar a escrever testes, é essencial entender completamente a funcionalidade do aplicativo que você está testando. Isso inclui como os usuários devem interagir com a aplicação, quais resultados são esperados e onde podem ocorrer problemas. Quando falamos de BDD e testes voltados ao usuário é isso que sempre temos que manter como foco.

### Sai do "caminho feliz"

O caminho feliz é o comportamento esperado quando tudo sai exatamente como queríamos. Este é o cenário ideal, não o real. Testes devem abordar todos os caminhos possíveis: **Não se limite a testar o "caminho feliz"**. Por isso testar os cenários de erro é tão importante quanto testar cenários de acerto. Lembre-se: o usuário não está tão familiarizado com a aplicação quanto você, e provavelmente não sabe como ela deve se comportar. É seu papel assegurar que nada dará errado, mesmo quando ele não souber o que está fazendo.

### Priorize os testes mais importantes:

Embora seja ideal ter uma cobertura de teste de 100%, isso nem sempre é possível, prático ou necessário. Priorize os testes para as partes mais críticas da sua aplicação. 

### Mantenha seus testes atualizados:

À medida que seu aplicativo muda, seus testes também precisarão mudar. Certifique-se de manter seus testes atualizados para refletir as funcionalidades atuais do seu aplicativo.

### Evite testes frágeis: 

Tente escrever testes que não quebrem com pequenas alterações na interface do usuário. Por exemplo, em vez de depender do texto exato de um erro, teste se algum tipo de mensagem de erro está presente.