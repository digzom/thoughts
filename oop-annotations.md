# Laboratório de Orientação a Objetos

- Objeto -> Guarda dentro de si os dados e o códigos dos dados. Ao invés de dados espalhados, temos os dados separados, encapsulados junto com o código que manipula esses dados. Isso é um objeto.
- Dados -> Variáveis e atributos
- Código -> Funções e métodos
- Uma classe é uma fábrica de objetos. Instanciação de objetos.

**Quando um método de uma classe A está chamando a execução de um método de uma classe B, esse método da classe A está enviando uma mensagem**. Enviando "pula" para o método da classe B, ele procurará um método com esse nome para executá-lo. O método executado pode ou não retornar alguma mensagem.

Quando o sistema cria a classe bola, **a classe já aloca memória para suas variáveis de classe**. Dessa forma, os valores das variáveis de classe são _compartilhados_ entre as instâncias das classes. Já para as variáveis de instância, a memória não é alocada na definição da classe, mas na instanciação do objeto da classe.

## Herança 

Herança é uma forma de evitar duplicação e promover o reúso de código. Quando uma classe herda da outra, ela pode herdar certos atributos e adicionar os seus próprios. A relação entre herança é "é-um". Se a Classe B herda da Classe A, dizemos que Classe B é uma Classe A. É possível reimplementar certos atributos/métodos da classe mãe.

Quando, a partir da classe filha, chamamos um método, a linguagem vai primeiro procurar o método no escopo mais próximo (na classe que está invocando o método). Se não existir, será buscado na classe mãe.

Superclasse -> Subclasse => Especialização
Subclasse -> Superclasse => Generalização

**This** referencia o próprio objeto/classe. Com ele podemos 
UML -> útil para definir arquitetura de sistemas; 

## Linguagens interpretadas vs compiladas

Linguagem de máquina (binário) -> linguagem de montagem (assembly) -> linguagens de alto nível (FORTRAN, LISP) 

### Linguagens interpretadas

1. Escreve o código fonte num arquivo texto
2. Esse arquivo é dado como entrada para um programa chamado interpretador
3. O interpretador lê uma linha por vez e interpreta a linha e traduz para linguagem de máquina e executa
4. O programa gera saídas

### Linguagens compiladas

1. Código fonte
2. É dado como entrada para um programa chamado compilador
3. Gera um "código objeto" (por isso a saída .o de C), que é linguagem de máquina
4. Depois esse código objeto é executado por um outro programa (geralmente o sistema operacional) 
5. Por isso falamos em "checagem em tempo de compilação", para compilar, o programa precisa estar correto nos termos da compilação esperada

-- Linguagens híbridas

Java e python são assim

1. O compilador traduz o código-fonte para bytecode (linguagem dos criadores do java, parecido com assembly). 
2. Ele é gravado num arquivo .class.
3. Para executar o programa, será usado um programa interpretador de java (na JVM) que vai ler os bytecodes, converter para linguagem de máquina e executar.

## Filosofia do java

***Write once, run everywhere***.

- Rodar em vários tipos diferentes de máquinas e SOs
- Linguagem para a internet

Ao escrever um programa, escrevemos para a máquina virtual do java ao invés de escrever para a nossa máquina. Então qualquer computador com a JVM poderia rodar o programa em java independente da arquitetura do processador ou sistema operacional. Existe uma JVM para android, outra para pc, outra para relógio, etc.

A JVM de um processador terá o JRE, que terá validação do bytecode, o interpretador JIT compiler, o garbage collector e as bibliotecas padrão do Java.

Outras linguagens criaram linguagens para gerar bytecode (existe em python, clojure)

A maioria das linguagens hoje são híbridas.

Métodos são funções dentro do escopo de uma classe.

**Prefira usar delegação ao invés de herança**

Ex.: Num sistema de logging e eu quero um log específico, é possível criar uma subclasse específica que herda da superclasse de log geral. Isso amarra o código. O que pode ser feito é delegar a impressão das diferentes strings de logs para uma classe separada. Assim uma classe não dependerá da outra.

**Encapsulamento e Modularização**

Agrupar código, api da classe (métodos privados são mais flexíveis para mudança). Uma classe não deve mexer nos atributos de classe de outra classe. 

