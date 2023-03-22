**Língua: > PT-BR | [EN](https://github.com/Ivi-SCD/GoF-DesignPatterns/blob/main/README-EN.md)**

## :bamboo: Guia Completo Sobre GoF Design Patterns :bamboo:
Neste repositório tratarei todos os padrões de projetos definidos no livro **[GoF (Gang of Four)](https://www.amazon.in/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8)**, também conhecido como "Design Patterns: Elements of Reusable Object-Oriented Software". Este livro voltado para a área de programação é essencial para todos os programadores, principalmente os que trabalham com o paradigma de orientação a objetos. Ele foi escrito por Erich Gamma, Richard Helm, Ralph Johnson e John Vlissides. O livro foi publicado em 1994 e desde então tem sido um dos principais recursos para entender os design patterns relacionados a orientação a objetos. Os autores do GoF apresentam um conjunto de **23 padrões de design** que são divididos em três categorias: **Padrões Criacionais, Padrões Estruturais e Padrões Comportamentais.**

Os design patterns são soluções para problemas comuns que surgem durante o desenvolvimento de software. Eles são técnicas comprovadas que podem ser usadas para resolver esses problemas de forma eficiente e eficaz. Cada design pattern é uma descrição completa de um problema específico e de uma solução geral que pode ser adaptada para atender a diferentes requisitos de projeto, em qualquer linguagem.

Sumário de todos os tipos de design patterns:
* **Padrões Criacionais**
  * [Singleton](#singleton)
  * [Factory Method](#factory)
  * [Abstract Factory](#afactory)
  * [Builder](#builder)
  * [Prototype](#prototype)
* **Padrões Estruturais**
  * Adapter
  * Bridge
  * Composite
  * Decorator
  * Facade
  * Flyweight
* **Padrões comportamentais**
  * Chain Of Responsability
  * Command
  * Iterator
  * Mediator
  * Memento
  * Observer
  * State
  * Strategy
  * Template Method
  * Visitor
  
Cada um desses padrões é explicado detalhadamente no livro GoF, juntamente com exemplos de código e diretrizes para sua implementação, este repositório tratará todos os principais pontos do livro, porém para entender e poder usufruir 100% do oferecido, recomendo fortemente a leitura do livro. Ao você estudar e entender esses padrões, poderá criar soluções de software mais flexíveis, reutilizáveis e fáceis de manter. Então vamos começar! Hands-On! Não se esqueça de marcar este repositório com uma :star: para poder sempre rever e estudar os design patterns sempre que precisar.

## Padrões Criacionais
### <a name="singleton"></a>Singleton

Singleton é um padrão criacional, ele garante que uma classe tenha **apenas uma instância** e forneça um ponto global de acesso a ela. Isso é útil quando precisamos por exemplo, de um objeto que coordene ações em todo o sistema, como um gerenciador de configurações ou um cache. O padrão Singleton garante que haja apenas uma instância desses objetos, evitando a necessidade de várias instâncias e, portanto, reduzindo o consumo de recursos do sistema.

A implementação básica do padrão Singleton consiste em **uma classe que possui um construtor privado e um método estático que retorna a única instância da classe**. O método estático **verifica se uma instância já foi criada e, se ainda não existir, cria uma nova instância.** A instância criada é então retornada para qualquer chamador que solicite a instância. 

Sei que com palavras fica um pouco difícil compreender e assimilar o assunto então aqui vai um exemplo de implementação do padrão Singleton em Java:

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Construtor privado para evitar instanciação externa
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    // Outros métodos da classe Singleton
}

```

No exemplo acima, a classe `Singleton` possui um construtor privado e um método estático `getInstance()` que retorna a única instância da classe. A instância é criada apenas quando o método `getInstance()` é chamado pela primeira vez e, a partir daí, a mesma instância é retornada em todas as chamadas subsequentes.

E a seguir, um exemplo de código que utiliza a classe `Singleton`:

```java
public class MyApp {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.println(s1 == s2); // true, as duas variáveis referenciam a mesma instância
    }
}

```

No exemplo acima, duas variáveis são criadas a partir da classe `Singleton` utilizando o método `getInstance()`. Como a classe `Singleton` garante que **apenas uma instância exista**, ambas as variáveis se referem à mesma instância. A saída do código será `true`, confirmando que ambas as variáveis se referem à mesma instância.

Em resumo, o padrão Singleton é útil quando precisamos garantir que **apenas uma instância de uma classe exista no sistema e quando precisamos fornecer um ponto global de acesso a essa instância**. Isso pode ser usado em vários casos, como gerenciadores de cache ou de configuração. A implementação do padrão Singleton consiste em uma classe com um construtor privado e um método estático que retorna a única instância da classe, criando-a apenas quando necessário.

##

### <a name="factory"></a>Factory Method

O Factory Method é design pattern criacional que **fornece uma interface para criação de objetos em uma classe**, mas permite que as subclasses decidam qual classe instanciar. O problema que esse padrão resolve é permitir que uma classe delegue a criação de objetos para suas subclasses, evitando a necessidade de que a classe principal conheça antecipadamente as classes concretas que serão criadas.

Um exemplo de aplicação do Factory Method pode ser encontrado em uma aplicação de processamento de pedidos de venda em uma loja virtual. Suponha que a loja tenha vários tipos de pedidos, como Pedido Nacional, Pedido Internacional, Pedido Expresso, entre outros. Cada tipo de pedido requer um tratamento específico e pode ter atributos e comportamentos diferentes.

Para resolver esse problema, podemos utilizar o Factory Method para que a classe Pedido possa ser criada por suas subclasses de acordo com as necessidades específicas de cada tipo de pedido. Dessa forma, a classe principal não precisa conhecer antecipadamente as classes concretas que serão criadas, mas delega essa responsabilidade às subclasses.

```java
public abstract class Pedido {
    protected double valor;
    protected String endereco;

    public Pedido(double valor, String endereco) {
        this.valor = valor;
        this.endereco = endereco;
    }

    public abstract double calcularFrete();

    // Outros métodos da classe Pedido
}

public class PedidoNacional extends Pedido {
    public PedidoNacional(double valor, String endereco) {
        super(valor, endereco);
    }

    public double calcularFrete() {
        return valor * 0.1;
    }

    // Outros métodos da classe PedidoNacional
}

public class PedidoInternacional extends Pedido {
    public PedidoInternacional(double valor, String endereco) {
        super(valor, endereco);
    }

    public double calcularFrete() {
        return valor * 0.2;
    }

    // Outros métodos da classe PedidoInternacional
}

public interface FabricaPedidos {
    public Pedido criarPedido(double valor, String endereco);
}

public class FabricaPedidoNacional implements FabricaPedidos {
    public Pedido criarPedido(double valor, String endereco) {
        return new PedidoNacional(valor, endereco);
    }
}

public class FabricaPedidoInternacional implements FabricaPedidos {
    public Pedido criarPedido(double valor, String endereco) {
        return new PedidoInternacional(valor, endereco);
    }
}

public class LojaVirtual {
    private FabricaPedidos fabrica;

    public LojaVirtual(FabricaPedidos fabrica) {
        this.fabrica = fabrica;
    }

    public Pedido criarPedido(double valor, String endereco) {
        return fabrica.criarPedido(valor, endereco);
    }
}

```

O exemplo acima talvez tenha assustado um pouco mas é relativamente simples de entender, basicamente a classe Pedido é uma classe abstrata que define a interface para as criações de pedidos e ela também possui um método abstrato `calcularFrete()`. As subclasses `PedidoNacional` e `PedidoInternacional` implementam essa interface e implementam seu próprio comportamento de cálculo do frete.

As classes `FabricaPedidos`, `FabricaPedidoNacional` e `FabricaPedidoInternacional` implementam o `Factory Method`, fornecendo uma interface para a criação de objetos Pedido. A classe `LojaVirtual` é responsável por criar um objeto Pedido de acordo com o tipo específico de pedido.

A seguir, um exemplo de código que utiliza o `Factory Method`:

```java
public class Main {
    public static void main(String[] args) {
        // Implementando as fábricas
        FabricaPedidos fabricaNacional = new FabricaPedidoNacional();
        FabricaPedidos fabricaInternacional = new FabricaPedidoInternacional();
        
        // Criando um objeto LojaVirtual e atribuindo no seu construtor a fabricaNacional
        LojaVirtual loja = new LojaVirtual(fabricaNacional);
        
        //Realizando o pedido nacional
        Pedido pedidoNacional = loja.criarPedido(1000, "Rua A, 123");
        
        
        //Seguindo a mesma lógica, agora com a fabricaInternacional e o pedidoInternacional
        loja = new LojaVirtual(fabricaInternacional);
        Pedido pedidoInternacional = loja.criarPedido(2000, "Av. B, 456");

        System.out.println("Valor do frete do pedido nacional: " + pedidoNacional.calcularFrete());
        System.out.println("Valor do frete do pedido internacional: " + pedidoInternacional.calcularFrete());

    }
}
```

No exemplo acima, a classe `Main` cria duas fábricas, uma para `PedidoNacional` e outra para `PedidoInternacional`. Em seguida, a LojaVirtual é instanciada com a fábrica de pedidos nacionais e um pedido nacional é criado. 

O método `calcularFrete()` de cada objeto Pedido é chamado, mostrando o valor do frete calculado de acordo com a implementação de cada classe concreta.

##

### <a name="afactory"></a> Abstract Factory
O Abstract Factory é um design pattern bastante similar ao Factory Method. Ele **fornece uma interface para criar famílias de objetos relacionados ou dependentes**, sem especificar suas classes concretas. Em outras palavras, ele permite que você **crie objetos que compartilham uma mesma temática**, como objetos de diferentes tipos, mas que possuem alguma relação entre si. Complicado de entender mas você vai compreender melhor com os exemplos.

Um bom exemplo de aplicação do Abstract Factory é um sistema de gerenciamento de veículos, nele há dois tipos de veículos: carros e motos. Cada tipo de veículo tem suas próprias características, como motor, rodas, modelo, etc. E para cada tipo de veículo, pode haver diferentes marcas e modelos. O Abstract Factory pode ser usado para criar objetos relacionados entre si, como um carro de determinada marca e modelo, ou uma moto de determinada marca e modelo.

A seguir, um exemplo de código que utiliza o Abstract Factory:

```java
public interface FabricaVeiculo {
   Carro criarCarro();
   Moto criarMoto();
}

public class FabricaFiat implements FabricaVeiculo {
   public Carro criarCarro() {
      return new Palio();
   }
   public Moto criarMoto() {
      return new Ducati();
   }
}

public class FabricaChevrolet implements FabricaVeiculo {
   public Carro criarCarro() {
      return new Onix();
   }
   public Moto criarMoto() {
      return new HarleyDavidson();
   }
}

public class LojaVeiculos {
   private FabricaVeiculo fabricaVeiculo;
   
   public LojaVeiculos(FabricaVeiculo fabricaVeiculo) {
      this.fabricaVeiculo = fabricaVeiculo;
   }
   
   public Carro criarCarro() {
      return fabricaVeiculo.criarCarro();
   }
   
   public Moto criarMoto() {
      return fabricaVeiculo.criarMoto();
   }
}

public class Main {
   public static void main(String[] args) {
      FabricaVeiculo fabricaFiat = new FabricaFiat();
      FabricaVeiculo fabricaChevrolet = new FabricaChevrolet();
      
      LojaVeiculos lojaFiat = new LojaVeiculos(fabricaFiat);
      LojaVeiculos lojaChevrolet = new LojaVeiculos(fabricaChevrolet);
      
      Carro palio = lojaFiat.criarCarro();
      Moto ducati = lojaFiat.criarMoto();
      
      Carro onix = lojaChevrolet.criarCarro();
      Moto harleyDavidson = lojaChevrolet.criarMoto();
   }
}

```

Nesse exemplo, há uma interface `FabricaVeiculo` que define os métodos para criar carros e motos. As classes `FabricaFiat` e `FabricaChevrolet` implementam essa interface e fornecem implementações concretas para criar carros e motos da Fiat e Chevrolet, respectivamente. A classe `LojaVeiculos` usa a fábrica de veículos para criar carros e motos de diferentes marcas e modelos. Por fim, a classe `Main` mostra como criar objetos Carro e Moto usando diferentes fábricas de veículos.

Esse padrão resolve o problema de criar objetos relacionados entre si sem especificar suas classes concretas, permitindo que sejam criados objetos de diferentes tipos, mas que possuem alguma relação entre si.

Ok, compreendido, mas qual é a diferença entre o Abstract Factory do Factory?
Basicamente, a diferença fundamental entre o padrão Abstract Factory e o padrão Factory Method é que o Abstract Factory é usado para criar **famílias de objetos relacionados ou dependentes**, enquanto o Factory Method é usado para criar **objetos individuais**.

Resumindo, enquanto o Factory Method cria um objeto único, o Abstract Factory cria uma família inteira de objetos relacionados.

##

### <a name="builder"></a> Builder

O padrão Builder é mais um dos padrões criacionais. Ele **separa a construção de um objeto complexo da sua representação**, permitindo que o mesmo processo de construção possa criar diferentes representações.

Em outras palavras, o Builder **permite a construção passo a passo de um objeto complexo**, sem expor a complexidade do processo de construção ao cliente final.

Suponha que queremos criar uma classe `Carro` com os seguintes atributos: `marca`, `modelo`, `ano de fabricação`, `número de portas`, `cor` e `motorização`. Além disso, queremos que a criação do carro seja feita passo a passo, ou seja, primeiro definimos a marca e o modelo, depois o ano, depois o número de portas, e assim por diante.

Usando o padrão Builder, podemos simplificar a criação de objetos dessa classe, permitindo que os atributos sejam definidos em etapas separadas, de acordo com o cliente.

Segue o exemplo:

```java
public class Carro {
    private String marca;
    private String modelo;
    private int anoFabricacao;
    private int numPortas;
    private String cor;
    private String motorizacao;

    public Carro() {}

    public Carro(String marca, String modelo, int anoFabricacao, int numPortas, String cor, String motorizacao) {
        this.marca = marca;
        this.modelo = modelo;
        this.anoFabricacao = anoFabricacao;
        this.numPortas = numPortas;
        this.cor = cor;
        this.motorizacao = motorizacao;
    }

    // getters e setters
}
```

Agora, criamos uma classe Builder que nos permitirá criar o carro passo a passo:
```java
public class CarroBuilder {
    private String marca;
    private String modelo;
    private int anoFabricacao;
    private int numPortas;
    private String cor;
    private String motorizacao;

    public CarroBuilder() {}

    public CarroBuilder comMarca(String marca) {
        this.marca = marca;
        return this;
    }

    public CarroBuilder comModelo(String modelo) {
        this.modelo = modelo;
        return this;
    }

    public CarroBuilder comAnoFabricacao(int anoFabricacao) {
        this.anoFabricacao = anoFabricacao;
        return this;
    }

    public CarroBuilder comNumPortas(int numPortas) {
        this.numPortas = numPortas;
        return this;
    }

    public CarroBuilder comCor(String cor) {
        this.cor = cor;
        return this;
    }

    public CarroBuilder comMotorizacao(String motorizacao) {
        this.motorizacao = motorizacao;
        return this;
    }

    public Carro build() {
        return new Carro(marca, modelo, anoFabricacao, numPortas, cor, motorizacao);
    }
}
```
Observe que o `Builder` tem os mesmos atributos que a classe `Carro`, mas também tem métodos para definir cada um desses atributos passo a passo. Cada um desses métodos retorna o próprio Builder (this), permitindo que possamos encadear as chamadas de método em uma única linha.

Finalmente, podemos usar o Builder para criar um carro passo a passo:

```java
Carro carro = new CarroBuilder()
        .comMarca("Ford")
        .comModelo("Mustang")
        .comAnoFabricacao(2022)
        .comNumPortas(2)
        .comCor("vermelho")
        .comMotorizacao("V8")
        .build();
```

Observe como cada chamada de método do Builder define um atributo do carro. Quando chamamos o método `build()` no final, o Builder cria e retorna um objeto Carro completo com todos os atributos e características que nós passamos, tornando a instanciação do objeto um processo simples e flexível.

##
### Prototype

O design pattern Prototype tem como objetivo permitir a criação de novos objetos a partir da **clonagem de objetos existentes**, sem que seja necessário conhecimento detalhado da sua implementação. Em outras palavras, **ele permite a criação de novos objetos a partir de um modelo existente**.

O padrão Prototype é útil em situações onde a criação de um objeto é muito cara ou complexa, ou quando a criação de um objeto requer a configuração de muitos parâmetros. Ao invés de criar um novo objeto toda vez que ele é necessário, o padrão Prototype **permite a clonagem do objeto existente, tornando o processo de criação muito mais eficiente**.

Em termos de implementação, o padrão Prototype define uma interface `Cloneable`, que permite que um objeto seja clonado. Esse objeto deve implementar o método `clone()`, que faz uma cópia do objeto e retorna uma referência para o novo objeto clonado.

Um exemplo real de uso do padrão Prototype em Java é na criação de documentos. Suponha que uma aplicação precise criar documentos com diferentes layouts e estilos. Em vez de criar um novo objeto para cada documento, podemos criar um modelo inicial e cloná-lo para criar novos documentos com as mesmas características.

Aqui está um exemplo de implementação em Java:

```java
public abstract class Documento implements Cloneable {
 
    private String conteudo;
 
    public Documento(String conteudo) {
        this.conteudo = conteudo;
    }
 
    public abstract Documento clone();
 
    public String getConteudo() {
        return conteudo;
    }
 
    public void setConteudo(String conteudo) {
        this.conteudo = conteudo;
    }
 
}
```

Nesse exemplo, a classe abstrata `Documento` define o modelo inicial para todos os documentos. Ela implementa a interface `Cloneable` e define um método `clone` abstrato, que será implementado pelas subclasses concretas.

Aqui está um exemplo de uma classe concreta que implementa a clonagem de objetos:

```java
public class DocumentoPadrao extends Documento {
 
    public DocumentoPadrao(String conteudo) {
        super(conteudo);
    }
 
    public Documento clone() {
        return new DocumentoPadrao(getConteudo());
    }
 
}
```

Nesse exemplo, a classe `DocumentoPadrao` extende a classe Documento e implementa o método `clone`. Esse método cria uma nova instância de `DocumentoPadrao` e retorna uma referência para ela.

Com a implementação do padrão `Prototype`, podemos criar diferentes tipos de documentos com diferentes layouts e estilos a partir de um modelo inicial, tornando o processo de criação de novos documentos muito mais eficiente e simplificado.

##

## Padrões Estruturais [Building... :construction_worker:]