**Coesão** -> As classes precisam ter apenas uma responsabilidade (princípio da responsabilidade única);

**Acoplamento é ruim** -> O quanto uma classe "conhece" ou mesmo "depende" do seu entorno; o quanto aponta, faz referência ou uma nomes de métodos ou outras classes. Quanto mais acoplado, menos flexível a classe será; é bom que classes sejam mais genéricas do que específicas. "Program to an interface, not an implementation".

## Linguagens Estáticas

Java, C, Pascal, Scala.

- É preciso declarar variáveis antes de usá-las:

```java
int variable;
```

- É preciso definir os tipos dos métodos e das variáveis;
- É possível identificar erros em tempo de compilação;

## Linguagens Dinâmicas

Lisp, Lua, Python, Elixir, Javascript.

- Não é preciso declarar as variáveis;
- A variável não precisa de anotação de tipo;
- A checagem de tipo só é feito em runtime;

```python
x = 32
carro = Carro()
```

## Outras características de linguagens dinâmicas

Enquanto linguagens estáticas geralmente são executadas utilizando um compilador, linguagens dinâmicas usam um interpretador.

- Capacidade de executar trechos da linguagem em tempo de execuação;

```js
exec("print('hello')")
```

- Reflexão computacional
  - Alterar estrutura do código em tempo de execução
  - Consultar a estrutura em tempo de execução.
- Gestão automática de memória
  - Garbbage Collector

## Coleções

- Implementam o tipo Iterable
  - Stack
  - ArrayList
  - List
  - LinkedList
- ArrayList -> se eu uso List.get(8), ele vai no sétimo elemento do array e pega; se eu ficar um get numa LinkedList, ele precisa percorrer os elementos (os apontadores) para achar o elemento que eu escolhi.
- É possível criar uma classe própria e implementar um for (desde que a classe ou método implemente a interface Iterable) e chamar o método para uma estrutura de dados específica. Tipo Protocols.
 
## Interface

- Functiona como uma classe puramente abstrata
- Tem uma lista de assinaturas dos métodos
  - Interface é um conjunto de operações que outras classes vão implementar
- Deve ser implementada por outras classes através da palavras `implements`
- Todas as variáveis são `public static final`

Com interfaces podemos definir tipos comuns, sem definir o comportamento, apenas as operações. Ou seja,
quais são as mensagens que aquele objeto entende, sem dizer necessariamente o que ele faz quando
recebe a mensagem. Quem escolhe o que fazer com a mensagem é uma classe que implementa o objeto.

### Exemplo

Num jogo, teríamos a ‘interface’ **ObjetoEspacial**, que poderia ser uma nave, um asteróide ou qualquer coisa assim.
*Ver exemplo ObjetoEspacial.java*

### Observações

- Em java não é possível fazer herança múltipla, mas é permite fazer herança múltipla de interfaces.
- É possível ter uma interface que estende outra interface.

## Polimofismo

- Multiplas formas
- 3 tipos
  - paramétrico (*generics*)
  - sobrecarga de métodos (*overloading*)
  - sobreescrita de métodos (*overriding*)

### Polimorfismo Paramétrico

```
ArrayList<Strig> a = new ArrayList<>();
ArrayList<Integer> a = new ArrayList<>();
ArrayList<SideralObject> a = new ArrayList<>();
```

Aqui estamos criando um ArrayList onde os elementos dentro do array serão do tipo que está descrito
entre o `<>`. A implementação do ArrayList foi feito como tipo genérico. Quando definimos tipos
genéricos e uma classe é tipada assim, essa classe pode receber um tipo como parâmetro e podemos
criar um código genérico que funciona com o parâmetro.

### Sobrecarga de Métodos

- 2 ou mais métodos com o mesmo nome

É quando dois ou mais métodos tem o mesmo nome, diferenciando nos seus argumentos. Seja na quantidade
quando no tipo.

### Sobreescrita de métodos

- Herança / subtipos
- O método da classe filha que tem a mesma assinatura do método da classe mãe, e o sobrepõe.
- Com uma boa classe genérica, alguém pode implementar uma classe a partir da que você criou para resolver um problema específico

### Observações

Polimorfismo ajuda a definir diferentes comportamentos para um mesmo método. Evita-se código repetido.
Mas há uma clara desvantagem: as coisas ficam menos claras e declarativas. Só ser um método `toString` não basta para
saber o que esse método está fazendo, já que cada classe pode sobreescrever esse método e implementar da forma
que preferir. Então temos que olhar nas subclasses.

## Tratamento de exceções

É necessário tratar os erros das aplicações.

### Try/catch

Separar o erro da execução do código pode trazer ganhos em desempenho (por questões de cache). Além disso,
separar o bloco de execução do bloco de erro é uma boa forma de organizar o código. Eu já conhecia isso.

É possível definir nossas próprias exceções, herdando da classe `Exception`.

É possível não tratar as `exceptions`, mas é obrigatório especificar que o método pode retornar uma,
dessa forma:

```java
import java.io.IOException;

public class LeitorDeArquivo {
  static char[] leArquivo(String nomeArq) throws IOException {
//      implementation
  }
}
```

Assim, quem chama o método precisará tratar essa exceção.

## I/O Streams

Tratamento de entrada e saída de dados em um fluxo contínuo.

- Entrada
  - Arquivo, rede (TCP/IP), teclado, array
- Saída
  - Arquivo, rede, impressora, array, tela

Em sistemas operacionais, nós temos as entradas e saídas padrão. A comunicação do Java com a entrada e saída padrão é
feita através de algumas classes:

- InputStream System.in
- PrintStream System.out
  - Essa classe PrintStream tem métodos do tipo `Print`, que é do mesmo método do `println`
- PrintStream System.err

### BufferedInputStream

Essa classe provê métodos para ser os bytes/inputs por blocos. Ou seja, ao invés de ler byte à byte enquanto chega o 
input, ao fazer uma chamada, essa classe já trás uma certa quantidade de bytes para a JVM e processa essa quantidade,
lendo os bytes que foram trazidos um por um. Depois de ler essa quantidade é que será feita outra chamada para pegar 
mais bytes e refazer o processo. A vantagem dessa técnica é que se faz menos chamadas ao sistema operacional, 
economizando processamento. 

## Orientação à Objetos no Javascript

O javascript implementa orientação à objetos através da ideia de `prototypes`. Um objeto é instanciado através de 
objetos prototípicos, então um objeto é usado como um molde para a criação de outros objetos. É uma ideia que tem 
influência da linguagem `Self`, que por sua vez é uma variante da `Smalltalk`. A linguagem `Self` também não tinha 
implementação de classes.

## Instanciação

Quando é feita a declaração de variáveis estáticas, essas variáveis são criadas na área Stack da memória.
Em runtime, é possível fazer uma alocação dinâmica de memória na região da memória Heap, que armazena aloca memória durante a execução. A gente faz essa alocação dinâmica quando instanciamos objetos.

Ao instanciar `x = new MyClass`, eu aloco memória da região Stack com o endereço de memória da região Heap, usando esse endereço de memória da Stack como uma referência para o endereço de memória que é alocado dinamicamente na região Heap. Na região Heap, terei a memória alocada para o meu objeto, junto com seus atributos. 

Ou seja, a variável X não contém um valor em si, ela é uma referência para o objeto que está no Heap.


## Ainda sobre delegação

Quem tem que calcular a área de um triangulo, é a classe `Triângulo`. Quem tem que calcular o valor de um pedido é a classe `Pedido`. A delegação deve ser feita para quem cuida do domínio do problema.

## Classe Object

Toda classe herda da classe Object. A classe object tem alguns métodos padrão que todas as classes podem sobreescrever, como o `toString`, por exemplo. Além disso, em todas as classes nós teremos esses métodos padrão.

Sobrescrevendo o `toString`, você consegue fazer com que sua classe lide com o caso de uso da sua classe de forma correta e específica. É tipo `protocols` no elixir.

Inclusive, o Java consegue detectar caso o objeto esteja dentro de um `println` ou outros métodos parecidos e utilizar o `toString` que está no objeto em questão. 

### Exercícios

- Implementei um código que calcula a área de um triângulo.
- Implementei uma classe que demonstra as informações de um funcionário. Utilizei métodos privados, deixando público apenas o método que recebe uma porcentagem de aumento do salário do funcionário.


## Métodos estáticos

Um método estático não pode chamar um método não estático da mesma classe. 

### Operação de instância (de objeto)

Numa classe `Triangulo` que implementa o método `area` para obter a área do triângulo instanciado, cada triangulo instanciado terá uma área diferente.

### Operação de classe

Já no caso de um método `add` que soma dois números, implementa comportamentos estáticos, ou seja, comportamento que independem do objeto instanciado. 

O método `add`, dado os mesmos valores como argumentos, terá sempre o mesmo resultado.

## Construtor

O construtor executa no momento da instanciação do objeto. Geralmente é usado para iniciar valores do atributos e permite (em alguns casos, obriga) que o objeto seja instanciado a partir de determinados argumentos.

Não é porque você não definiu o construtor que ele não existe. A classe sempre vai disponibilizar o constructor padrão. Por isso, quando instancia-se uma classe assim: `Product p = new Product();`, o `Product` é um construtor padrão.

Além disso, é possível ter mais de um construtor por classe.

## This

O this é uma referência para o próprio objeto.

Usado para:

- Diferenciar variável/atributo local de variáveis externas
- Passar alguma propriedade do próprio objeto na chamada de um método

Em memória, é criado o escopo do construtor daquele objeto com a cópia das variáveis passadas por parâmetro e outras variáveis locais (caso existam). Ao escrever, no construtor:

```java
public Example(String var1, int var2) {
  this.var1 = var1;
  this.var2 = var2;
}
```

Os valores do construtor serão copiados para os espaços de memória do objeto `Example`. Note que o `this` remove a ambiguidade do argumento e ao mesmo tempo ajuda a dar "match" pelo nome.

### Passando o próprio objeto como chamada de um método ou construtor

Ao chamar um método, podemos "compartilhar" o estado da própria classe com esse método, caso necessário:

```java 
public class Example {
  (...)

  someMethod('arg1', arg2, this)

  (...)
}
```

Dessa forma, o metodo `someMethod`, que pode ser um método de outra classe, inclusive, consegue ter acesso ao estado atual do objeto `Example`, podendo, internamente, aplicar herança, modificar atributos, etc. É algo que tem que ser feito com certo cuidado, mas é possível.

## Sobrecarga

Permite que uma classe ofereça mais de uma operação com o mesmo nome, porém com diferentes parâmetros. (tipo elixir, só que um pouco menos poderoso, pois não tem um pattern matching tão avançado quanto). Inclusive, para que os argumentos na instanciação sejam opcionais, é só criar um construtor com parâmetros vazios.

## Encapsulamento

Consiste em esconder detalhes de implementação de uma classe, expondo apenas as operações necessárias. **O objeto deve sempre estar em um estado consistente, e a própria classe deve garantir isso**.

Um objeto não deve expor seus atributos.

Para "esconder" atributos ou métodos, é só usar `private`.

O ideal é acessar/alterar os atributos através de métodos get/set.

--- **POJO** ---

## Modificadores de acesso

Private -> Só pode ser acessado no escopo da classe
Public -> Pode ser acessado fora da classe (também em outro módulo, desde que importe o package)
Nada -> Pode ser acessado no escopo do package
Protected -> No escopo do package e nas subclasses

# Projetinho Banking

Tipo char;
Scanner só pega o char se fizer assim: `sc.next().chatAt(0);`
`.next()` é para pegar o próximo valor da linha em questão. `.nextLine()` é para pegar o valor da próxima linha.

# Tipos referência X Tipos valor

## Tipos referência

Classes são tipos referências. São variáveis que não devem ser entendidas como caixas, mas sim como "tentáculos" (ponteiros) para caixas.

É aquele papo de um objeto instanciado funcionar como uma referência, ou seja guardar, na memória Stack, o endereço de memória da memória Heap onde estão os valores (atributos) daquela classe. 

Quando a gente instancia um objeto `p1`, o endereço de memória stack no qual esse objeto alocou tem uma referência para a memória de alocação dinâmica Heap. Se a gente atribui o valor de `p1` para uma variável `p2`, `p2` apontará para o mesmo endereço de memória que `p1`. Ou seja, se alguma modificação nos atributos da classe for feita em `p2`, será o mesmo que estar fazendo em `p1` também.

## Tipos valor

Em java, tipos primitivos são tipos valor. Tipos valor são caixas e não ponteiros.

Se eu faço `double x = 10.00`, x vai armazenar em memória Stack (estática) o valor de x, não uma referência para outra memória.

Nesse caso, quando a gente faz a atribuição de uma variável `Type p2 = p1;`, nós criamos uma **cópia** do valor de `p1` e armazenamos no novo endereço de memória `p2`. Nesse caso, não há compartilhamento de estado.

## Valores padrão

Quando alocamos qualquer tipo estruturado (classe ou array), são atribuídos valores padrão ao sseus elementos. Ex.:

- int/float/double/long/etc -> 0/0.0
- boolean -> false
- char: char code 0
- object: null

# Desalocação de memória - garbage collector e escopo local

## Garbage collector

- Automatiza o gerenciamento de memória de um programa em execução
- O garbage collector monitor os objetos alocados dinamicamente pelo programa (no heap), desalocando aqueles que não estão mais sendo utilizados.

```java
TypeClass p1 = new TypeClass("TV", 900.00, 0);
TypeClass p2 = new TypeClass("Bike", 400.00, 0);

p1 = p2;
```

No snippet acima, p1 é coletado pelo garbage collector e a memória que `p1` alocava é liberada na Heap.

## Desalocação por escopo

```java
void myMethod() {
  int x = 10;
  if (x > 1) {
    int y = 20;
  }
  System.out.println(x);
}
```

No snippet acima, a variável `y` foi com deus. 

O que acontece é que nós temos, na memória stack, o escopo de memória alocada pelo método. Dentro do escopo do método, teremos a variável `x` que foi declarada. Logo depois alocaremos uma parte do escopo do `myMethod` para o `if` statement, criando um subescopo. A variável `y` será alocada dentro desse subescopo do `if`. Ao sair do `if`, todo o escopo do if é liberado, incluindo a variável `y`.

A mesma coisa acontecerá com a variável `x` quando esse método acabar.

```java
void method1() {
  Product p = method2();
  System.out.println(p.Name);
}

Product method2() {
  Product prod = new Product("TV", 900.0, 0);
  return prod;
}
```

Nesse exemplo, `method2` estará num subescopo na memória alocada pelo `method1`, e `method2` está apontando para um endereço de memória Heap que aloca dinamicamente os valores dos atributos da classe `Product`. Ao terminar o `method2` (ou seja, no retorno do método), a memória alocada para `prod`, que está no escopo do `method2` vai ser liberada, assim como o subescopo do `method2`, pois a execução agora volta para o `method1`.

No caso da variável `p` que está no escopo do `method1`, ela estará apontando para o mesmo endereço de memória Heap que `prod` estava apontando. Então, no escopo do `method1`, a memória alocada no Heap não será liberada/desalocada, pois ainda há referência à este endereço.

### Resumo

Objetos alocados dinamicamente, quando não possuem mais referênciap ara eles, serão desalocados pelo garbage collector

Variáveis locais são desalocadas imediatamente assim que seu escopo local sai de execução.

# Vetores

- São arrays unifimensionais
- Arrays são estruturas :
  - Homogêneas (dados do mesmo tipo);
  - Ordenadas (elementos acessados por meio de posições);
  - Alocadas de uma vez só em um bloco contíguo de memória;

### Vantagens

- Acesso imediato aos elementos pela sua posição

### Desvantagens

- Tamanho fixo
- Dificuldade para realizar inserções e deleções
  - Para inserir algo numa parte específica do array, é preciso "empurrar" os elementos posterioes para frente. No caso da deleção é a mesma coisa, só que vamos "puxar" os posteriores para trás. Em arrays gigantes, dentro que fazer alterações em posições muito distantes, isso é uma grande desvantagem.

## Boxing

- Boxing é o processo de conversão de um objeto tipo valor para um objeto tipo referência compatível.

Quando eu faço 

```java
x = 20;
```

E logo depois 

```java
Object obj = x;
```

Eu estou alocando bloco de memória heap. A variável `obj` estará apontando para essa referência.


## Unboxing

É o processo contrário. É quando convertemos um objeto tipo referência para um objeto tipo valor compatível.

Se, continuando o snippet acima, eu fizer

```java
int y = (int) obj;
```

Eu aloco memória da região stack com o valor de `obj` que estava na memória heap.

## Wrapper classes

São classes "equivalentes" aos tipos primitivos do java. Ou seja, para o tipo `boolean`, nós temos a classe `Boolean`. Para o tipo `char` nós temos a classe `Character`, etc.

Isso existe para que o java consiga fazer o boxing/unboxing de forma mais orgânica. No snippet acima nós tivemos que usar casting (colocar o tipo entre parênteses), mas se tivéssemos criado a variável `obj` assim: `Integer obj = x;`, então não seria necessário usar o casting, pois a wrapper class sabe como tratar aquele tipo primitivo. 

**Tipos referência aceitam valor nulo**.

Uso comum: campos de entidades em sistema de informação, pois para que tenhamos algumas vantagens de orientação há objetos, é bom criarmos variáveis com sua wrapper class ao invés do tipo primitivo puro. Pois poderemos usufruir de vantagens de OO (como métodos, herança, etc) e também poderemos inicializar os campos como nulos.

## List

- Lista é homogênea (elementos do mesmo tipo)
- Ordenada
- Inicia vazia e seus elementos são alocados sobre demanda
  - Esse comportamento é diferente de array, que precisa ser iniciado com número de elementos conhecido
- Cada elemento ocupado um `nó` (node)

Esta é a linked list, ou lista encadeada. É quando cada nodo da lista aponta para o próximo nodo.

Classes que implementam a interface `List`: ArrayList, LinkedList, etc.

Listas não aceitam tipos primitivos como generic, é precisa usar a wrapper class.

### Vantagens

- Nesse tipo de lista é mais fácil fazer inserção ou deleção de um elemento.

### Desvantagem

- O acesso aos elementos é sequencial.
  - Vale ressaltar que mesmo sendo sequencial e precisando percorrer todas as referências para chegar num elemento, dentro da implementação das classes que extendem a interface existem otimizações para essa busca.

## Enums

- Especifica de forma **literal** um conjunto de constantes relacionadas.
- A maior vantagem é que é super legível, semântico e auxiliado pelo compilador.

## Tópicos sobre UML

Em UML, quando temos um diamante numa entidade A e uma seta para uma entidade B, a entidade A é o TODO e a entidade B é uma parte. Ou seja, B compõe A. Associação é diferente de ser "parte", mas mesmo assim pode ser uma composição.

## Estrutura de posts/comments

Para criar composição entre uma classe e outra, é possível fazer algo como um "has many". Você cria uma classe e dentro dessa classe você instancia uma lista (ou outra estrutura) da classe que a compõe. Ex.:

```java
public class Post {
  private List<Comment> comments = new ArrayList<>()
}
```

Perceba que no snippet acima, a classe `Comment` compõe a clase `Post`. É quase como a relação do banco de dados `has many`.

Para lidar com datas, pode-se usar o `SimpleDateFormat`. Dá pra formatar a data.

`StringBuilder` é muito útil para criar strings grandes com diversas variáveis.

Herança é uma associação entre classes, não entre objetos. Enquanto na composição você terá dois objetos diferentes associados, na herança você tem duas classes associadas, mas apenas um objeto com todos os membros das duas classes.

### Upcasting & Downcasting

**Upcasting**:

- Casting da subclasse para superclasse
- Geralmente usado em polimorfismo

```java
Account acc = new Account(1001, "Digzom", 0.0);
BusinessAccount bacc = new BusinessAccount(1002, "Amanda", 0.0, 600.0);

Account acc1 = bacc;
Account acc2 = new BusinessAccount(1003, "Ava", 0.0, 200.0);
Account acc3 = new AnotherAccountType(1004, "Lula", 0.0);
```

**Downcasting**:

- Casting da superclasse para subclasse
- Dá pra usar instanceof
- Usa-se muito em métodos que recebem parâmetros genéricos

```java
// compiler yells
BusinessAccount acc4 = acc2;

// compiler likes
BusinessAccount acc4 = (BusinessAccount) acc2;
```

Assim como no typescript, pode-se usar `intanceof` para saber a instância de uma classe e saber como tratá-la apropriadamente.

### Override

É legal usar o `@Override` porque o compilador pode fazer verificações acerca do método que está sendo sobreescrito. Pode ser que você erre uma letra ou não confunda o nome do método (ou argumentos). Com o `@Override` o compilador vai te avisar.

### Super

Com o `super` eu posso acessar métodos ou atributos. Ex.:

```java
@Override
public void withdraw(double amount) {
  super.withdraw(amount);
  balance -= 2.0
}
```

No snippet acima eu estou sobreescrevendo o método `withdraw`. Dentro do método eu chamo o `super.withdraw`, que corresponde ao método da superclasse. Depois de fazer o saque, eu diminuo o `balance` (saldo).

## Final

A palavra chave `final` usado em classe `public final class MyClass` evita que a classe seja herdada. A palavra sendo usada no método, evita que o método seja sobreescrito.

**Insight:** tenho a impressão de que em java os programas são mais entendidos como "building blocks" do que em outras linguagens pelas quais eu já passei. As coisas parecem sólidas.

### Porque?

- Segurança
  - Métodos sobrepostos e heranças mais "profundas" são bons candidatos à serem `final`, pois muitas sobreescritas e heranças podem gerar inconsistências e complexidade no código.
  - Pode ser uma regra de negócio também
- Performance
  - Atributos de tipo de uma classe final são analisados de forma mais rápida em tempo de execução

## Classes abstratas

- Não podem ser instanciadas
- Uma forma de garantir **herança total**: somente subclasses não abstratas podem ser instanciadas.

### Porque?

- Reuso

- Organiza os métodos e atributos de forma uniforme, sendo possível utilizar polimorfismo nas classes filhas
  - Por exemplo: se eu tenho uma classe abstrata `Account` e, herdando dela, tenho `SavingsAccount` e `BusinessAccount`, é possível criar um método que, por exemplo, totalize o saldo de todas as contas de todos os tipo através de uma classe abstrata com um método abstrato.

## Tratamento de Exceções

- Throw 
- Instanciação de classes de exceção
- Criação de exceções custumizadas
  - É uma boa prática dedicar um package para isso
  - As classes de exceções customizadas podem herdar de duas classes, geralmente: RuntimeException e Exception.

A classe `RuntimeException` é um tipo de exceção que o compilador **não** te obriga a tratar.

Às vezes ainda não dá pra saber quais são todos os tipos de erros que podem ser lançados em runtime, então é possível fazer upcasting para utilizar a classe `RuntimeError` no bloco catch para lançar uma mensagem de erro tratada, já que é uma classe mais genérica.

## Design Patterns

A ideia de padrões foi apresentada por Christopher Alexander, em 1977, no contexto da arquitetura e construção civil.

- Funciona como um "catálogo de soluções". Então um padrão encapsula uma solução que pode ser reutilizada e transmitida entre desenvolvedores de forma conceitual.
- Outras engenhenharias também possuem catálogos de soluções.
- Dando nomes para coisas, a gente consegue comunicar melhor uma ideia. Se eu falo para alguém sobre usar um padrão **Observer**, sem precisar explicar muita coisa, essa pessoa já saberá o que significa, quais conjuntos de classe e relacionamento nós teremos, quais características, etc.

### Estrutura de um padrão

- Todo padrão inclui:
  - Nome
  - Problema
  - Solução
  - Consequências/Forças

No livro GOF, temos uma estrutura parecida, apesar de diferente:

- Nome (inclui número da página)
- Objetivo/Intenção
- Também conhecido como
- Motivação
- Aplicabilidade
  - Como reconhecer as situações nas quais o padrão é aplicável
- Estrutura
  - Uma representação gráfica (como UML por exemplo)
- Participantes
- Colaborações
- Consequências
  - Vantagens e desvantagens
- Implementação
- Exemplo de código
- Usos conhecidos
  - Exemplos reais
- Padrões relacionados

### Tipos de padrão

- Padrões de Criação
- Padrões Estruturais
  - Organização para tornar tudo mais flexível
- Padrões comportamentais
  - A dinâmica do sistema

# Padrões de Projeto

## Strategy

- Objetivo: definir uma família de algoritmos, encapsular cada um deles em uma classe e torná-los intercambiáveis. Estratégia permite que o algoritmo varie independentemente dos clientes que o utilizam.
- É uma forma de extrair da classe algo que pode mudar.
- Usos conhecidos: verificação ortográfica multilíngue, separação silábica, highlight de documentos no Emacs, sistemas adaptativos, algoritmos de ordenação, conectores a bancos de dados, etc.

A estrutura básica é:

Um contexto (seu programa).

Seu programa precisa executar alguma coisa (um algoritmo, por exemplo).

Ao invés de sua classe principal (contexto) selecionar a estratégia, um método que implementa os algoritmos, a gente delega essa execução (através de um método, por exemplo) para uma outra classe, que é abstrata. As subclasses concretas é que executarão o código de sua própria forma. Essa "decisão" de por qual subclasse vai executar o código dependendo do parâmetro passado é feito em tempo de execução (Runtime).

O contexto pouco sabe sobre a estratégia. Ele apenas mantem a referncia para uma estratégia concreta.

Dessa forma os "algoritmos" tornam-se intercabiáveis. Pois em momentos diferentes podemos utilizar "comportamentos" diferentes. Além disso, é possível adicionar um novo algoritmo sempre que precisar.

Assim a gente evita ter uma classe muito grande para executar todas as possíveis branches, ou heranças muito profundas. Ao invés disso, preferimos delegar essas escolhas para uma outra classe diferente. 

Quando temos várias classes que diferem apenas na forma como elas executam algum comportamento, é um bom caso para se usar esse DP. Another cenario is when you want to isolate the business logic of a classe from the implementation details.

**"Exemplo do pato"**

Criamos uma classe `Duck`. Esta classe tem 3 classes subclasses herdeiras: `MallardDuck`, `DecoyDuck` e `RubberDuck`.

Se implementarmos, na superclasse, um método `fly`, teremos um "bug" no sistema, pois `RubberDuck` (pato de borracha) não deve voar. Acidentalmente, um desenvolvedor pode acabar utilizando esse método da superclasse para fazer todos os patos voarem e ocasionar essa inconsistência.

Usando stragegy a gente criaria um método chamado `setFlyBehavior`, que apontaria para um método da classe abstrata `FlyBehavior`. Herdando dessa classe, teríamos, por exemplo, as classes `FlyWithWings` e `FlyNoWay`. Cada uma dessas classes implementaria o método `fly` de acordo com sua necessidade.

Outro método criado na superclasse seria o `performFly`, que executaria de fato o vôo.

Então, ao criar um `RubberDuck rb = new RubberDuck`, no meu construtor, eu preciso passar um `FlyNoWay doNotFly.fly()`, e essa característica será "plugada" no meu `rb`. Algo assim:

```java
RubberDuck rb = new RubberDuck();
FlyBehavior fb = new FlyNoWay();
rb.setFlyBehavior(fb);
rb.performFly();
```

No snippet acima eu não adicionei o comportamento de vôo já no construtor para ficar mais explícito, mas provavelmente seria o mais indicado nesse contexto.

## Padrão Adapter

É quando, ao precisar de um método de uma api ou biblioteca externa, e nossa classe não tem compatibilidade com esse método, nós criamos um método próprio, numa classe Adapter, que aponta para o método externo a fim de fazer modificações no método da api/biblioteca externa de forma que a funcionalidade possa ser usada na nossa classe principal.

Ex.: 

- Mudar o nome do método;
- Mudar número de parâmetros ou tipo dos métodos;
- Mudar ordem dos argumentos;

Classe de adaptação não faz muita coisa, possui apenas métodos bem curtos que delegam a execução para o objeto adaptado.

Snippet1: 

```java
class Matematica {
  static double logaritmoE (double x) {
    // muda o nome
    return Math.log(x);
  }

  static double logaritmo_rule(double x) {
    // muda o nome e a implementação
    return Math.log(x) / Math.log(2);
  }

  static double logaritmo(double x, base b) {
    // muda o nome e a implementação
    return Math.log(x) / Math.log(b);
  }
}
```







