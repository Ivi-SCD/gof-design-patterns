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
  * [Adapter](#adapter)
  * [Bridge](#bridge)
  * [Composite](#composite)
  * [Decorator](#decorator)
  * [Facade](#facade)
  * [Flyweight](#flyweight)
  * [Proxy](#proxy)
* **Padrões comportamentais**
  * [Chain Of Responsability](#cor)
  * [Command](#command)
  * [Iterator](#iterator)
  * [Mediator](#mediator)
  * [Memento](#memento)
  * [Observer](#observer)
  * [State](#state)
  * [Strategy](#strategy)
  * [Template Method](#tm)
  * [Visitor](#visitor)
  * [Interpreter](#interpreter)
  
Cada um desses padrões é explicado detalhadamente no livro GoF, juntamente com exemplos de código e diretrizes para sua implementação, este repositório tratará todos os principais pontos do livro, porém para entender e poder usufruir 100% do oferecido, recomendo fortemente a leitura do livro. Ao você estudar e entender esses padrões, poderá criar soluções de software mais flexíveis, reutilizáveis e fáceis de manter. Então vamos começar! Hands-On! Não se esqueça de marcar este repositório com uma :star: para poder sempre rever e estudar os design patterns sempre que precisar.

## Padrões Criacionais
> Eles lidam com o processo de criação de objetos e como eles são criados, gerenciados e implementados. Eles fornecem maneiras de criar objetos sem expor a lógica de criação ao cliente, permitindo maior flexibilidade na criação de objetos.

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

## Padrões Estruturais
> Estes padrões se concentram na composição de classes e objetos para formar estruturas maiores e mais complexas. Eles ajudam a organizar e simplificar o código, tornando-o mais fácil de entender e manter.

### <a name="adapter"></a> Adapter
O padrão Adapter é um design pattern estrutural que permite que **duas classes com interfaces incompatíveis possam trabalhar juntas**. Ele **converte a interface de uma classe em outra interface** que o cliente espera. Isso permite que objetos com interfaces diferentes trabalhem juntos, sem que o cliente precise modificar o código da classe original.

O padrão Adapter é **útil quando temos uma classe existente que possui a funcionalidade necessária, mas sua interface não é compatível com a interface do cliente**. Em vez de modificar a classe original, podemos criar uma classe adaptadora que implementa a interface necessária e delega as chamadas para a classe original.

Em Java, o padrão Adapter é implementado por meio de uma classe adaptadora que implementa a interface desejada e contém uma instância da classe original. A classe adaptadora implementa os métodos da interface desejada e chama os métodos correspondentes na classe original.

A seguir teremos uma classe que fornece informações sobre o tempo, mas sua interface não é compatível com a interface que o cliente deseja usar. Em vez de modificar a classe original, podemos criar uma classe adaptadora que implementa a interface desejada e chama os métodos correspondentes na classe original.

Segue o exemplo:
```java
// Interface do cliente
public interface TempoInfo {
    public double getTemperatura();
    public double getUmidade();
}

// Classe original com interface incompatível
public class Tempo {
    public float getTemp() {
        // código para obter a temperatura
    }

    public float getUmi() {
        // código para obter a umidade
    }
}

// Classe adaptadora
public class TempoAdapter implements TempoInfo {
    private Tempo tempo;

    public TempoAdapter(Tempo tempo) {
        this.tempo = tempo;
    }

    public double getTemperatura() {
        return tempo.getTemp();
    }

    public double getUmidade() {
        return tempo.getUmi();
    }
}

```

Nesse exemplo, a classe `Tempo` fornece informações sobre o tempo, mas sua interface não é compatível com a interface do cliente. A classe `TempoAdapter` implementa a interface `TempoInfo` e contém uma instância da classe `Tempo`. A classe `TempoAdapter` implementa os métodos da interface `TempoInfo` e chama os métodos correspondentes na classe `Tempo`.

Com o padrão Adapter, o cliente pode usar a classe `TempoAdapter` para obter informações sobre o tempo, sem precisar modificar a classe original `Tempo`. Isso permite que objetos com interfaces diferentes trabalhem juntos, sem que o cliente precise modificar o código da classe original.

##

### <a name="bridge"></a> Bridge
O padrão Bridge é um design pattern estrutural que separa uma abstração da sua implementação, permitindo que ambas possam variar independentemente. Isso é útil quando temos várias variações de abstrações e implementações, e queremos evitar uma explosão de subclasses.

Em Java, o padrão Bridge pode ser implementado através de uma classe abstrata que representa a abstração e uma interface que representa a implementação. A classe abstrata tem uma referência para a interface e delega a chamada dos métodos para a implementação.

Veja um exemplo real do padrão Bridge em Java:

Suponha que temos uma aplicação de desenho que permite ao usuário desenhar diferentes formas, como retângulos, círculos e triângulos. Para cada forma, temos diferentes variações de cores e estilos de desenho. Para evitar uma explosão de subclasses para cada combinação de forma e estilo, podemos usar o padrão Bridge.

```java
// Interface de implementação
public interface DrawingAPI {
    public void drawShape(int x, int y, int width, int height);
}

// Implementação A
public class DrawingAPIA implements DrawingAPI {
    public void drawShape(int x, int y, int width, int height) {
        // desenha a forma usando a implementação A
    }
}

// Implementação B
public class DrawingAPIB implements DrawingAPI {
    public void drawShape(int x, int y, int width, int height) {
        // desenha a forma usando a implementação B
    }
}

// Abstração
public abstract class Shape {
    protected DrawingAPI drawingAPI;

    public Shape(DrawingAPI drawingAPI) {
        this.drawingAPI = drawingAPI;
    }

    public abstract void draw();
}

// Abstração refinada
public class Rectangle extends Shape {
    private int x, y, width, height;

    public Rectangle(int x, int y, int width, int height, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }

    public void draw() {
        drawingAPI.drawShape(x, y, width, height);
    }
}

// Abstração refinada
public class Circle extends Shape {
    private int x, y, radius;

    public Circle(int x, int y, int radius, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    public void draw() {
        drawingAPI.drawShape(x, y, radius, radius);
    }
}
```

Nesse exemplo, a interface `DrawingAPI` representa a implementação de como desenhar as formas. As classes `DrawingAPIA` e `DrawingAPIB` são implementações diferentes da interface `DrawingAPI`.

A classe abstrata `Shape` representa a abstração de uma forma genérica. Ela tem uma referência para a interface `DrawingAPI` e delega a chamada do método `draw()` para a implementação. As classes `Rectangle` e `Circle` são variações refinadas da abstração `Shape`, cada uma com seus próprios parâmetros e comportamentos específicos.

Com o padrão Bridge, podemos adicionar novas formas ou implementações sem precisar criar uma nova classe para cada combinação de forma e estilo. Isso simplifica o código e torna a manutenção mais fácil.

##

### <a name="composite"></a> Composite
O padrão Composite é um padrão de design estrutural que permite compor objetos em estruturas de árvore para representar hierarquias de objetos. Ele permite que os clientes tratem objetos individuais e coleções de objetos de maneira uniforme.

Em Java, o padrão Composite pode ser implementado usando uma interface ou classe abstrata que representa o componente base e uma classe que representa o componente composto. O componente base pode ter métodos que são implementados tanto pelos componentes simples quanto pelos componentes compostos. O componente composto mantém uma lista de seus componentes filhos e implementa os métodos que trabalham com a lista de filhos.

Aqui está um exemplo real do padrão Composite em Java:

Suponha que temos uma hierarquia de componentes para construir um menu de um aplicativo. O menu pode ser composto por vários itens de menu, incluindo menus suspensos e itens de menu regulares. Cada item de menu pode ter um rótulo, um ícone e uma ação associada a ele. Podemos usar o padrão Composite para criar uma estrutura de árvore para representar o menu.

```java
// Componente base
public interface MenuComponent {
    public void add(MenuComponent menuComponent);
    public void remove(MenuComponent menuComponent);
    public MenuComponent getChild(int i);
    public String getName();
    public String getDescription();
    public void print();
}

// Componente folha
public class MenuItem implements MenuComponent {
    private String name;
    private String description;
    private boolean vegetarian;
    private double price;

    public MenuItem(String name, String description, boolean vegetarian, double price) {
        this.name = name;
        this.description = description;
        this.vegetarian = vegetarian;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public String getDescription() {
        return description;
    }

    public boolean isVegetarian() {
        return vegetarian;
    }

    public double getPrice() {
        return price;
    }

    public void print() {
        System.out.print("  " + getName());
        if (isVegetarian()) {
            System.out.print("(v)");
        }
        System.out.println(", " + getPrice());
        System.out.println("     -- " + getDescription());
    }

    public void add(MenuComponent menuComponent) {
        throw new UnsupportedOperationException();
    }

    public void remove(MenuComponent menuComponent) {
        throw new UnsupportedOperationException();
    }

    public MenuComponent getChild(int i) {
        throw new UnsupportedOperationException();
    }
}

// Componente composto
public class Menu implements MenuComponent {
    private List<MenuComponent> menuComponents = new ArrayList<>();
    private String name;
    private String description;

    public Menu(String name, String description) {
        this.name = name;
        this.description = description;
    }

    public void add(MenuComponent menuComponent) {
        menuComponents.add(menuComponent);
    }

    public void remove(MenuComponent menuComponent) {
        menuComponents.remove(menuComponent);
    }

    public MenuComponent getChild(int i) {
        return menuComponents.get(i);
    }

    public String getName() {
        return name;
    }

    public String getDescription() {
        return description;
    }

    public void print() {
        System.out.print("\n" + getName());
        System.out.println(", " + getDescription());
        System.out.println("---------------------");

        for (MenuComponent menuComponent : menuComponents) {
            menuComponent.print();
        }
    }
}
```

Neste exemplo, a interface `MenuComponent` é o componente base, que define os métodos que são implementados tanto pelos componentes simples quanto pelos componentes compostos. A classe `MenuItem` é um componente folha, que representa um item de menu regular. Ele implementa apenas os métodos que são relevantes para um item de menu. A classe `Menu` é um componente composto, que representa um menu suspenso. Ele mantém uma lista de seus componentes filhos (que podem ser itens de menu regulares ou outros menus suspensos).

##

### <a name="decorator"></a> Decorator
O padrão de projeto Decorator é um padrão estrutural que permite **adicionar comportamentos e funcionalidades a um objeto dinamicamente, sem precisar alterar a sua estrutura ou código**. Esse padrão é muito útil quando precisamos adicionar funcionalidades a objetos que já foram criados ou para os quais não temos acesso ao código-fonte.

O padrão Decorator é **composto por quatro elementos principais: o componente abstrato, o componente concreto, o decorador abstrato e o decorador concreto**. O componente abstrato define a interface para objetos que podem ter responsabilidades adicionais acrescentadas a eles. O componente concreto implementa a interface do componente abstrato e define o objeto ao qual as responsabilidades adicionais serão acrescentadas. O decorador abstrato define a interface para os decoradores concretos e possui uma referência para um objeto do componente abstrato. O decorador concreto acrescenta responsabilidades ao componente.

Um exemplo de uso do padrão Decorator em Java seria a implementação de um sistema de café que permite personalizar a bebida adicionando ingredientes extras, como leite, chantilly, caramelo, etc. invés de criar uma classe separada para cada combinação possível de café com ingredientes adicionais, podemos utilizar o padrão Decorator para adicionar dinamicamente os ingredientes desejados.

```java
// Component interface
public interface Beverage {
    String getDescription();
    double getCost();
}

// Concrete component
public class Espresso implements Beverage {
    public String getDescription() {
        return "Espresso";
    }

    public double getCost() {
        return 1.99;
    }
}

// Decorator abstract class
public abstract class CondimentDecorator implements Beverage {
    protected Beverage beverage;

    public CondimentDecorator(Beverage beverage) {
        this.beverage = beverage;
    }

    public abstract String getDescription();
}

// Concrete decorator classes
public class Milk extends CondimentDecorator {
    public Milk(Beverage beverage) {
        super(beverage);
    }

    public String getDescription() {
        return beverage.getDescription() + ", Milk";
    }

    public double getCost() {
        return beverage.getCost() + 0.10;
    }
}

public class Caramel extends CondimentDecorator {
    public Caramel(Beverage beverage) {
        super(beverage);
    }

    public String getDescription() {
        return beverage.getDescription() + ", Caramel";
    }

    public double getCost() {
        return beverage.getCost() + 0.20;
    }
}

// Client code
public class Cafe {
    public static void main(String[] args) {
        Beverage espresso = new Espresso();
        System.out.println(espresso.getDescription() + " $" + espresso.getCost());

        Beverage espressoWithMilk = new Milk(espresso);
        System.out.println(espressoWithMilk.getDescription() + " $" + espressoWithMilk.getCost());

        Beverage espressoWithCaramel = new Caramel(espresso);
        System.out.println(espressoWithCaramel.getDescription() + " $" + espressoWithCaramel.getCost());

        Beverage espressoWithMilkAndCaramel = new Caramel(new Milk(espresso));
        System.out.println(espressoWithMilkAndCaramel.getDescription() + " $" + espressoWithMilkAndCaramel.getCost());
    }
}
```
Nesse exemplo, a interface `Beverage` é o componente base, e a classe `Espresso` é a implementação concreta desse componente. As classes `CondimentDecorator`, `Milk` e `Caramel` são os decoradores abstrato e concretos, respectivamente. A classe `CondimentDecorator` é uma classe abstrata que estende a interface `Beverage` e contém uma referência a outra instância de `Beverage`. As classes `Milk` e `Caramel` são decoradoras concretes que extendem do `CondimentDecorator` e referencia suas funcionalidades ao objeto original. O cliente pode criar diferentes combinações de café com diversos ingredientes apenas instanciando diferentes decoradores.

##

### <a name="facade"></a> Facade
O padrão Facade é um padrão de projeto estrutural que **fornece uma interface simplificada para um conjunto de classes mais complexas e difíceis de usar**. O objetivo do padrão Facade é fornecer uma camada de abstração que esconde a complexidade subjacente do sistema e fornece uma interface simples e fácil de usar para os clientes.

O padrão Facade é útil quando há um sistema complexo com muitas classes e interfaces e o cliente precisa interagir com várias partes dele. Em vez de o cliente ter que conhecer todos os detalhes de implementação do sistema, ele pode simplesmente usar a interface fornecida pela fachada.

O padrão Facade é **implementado criando uma classe que fornece uma interface simplificada** para o cliente, escondendo toda a complexidade do sistema subjacente. A fachada delega as chamadas de métodos para as classes do sistema e retorna os resultados de forma simples e fácil de usar para o cliente.

Para ilustrar o padrão Facade, vamos considerar um exemplo de um sistema bancário. O sistema bancário pode ter muitas classes e interfaces diferentes, como contas bancárias, cartões de crédito, empréstimos, etc. Em vez de o cliente ter que interagir diretamente com todas essas classes e interfaces, podemos fornecer uma fachada que simplifica a interação do cliente com o sistema bancário.

```java
// Facade class
public class BankSystem {
    private AccountService accountService;
    private CreditCardService creditCardService;
    private LoanService loanService;

    public BankSystem() {
        accountService = new AccountService();
        creditCardService = new CreditCardService();
        loanService = new LoanService();
    }

    public void createAccount(String customerName, String accountType) {
        accountService.createAccount(customerName, accountType);
    }

    public void applyForCreditCard(String customerName) {
        creditCardService.applyForCreditCard(customerName);
    }

    public void applyForLoan(String customerName, double amount) {
        loanService.applyForLoan(customerName, amount);
    }
}

// Account service class
public class AccountService {
    public void createAccount(String customerName, String accountType) {
        // Implementation details
    }
}

// Credit card service class
public class CreditCardService {
    public void applyForCreditCard(String customerName) {
        // Implementation details
    }
}

// Loan service class
public class LoanService {
    public void applyForLoan(String customerName, double amount) {
        // Implementation details
    }
}

// Client code
public class BankClient {
    public static void main(String[] args) {
        BankSystem bankSystem = new BankSystem();
        bankSystem.createAccount("John Doe", "Checking");
        bankSystem.applyForCreditCard("John Doe");
        bankSystem.applyForLoan("John Doe", 10000);
    }
}
```
Neste exemplo, a classe `BankSystem` é a fachada que fornece uma interface simplificada para o cliente interagir com o sistema bancário. A fachada delega as chamadas de métodos para as classes `AccountService`, `CreditCardService` e `LoanService`, que são as classes complexas do sistema bancário. O cliente interage apenas com a fachada, que esconde toda a complexidade do sistema subjacente.

O padrão Facade é muito útil quando se lida com sistemas complexos e difíceis de usar. Ele fornece uma camada de abstração que torna

##

### <a name="flyweight"></a> Flyweight

O padrão Flyweight é um padrão de design estrutural que tem como objetivo **minimizar o uso de memória compartilhando objetos que são usados repetidamente**. O padrão Flyweight é útil quando uma aplicação precisa lidar com um grande número de objetos similares, e o custo de criar e manter esses objetos individualmente é muito alto em termos de memória e desempenho.

O padrão Flyweight é implementado através da criação de objetos leves (flyweights) que **armazenam as propriedades comuns entre objetos similares e compartilham essas propriedades com outros objetos**. Os flyweights armazenam apenas as propriedades que são únicas para cada objeto, reduzindo significativamente a quantidade de memória necessária para armazenar objetos similares.

Para implementar o padrão Flyweight, é necessário separar as propriedades compartilhadas entre objetos similares e as propriedades que são únicas para cada objeto. As propriedades compartilhadas são armazenadas em um objeto flyweight, enquanto as propriedades únicas são armazenadas em um objeto contexto.

Para ilustrar o padrão Flyweight, vamos considerar um exemplo de uma aplicação que desenha formas geométricas, como círculos e quadrados. Em vez de criar um novo objeto para cada forma geométrica desenhada, podemos usar o padrão Flyweight para compartilhar objetos similares.

```java
// Flyweight interface
public interface Shape {
    void draw(int x, int y, int radius);
}

// Concrete flyweight class for circle
public class Circle implements Shape {
    private final String color;

    public Circle(String color) {
        this.color = color;
        System.out.println("Creating circle of color: " + color);
    }

    @Override
    public void draw(int x, int y, int radius) {
        System.out.println("Drawing circle of color: " + color + ", at x: " + x + ", y: " + y + ", radius: " + radius);
    }
}

// Flyweight factory class
public class ShapeFactory {
    private static final Map<String, Shape> circleMap = new HashMap<>();

    public static Shape getCircle(String color) {
        Shape circle = circleMap.get(color);

        if (circle == null) {
            circle = new Circle(color);
            circleMap.put(color, circle);
        }

        return circle;
    }
}

// Client code
public class FlyweightClient {
    private static final String[] colors = { "Red", "Green", "Blue" };

    public static void main(String[] args) {
        for (int i = 0; i < 20; i++) {
            Shape circle = ShapeFactory.getCircle(getRandomColor());
            circle.draw(getRandomX(), getRandomY(), getRandomRadius());
        }
    }

    private static String getRandomColor() {
        return colors[(int) (Math.random() * colors.length)];
    }

    private static int getRandomX() {
        return (int) (Math.random() * 100);
    }

    private static int getRandomY() {
        return (int) (Math.random() * 100);
    }

    private static int getRandomRadius() {
        return (int) (Math.random() * 50);
    }
}

```

Nesse exemplo, a interface `Shape` representa o flyweight, que é implementado pela classe `Circle`. A classe `Circle` armazena apenas a cor do círculo, que é uma propriedade compartilhada por todos os círculos.

A classe `ShapeFactory` é responsável por gerenciar os flyweights. Ela mantém um mapa de objetos Circle já criados e retorna um objeto existente se ele já foi criado antes ou cria um novo objeto `Circle` se ele ainda não existe.

O cliente utiliza a classe `ShapeFactory` para obter os objetos `Circle` e chamar o método `draw()`. Neste exemplo, são criados 20 objetos `Circle` com cores e posições aleatórias. Observe que as cores são compartilhadas entre vários objetos `Circle`.

Com o uso do padrão Flyweight, é possível reduzir significativamente a quantidade de memória necessária para armazenar objetos similares. No exemplo acima, em vez de criar 20 objetos `Circle` com cores diferentes, apenas 3 objetos `Circle` são criados, um para cada cor, e são compartilhados entre todos os círculos desenhados.

##

### <a name="proxy"></a> Proxy

O padrão Proxy é um padrão de projeto estrutural que permite que um objeto substituto atue como substituto para outro objeto. O objeto substituto age como um intermediário entre o cliente e o objeto real. O objetivo desse padrão é permitir que o objeto real seja acessado remotamente ou através de outros meios complexos.

O padrão Proxy é útil em situações em que o objeto real é caro para criar, levar muito tempo para responder ou está em um local remoto. Em vez de interagir diretamente com o objeto real, o cliente interage com o objeto substituto que fornece a mesma interface que o objeto real.

Vamos supor que você está trabalhando em um sistema de compartilhamento de arquivos. Você tem uma classe chamada "FileDownloader" que baixa arquivos da Internet. O download de arquivos grandes pode levar muito tempo e pode ocupar muito espaço em disco. Portanto, em vez de baixar o arquivo diretamente, você pode criar uma classe Proxy para baixar o arquivo sob demanda.

Aqui está o código Java para o padrão Proxy:

```java
public interface FileDownloader {
    void download(String url);
}

public class RealFileDownloader implements FileDownloader {
    public void download(String url) {
        // Real implementation of file download
    }
}

public class ProxyFileDownloader implements FileDownloader {
    private RealFileDownloader downloader;
    private String url;

    public void download(String url) {
        if (downloader == null) {
            downloader = new RealFileDownloader();
            this.url = url;
        }

        downloader.download(url);
    }
}
```

Nesse exemplo, a interface "FileDownloader" define um método "download" que baixa um arquivo a partir de uma URL. A classe "RealFileDownloader" implementa a interface "FileDownloader" e fornece a implementação real para o download de arquivos.

A classe "ProxyFileDownloader" também implementa a interface "FileDownloader", mas em vez de baixar o arquivo diretamente, ela cria uma instância de "RealFileDownloader" sob demanda e delega o download para ela.

##

## Padrões Comportamentais
> Estes padrões lidam com a comunicação entre objetos e como eles interagem e se comunicam entre si para executar uma tarefa. Eles ajudam a separar as responsabilidades entre objetos e tornam o código mais flexível e fácil de modificar.

### <a name="cor"></a> Chain of Responsability

O padrão Chain of Responsibility é um padrão comportamental que **permite que uma série de objetos (ou handlers) tratem uma solicitação**, sendo que cada objeto decide se irá tratar a solicitação ou se irá passá-la para o próximo objeto na cadeia. É como uma cadeia de montagem, onde cada etapa adiciona algum valor e depois passa o produto para a próxima etapa.

O padrão é composto por três elementos principais:

* Handler (Manipulador): Define uma interface comum para todos os objetos da cadeia. Este objeto tem a responsabilidade de manipular a solicitação e decidir se deve passá-la para o próximo objeto da cadeia ou não.

* ConcreteHandler (Manipulador Concreto): Implementa a interface do manipulador e manipula a solicitação. Se o objeto não puder lidar com a solicitação, ele passará a solicitação para o próximo objeto da cadeia.

* Client (Cliente): Inicia a solicitação para a cadeia de objetos.

Vamos supor que estamos construindo um sistema de validação de login para uma aplicação web em Java. Neste sistema, queremos garantir que a senha do usuário tenha pelo menos 8 caracteres, que contenha letras maiúsculas e minúsculas, e que tenha pelo menos um caractere especial.

Podemos utilizar o padrão Chain of Responsibility para implementar a validação da senha, onde cada validação será tratada por um handler diferente, e se uma validação falhar, a responsabilidade será passada para o próximo handler na cadeia.

A seguir, segue um exemplo de implementação:

```java
public abstract class ValidadorSenha {
    private ValidadorSenha proximoValidador;

    public ValidadorSenha(ValidadorSenha proximoValidador) {
        this.proximoValidador = proximoValidador;
    }

    public boolean validar(String senha) {
        if (this.realizarValidacao(senha)) {
            if (this.proximoValidador != null) {
                return this.proximoValidador.validar(senha);
            } else {
                return true;
            }
        } else {
            return false;
        }
    }

    protected abstract boolean realizarValidacao(String senha);
}

public class TamanhoSenhaValidador extends ValidadorSenha {
    public TamanhoSenhaValidador(ValidadorSenha proximoValidador) {
        super(proximoValidador);
    }

    protected boolean realizarValidacao(String senha) {
        return senha.length() >= 8;
    }
}

public class MaiusculaSenhaValidador extends ValidadorSenha {
    public MaiusculaSenhaValidador(ValidadorSenha proximoValidador) {
        super(proximoValidador);
    }

    protected boolean realizarValidacao(String senha) {
        return senha.matches(".*[A-Z].*");
    }
}

public class MinusculaSenhaValidador extends ValidadorSenha {
    public MinusculaSenhaValidador(ValidadorSenha proximoValidador) {
        super(proximoValidador);
    }

    protected boolean realizarValidacao(String senha) {
        return senha.matches(".*[a-z].*");
    }
}

public class CaractereEspecialSenhaValidador extends ValidadorSenha {
    public CaractereEspecialSenhaValidador(ValidadorSenha proximoValidador) {
        super(proximoValidador);
    }

    protected boolean realizarValidacao(String senha) {
        return senha.matches(".*[!@#$%^&*()_+\\-=\\[\\]{};':\"\\\\|,.<>\\/?].*");
    }
}
```


Neste exemplo, temos a classe abstrata `ValidadorSenha` que define a estrutura da cadeia de validação de senha. Cada handler de validação é implementado por uma classe concreta que herda de ValidadorSenha. Cada handler realiza uma validação específica na senha e chama o próximo handler na cadeia, caso a validação seja bem-sucedida.

A classe `Cliente` pode então criar uma instância de cada handler e configurar a cadeia de responsabilidade definindo o próximo handler para cada um. Em seguida, o cliente chama o método validar da instância do primeiro handler da cadeia, passando a senha a ser validada.

```java
public class Cliente {
    public static void main(String[] args) {
        ValidadorSenha tamanhoValidador = new TamanhoSenhaValidador(null);
        ValidadorSenha maiusculaValidador = new MaiusculaSenhaValidador(tamanhoValidador);
        ValidadorSenha minusculaValidador = new MinusculaSenhaValidador(maiusculaValidador);
        ValidadorSenha especialValidador = new CaractereEspecialSenhaValidador(minusculaValidador);
        
        String senha = "MinhaSenha123!";

        if (especialValidador.validar(senha)) {
            System.out.println("Senha válida!");
        } else {
            System.out.println("Senha inválida!");
        }
    }
 }
```


Neste exemplo, criamos instâncias de cada handler de validação e definimos o próximo handler para cada um. Em seguida, chamamos o método validar da instância do primeiro handler na cadeia (`CaractereEspecialSenhaValidador`) e passamos a senha a ser validada. Se a senha passar por todos os handlers sem problemas, a mensagem "Senha válida!" será exibida. Caso contrário, a mensagem "Senha inválida!" será exibida.

Com este exemplo, podemos ver como o padrão `Chain of Responsibility` pode ser útil para implementar uma cadeia de validação de senha de forma eficiente e escalável, permitindo que cada handler de validação tenha uma responsabilidade específica na validação da senha.

##

### <a name="command"></a> Command

O padrão Command é um padrão de design comportamental que é **usado para encapsular uma solicitação como um objeto**, permitindo que você parametrize clientes com diferentes solicitações, faça fila ou registre solicitações e suporte operações de desfazer. Em outras palavras, o padrão Command **ajuda a separar o objeto que emite uma solicitação do objeto que realmente executa a solicitação**.

Vamos supor que temos uma aplicação que pode executar várias tarefas, como salvar um arquivo, imprimir um documento, fechar um programa etc. Com o padrão Command, podemos encapsular cada tarefa como um objeto de comando, que pode ser executado mais tarde. Aqui está um exemplo simples de como o padrão Command pode ser implementado em Java:

```java
public interface Command {
    void execute();
}

public class SaveCommand implements Command {
    private Document document;

    public SaveCommand(Document document) {
        this.document = document;
    }

    @Override
    public void execute() {
        document.save();
    }
}

public class PrintCommand implements Command {
    private Document document;

    public PrintCommand(Document document) {
        this.document = document;
    }

    @Override
    public void execute() {
        document.print();
    }
}

public class Document {
    public void save() {
        // código para salvar o documento
    }

    public void print() {
        // código para imprimir o documento
    }
}

public class Application {
    private Command saveCommand;
    private Command printCommand;

    public Application(Command saveCommand, Command printCommand) {
        this.saveCommand = saveCommand;
        this.printCommand = printCommand;
    }

    public void saveDocument() {
        saveCommand.execute();
    }

    public void printDocument() {
        printCommand.execute();
    }
}
```

Neste exemplo, temos uma interface `Command` que define o método `execute()` que deve ser implementado por cada comando específico. Em seguida, temos duas classes de comando concretas, `SaveCommand` e `PrintCommand`, cada uma com uma referência ao objeto `Document` que será manipulado. A classe `Document` contém as operações reais de salvar e imprimir um documento.

Finalmente, temos a classe `Application`, que possui referências aos objetos de comando e fornece métodos para executá-los. Observe que a classe `Application` não precisa saber como cada comando é implementado, ela só precisa saber que cada comando implementa a interface `Command` e pode ser executado.

Assim, podemos criar uma instância de `Application` passando os objetos `SaveCommand` e `PrintCommand` como argumentos, e então chamar os métodos `saveDocument()` e `printDocument()` quando necessário.

```java
Document document = new Document();
Command saveCommand = new SaveCommand(document);
Command printCommand = new PrintCommand(document);
Application app = new Application(saveCommand, printCommand);

// salvar o documento
app.saveDocument();

// imprimir o documento
app.printDocument();
```

Observe que, se precisássemos adicionar uma nova operação, como fechar o documento, por exemplo, poderíamos criar uma nova classe de comando que implementa a interface `Command` e adicioná-la à classe `Application` sem afetar o código existente. Isso é possível graças ao encapsulamento fornecido pelo padrão Command.

##

### <a name="iterator"></a> Iterator

O padrão Iterator é um padrão de projeto de comportamental que **permite percorrer elementos de uma coleção de maneira sequencial sem expor sua estrutura interna**. Ele permite acessar os elementos de uma coleção sem se preocupar com a forma como a coleção é implementada ou armazenada. Em Java, o padrão Iterator é usado extensivamente nas coleções da API Java Collections Framework, como ArrayList, LinkedList e HashSet.

O padrão Iterator define duas interfaces principais: a interface Iterator e a interface Iterable. A interface Iterator é usada para iterar sobre os elementos de uma coleção, enquanto a interface Iterable é usada para obter um objeto Iterator para uma coleção. A classe que implementa a interface Iterable deve fornecer uma implementação do método iterator() que retorna um objeto Iterator para a coleção.

Aqui está um exemplo de como usar o padrão Iterator em Java:

```java
import java.util.ArrayList;
import java.util.Iterator;

public class IteratorExample {

    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        // Obtém um Iterator para a coleção de nomes
        Iterator<String> iterator = names.iterator();

        // Percorre a coleção usando o Iterator
        while (iterator.hasNext()) {
            String name = iterator.next();
            System.out.println(name);
        }
    }

}
```

Neste exemplo, criamos uma coleção de nomes usando a classe `ArrayList`. Em seguida, obtemos um objeto `Iterator` para a coleção usando o método `iterator()` da classe `ArrayList`. Em seguida, usamos um laço while para percorrer a coleção usando o `Iterator`. Dentro do laço `while`, usamos o método `hasNext()` para verificar se ainda existem elementos na coleção e o método `next()` para obter o próximo elemento.

Outro exemplo é o seguinte:

```java
import java.util.HashSet;
import java.util.Iterator;

public class IteratorExample {

    public static void main(String[] args) {
        HashSet<Integer> numbers = new HashSet<>();
        numbers.add(1);
        numbers.add(2);
        numbers.add(3);

        // Obtém um Iterator para a coleção de números
        Iterator<Integer> iterator = numbers.iterator();

        // Percorre a coleção usando o Iterator
        while (iterator.hasNext()) {
            Integer number = iterator.next();
            System.out.println(number);
        }
    }

}
```

Neste exemplo, criamos uma coleção de números usando a classe `HashSet`. Em seguida, obtemos um objeto `Iterator` para a coleção usando o método `iterator()` da classe `HashSet`. Em seguida, usamos um laço `while` para percorrer a coleção usando o `Iterator`. Dentro do laço `while`, usamos o método `hasNext()` para verificar se ainda existem elementos na coleção e o método `next()` para obter o próximo elemento.

O padrão Iterator é uma maneira eficiente e flexível de percorrer elementos de uma coleção em Java. Ele fornece uma abstração de alto nível que permite percorrer a coleção de maneira independente da implementação subjacente. Ele também fornece um mecanismo seguro para acessar elementos da coleção e protege a coleção contra modificações acidentais durante a iteração.

##

### <a name="mediator"></a> Mediator

O padrão Mediator é um padrão de projeto comportamental que **permite a comunicação entre diferentes objetos sem que eles conheçam diretamente uns aos outros**. Em vez disso, um objeto mediador é responsável por gerenciar a comunicação e as interações entre os objetos. Isso ajuda a desacoplar os objetos envolvidos e a simplificar sua interação, facilitando a manutenção e evolução do código.

Em Java, o padrão Mediator pode ser usado em diversas situações, como em sistemas de mensagens, sistemas de chat, jogos multiplayer, sistemas de automação residencial, entre outros. Vamos analisar um exemplo de sistema de chat para entender melhor como o padrão funciona.

Suponha que estamos desenvolvendo um sistema de chat em que várias pessoas podem conversar em uma mesma sala. Cada pessoa pode enviar e receber mensagens dos outros usuários da sala. Para implementar isso usando o padrão Mediator, podemos criar uma classe ChatRoom que atua como o mediador entre os diferentes usuários da sala.

Aqui está um exemplo de como usar o padrão Mediator em Java:

```java
import java.util.ArrayList;
import java.util.List;

public class ChatRoom {
    private List<User> users = new ArrayList<>();

    public void sendMessage(String message, User sender) {
        for (User user : users) {
            if (user != sender) {
                user.receiveMessage(message);
            }
        }
    }

    public void addUser(User user) {
        users.add(user);
    }
}

public class User {
    private String name;
    private ChatRoom chatRoom;

    public User(String name, ChatRoom chatRoom) {
        this.name = name;
        this.chatRoom = chatRoom;
    }

    public void sendMessage(String message) {
        chatRoom.sendMessage(message, this);
    }

    public void receiveMessage(String message) {
        System.out.println(name + " received message: " + message);
    }
}

public class ChatRoomExample {
    public static void main(String[] args) {
        ChatRoom chatRoom = new ChatRoom();

        User alice = new User("Alice", chatRoom);
        User bob = new User("Bob", chatRoom);
        User charlie = new User("Charlie", chatRoom);

        chatRoom.addUser(alice);
        chatRoom.addUser(bob);
        chatRoom.addUser(charlie);

        alice.sendMessage("Hello, everyone!");
        bob.sendMessage("Hi, Alice!");
        charlie.sendMessage("Hey, guys!");
    }
}
```

Neste exemplo, a classe `ChatRoom` atua como o mediador entre os diferentes usuários da sala. Ela possui uma lista de usuários que foram adicionados à sala e um método `sendMessage` que envia uma mensagem para todos os usuários, exceto para o remetente.

A classe `User` representa um usuário na sala de chat. Cada usuário possui um nome e uma referência à sala de chat em que está participando. Cada usuário também possui um método sendMessage que envia uma mensagem para a sala de chat usando o método `sendMessage` da classe `ChatRoom`. Quando um usuário recebe uma mensagem, o método `receiveMessage` é chamado para imprimir a mensagem na tela.

Finalmente, na classe `ChatRoomExample`, criamos uma sala de chat e adicionamos três usuários à sala. Em seguida, cada usuário envia uma mensagem para a sala de chat usando o método `sendMessage`.

O padrão Mediator é uma maneira eficiente de gerenciar a comunicação entre diferentes objetos em Java, ajudando a desacoplar os objetos envolvidos na comunicação. Ele é particularmente útil em cenários em que vários objetos precisam se comunicar uns com os outros de forma complexa e pode ser usado em vários tipos de aplicativos, desde aplicativos de chat até aplicativos empresariais complexos.

##

### <a name="memento"></a> Memento

O padrão Memento é um padrão de projeto comportamental que **permite que você salve e restaure o estado de um objeto sem violar o encapsulamento**. Isso é especialmente útil em situações em que você deseja permitir que um objeto retorne a um estado anterior sem expor sua estrutura interna.

Em Java, o padrão Memento **é comumente usado em aplicações em que o histórico de estados de um objeto é importante**, como editores de texto, jogos e aplicativos de desenho. Vamos analisar um exemplo de um editor de texto para entender melhor como o padrão funciona.

Suponha que estamos desenvolvendo um editor de texto que permite que o usuário digite e edite o conteúdo do documento. Além disso, o editor deve ser capaz de desfazer as alterações realizadas pelo usuário, retornando o conteúdo do documento a um estado anterior. Para implementar isso usando o padrão Memento, podemos criar uma classe Memento que atua como uma cápsula que armazena o estado anterior do objeto.

Aqui está um exemplo de como usar o padrão Memento em Java:

```java
public class TextEditor {
    private StringBuilder content = new StringBuilder();
    private Stack<TextEditorMemento> mementos = new Stack<>();

    public void append(String text) {
        mementos.push(saveMemento());
        content.append(text);
    }

    public void undo() {
        if (!mementos.isEmpty()) {
            restoreMemento(mementos.pop());
        }
    }

    private TextEditorMemento saveMemento() {
        return new TextEditorMemento(content.toString());
    }

    private void restoreMemento(TextEditorMemento memento) {
        content = new StringBuilder(memento.getState());
    }

    public String getContent() {
        return content.toString();
    }

    private class TextEditorMemento {
        private String state;

        public TextEditorMemento(String state) {
            this.state = state;
        }

        public String getState() {
            return state;
        }
    }
}

public class TextEditorExample {
    public static void main(String[] args) {
        TextEditor editor = new TextEditor();

        editor.append("Hello");
        editor.append(", World!");

        System.out.println(editor.getContent()); // Output: "Hello, World!"

        editor.undo();

        System.out.println(editor.getContent()); // Output: "Hello"
    }
}
```

Neste exemplo, a classe `TextEditor` representa o editor de texto em si. Ela possui um `StringBuilder` que armazena o conteúdo atual do documento e uma `Stack` que armazena os estados anteriores do documento. Os métodos `append` e `undo` são usados para adicionar texto ao documento e desfazer a última alteração, respectivamente.

A classe `TextEditorMemento` atua como a cápsula que armazena o estado anterior do documento. Ela possui um único atributo que representa o estado anterior do documento e um método `getState` para retornar o estado armazenado.

Ao chamar o método `append`, o editor de texto empurra um novo `TextEditorMemento` para a pilha de mementos e adiciona o texto ao `StringBuilder`. Quando o método undo é chamado, o editor de texto restaura o estado anterior do documento usando o `TextEditorMemento` mais recente na pilha de mementos.

Finalmente, na classe `TextEditorExample`, criamos um editor de texto, adicionamos duas linhas de texto ao documento e, em seguida, desfazemos a última ação usando o método undo. Em seguida, adicionamos mais uma linha de texto e desfazemos novamente. Ao final, imprimimos o documento atualizado para verificar que apenas a primeira e a terceira linhas permaneceram.

O padrão Memento é útil em situações em que é necessário salvar o estado de um objeto em um determinado ponto do tempo para que possa ser restaurado mais tarde, como em editores de texto, editores gráficos, jogos e aplicativos financeiros. Ele permite que o objeto mantenha seu encapsulamento, pois a lógica de armazenamento do estado é colocada em um objeto separado. Isso torna o código mais fácil de manter e evoluir.

##

### <a name="observer"></a> Observer 

O padrão Observer é um padrão de projeto comportamental que define uma relação de **um-para-muitos entre objetos, de modo que, quando um objeto muda de estado, todos os seus dependentes são notificados e atualizados automaticamente**.

O padrão Observer é composto por duas entidades principais: o sujeito (ou observável) e o observador. O sujeito é o objeto que contém o estado que pode mudar, enquanto o observador é o objeto que depende do estado do sujeito e precisa ser notificado quando ocorre uma mudança.

Em Java, o padrão `Observer` é frequentemente implementado usando a interface `Observer` e a classe `Observable`. A classe `Observable` representa o sujeito e a interface Observer representa o observador.

Aqui está um exemplo simples de como usar o padrão Observer em Java:

```java
import java.util.Observable;
import java.util.Observer;

public class WeatherStation extends Observable {
    private int temperature;
    private int humidity;

    public void setWeather(int temperature, int humidity) {
        this.temperature = temperature;
        this.humidity = humidity;

        setChanged();
        notifyObservers();
    }

    public int getTemperature() {
        return temperature;
    }

    public int getHumidity() {
        return humidity;
    }
}

public class PhoneDisplay implements Observer {
    private WeatherStation weatherStation;

    public PhoneDisplay(WeatherStation weatherStation) {
        this.weatherStation = weatherStation;
        weatherStation.addObserver(this);
    }

    public void update(Observable obs, Object arg) {
        if (obs instanceof WeatherStation) {
            WeatherStation weatherStation = (WeatherStation) obs;
            System.out.println("Temperatura: " + weatherStation.getTemperature() + "°C, Umidade: " + weatherStation.getHumidity() + "%");
        }
    }
}

public class WeatherStationExample {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();
        PhoneDisplay phoneDisplay = new PhoneDisplay(weatherStation);

        weatherStation.setWeather(25, 60); // Output: "Temperatura: 25°C, Umidade: 60%"
    }
}
```

Neste exemplo, a classe `WeatherStation` representa o sujeito e contém o estado que pode mudar, representado pela temperatura e umidade. Quando o método `setWeather` é chamado, o estado é atualizado e os métodos `setChanged` e `notifyObservers` são chamados. O método `setChanged` informa que o estado do objeto mudou e o método `notifyObservers` notifica todos os observadores registrados sobre a mudança.

A classe `PhoneDisplay` representa o observador e é notificada sobre a mudança de estado usando o método `update`. O método `update` é chamado automaticamente pelo sujeito sempre que ocorre uma mudança. Neste exemplo, o observador imprime a temperatura e umidade atual.

Por fim, na classe `WeatherStationExample`, criamos uma instância da classe `WeatherStation` e uma instância da classe `PhoneDisplay`. A instância de `PhoneDisplay` se registra como um observador da instância de `WeatherStation` usando o método `addObserver`. Em seguida, atualizamos a temperatura e umidade usando o método `setWeather` e observamos que a instância de `PhoneDisplay` é notificada automaticamente e imprime a temperatura e umidade atual.

Em resumo, o padrão Observer é útil para implementar a comunicação entre objetos de forma desacoplada, permitindo que um objeto seja notificado automaticamente quando ocorrer uma alteração em outro objeto, sem que haja acoplamento entre eles. Isso permite que um objeto seja alterado sem afetar outros objetos que dependem dele, tornando o código mais modular e flexível.

##

### <a name="state"></a> State

O padrão State é um padrão de projeto comportamental que permite que um objeto altere seu comportamento quando seu estado interno muda. Isso é alcançado por meio da separação do comportamento em classes separadas que representam cada estado possível do objeto.

O padrão State é composto por duas entidades principais: o contexto e o estado. O contexto é o objeto que contém o estado interno que pode mudar, enquanto o estado é a classe que representa cada estado possível do objeto.

Em Java, o padrão State é frequentemente implementado usando interfaces e classes concretas. A interface `State` representa o estado e as classes concretas implementam a lógica específica do estado. A classe Context representa o objeto que contém o estado interno.

Aqui está um exemplo simples de como usar o padrão State em Java:

```java
public interface State {
    void pressPlay();
}

public class ReadyState implements State {
    private AudioPlayer audioPlayer;

    public ReadyState(AudioPlayer audioPlayer) {
        this.audioPlayer = audioPlayer;
    }

    public void pressPlay() {
        audioPlayer.changeState(new PlayingState(audioPlayer));
    }
}

public class PlayingState implements State {
    private AudioPlayer audioPlayer;

    public PlayingState(AudioPlayer audioPlayer) {
        this.audioPlayer = audioPlayer;
    }

    public void pressPlay() {
        audioPlayer.changeState(new ReadyState(audioPlayer));
    }
}

public class AudioPlayer {
    private State state;

    public AudioPlayer() {
        state = new ReadyState(this);
    }

    public void changeState(State newState) {
        state = newState;
    }

    public void pressPlay() {
        state.pressPlay();
    }
}

public class AudioPlayerExample {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();

        audioPlayer.pressPlay(); // Output: "Playing"
        audioPlayer.pressPlay(); // Output: "Ready"
    }
}
```

Neste exemplo, a classe `State` representa o estado e define o método `pressPlay`. As classes `ReadyState` e `PlayingState` implementam a lógica específica de cada estado e implementam o método `pressPlay` de acordo com o comportamento necessário.

A classe `AudioPlayer` representa o contexto e contém o estado interno do objeto. O método `changeState` altera o estado interno do objeto para o novo estado. O método `pressPlay` delega a chamada ao método `pressPlay` para o estado atual.

Por fim, na classe `AudioPlayerExample`, criamos uma instância da classe `AudioPlayer` e chamamos o método `pressPlay` duas vezes. Na primeira chamada, o estado do objeto é alterado para `PlayingState` e é impressa a mensagem "Playing". Na segunda chamada, o estado do objeto é alterado de volta para `ReadyState` e é impressa a mensagem "Ready".

Em resumo, o padrão `State` é útil para implementar objetos que mudam de comportamento de acordo com seu estado interno. Isso permite que o código seja mais modular e flexível, já que a lógica de cada estado é encapsulada em sua própria classe. Além disso, o padrão `State` permite que o objeto altere seu comportamento sem a necessidade de mudar sua interface pública.

##

### <a name="strategy"></a> Strategy

O padrão Strategy é um padrão de projeto comportamental que permite que um objeto tenha um comportamento variável, permitindo que a classe possa selecionar um algoritmo dentre vários diferentes, dependendo das necessidades do contexto em que o objeto está sendo utilizado. Isso pode ser útil em situações em que uma classe precisa mudar dinamicamente o seu comportamento em tempo de execução.

Em Java, o padrão Strategy é frequentemente implementado usando interfaces e classes concretas. A interface Strategy define o comportamento comum a todas as estratégias, enquanto as classes concretas implementam algoritmos específicos.

Aqui está um exemplo simples de como usar o padrão Strategy em Java:

```java
public interface PaymentStrategy {
    void pay(double amount);
}

public class CreditCardStrategy implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String dateOfExpiry;

    public CreditCardStrategy(String name, String cardNumber, String cvv, String dateOfExpiry) {
        this.name = name;
        this.cardNumber = cardNumber;
        this.cvv = cvv;
        this.dateOfExpiry = dateOfExpiry;
    }

    public void pay(double amount) {
        System.out.println("Paid " + amount + " using credit card");
    }
}

public class PayPalStrategy implements PaymentStrategy {
    private String email;
    private String password;

    public PayPalStrategy(String email, String password) {
        this.email = email;
        this.password = password;
    }

    public void pay(double amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}

public class ShoppingCart {
    private List<Item> items;

    public ShoppingCart() {
        this.items = new ArrayList<>();
    }

    public void addItem(Item item) {
        this.items.add(item);
    }

    public void removeItem(Item item) {
        this.items.remove(item);
    }

    public double calculateTotal() {
        double sum = 0;
        for (Item item : items) {
            sum += item.getPrice();
        }
        return sum;
    }

    public void pay(PaymentStrategy paymentStrategy) {
        double amount = calculateTotal();
        paymentStrategy.pay(amount);
    }
}

public class StrategyExample {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        Item item1 = new Item("Shirt", 100);
        Item item2 = new Item("Pants", 200);

        cart.addItem(item1);
        cart.addItem(item2);

        cart.pay(new CreditCardStrategy("John Doe", "123456789", "123", "12/24"));
        cart.pay(new PayPalStrategy("johndoe@example.com", "password"));
    }
}
```

Neste exemplo, a interface `PaymentStrategy` define o comportamento comum a todas as estratégias. As classes `CreditCardStrategy` e `PayPalStrategy` implementam algoritmos específicos de pagamento usando cartão de crédito e PayPal, respectivamente.

A classe `ShoppingCart` representa o contexto em que a estratégia é utilizada. O método `pay` delega a chamada ao método `pay` para a estratégia selecionada. Isso permite que o objeto `ShoppingCart` tenha diferentes comportamentos de pagamento, dependendo da estratégia selecionada.

Na classe `StrategyExample`, criamos uma instância da classe `ShoppingCart` e adicionamos dois itens. Em seguida, selecionamos diferentes estratégias de pagamento, passando cada uma delas como parâmetro para o método `pay`.

Em resumo, o padrão Strategy é um padrão de projeto comportamental que permite que diferentes algoritmos possam ser selecionados dinamicamente em tempo de execução, dependendo do contexto em que são usados. Ele separa o algoritmo da sua implementação, permitindo que cada um possa ser alterado independentemente, sem afetar o código cliente.

##

### <a name="tm"></a> Template Method

O padrão Template Method é um padrão de projeto comportamental que define a estrutura básica de um algoritmo, permitindo que as subclasses forneçam implementações específicas para certos passos do algoritmo. Isso permite que a estrutura geral do algoritmo seja definida em uma classe base, enquanto os detalhes específicos são deixados para as subclasses.

O padrão Template Method **é útil em situações em que vários algoritmos têm estruturas semelhantes, mas diferem em alguns detalhes**. Em vez de repetir a mesma estrutura básica em várias classes, o padrão Template Method **permite que a estrutura geral seja definida em uma única classe e os detalhes específicos sejam implementados em subclasses**.

Em Java, o padrão Template Method é frequentemente implementado usando uma classe abstrata que define o método template, que define a estrutura geral do algoritmo, e métodos abstratos, que as subclasses devem implementar para fornecer detalhes específicos.

Aqui está um exemplo simples de como usar o padrão Template Method em Java:

```java
public abstract class Game {
    protected abstract void initialize();
    protected abstract void startPlay();
    protected abstract void endPlay();

    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
}

public class Chess extends Game {
    @Override
    protected void initialize() {
        System.out.println("Initializing Chess Game...");
    }

    @Override
    protected void startPlay() {
        System.out.println("Starting Chess Game...");
    }

    @Override
    protected void endPlay() {
        System.out.println("Ending Chess Game...");
    }
}

public class TicTacToe extends Game {
    @Override
    protected void initialize() {
        System.out.println("Initializing Tic-Tac-Toe Game...");
    }

    @Override
    protected void startPlay() {
        System.out.println("Starting Tic-Tac-Toe Game...");
    }

    @Override
    protected void endPlay() {
        System.out.println("Ending Tic-Tac-Toe Game...");
    }
}

public class TemplateMethodExample {
    public static void main(String[] args) {
        Game chess = new Chess();
        chess.play();

        Game tictactoe = new TicTacToe();
        tictactoe.play();
    }
}
```

Neste exemplo, a classe abstrata `Game` define o método template `play`, que define a estrutura geral do jogo. As subclasses `Chess` e `TicTacToe` implementam os métodos abstratos `initialize`, `startPlay` e `endPlay`, que fornecem os detalhes específicos para cada jogo.

A classe `TemplateMethodExample` cria instâncias das subclasses `Chess` e `TicTacToe` e chama o método `play` em cada uma delas. O método `play` executa a estrutura geral do jogo, chamando os métodos `initialize`, `startPlay` e `endPlay` nas subclasses.

Em resumo, o padrão Template Method é um padrão de projeto comportamental que define a estrutura básica de um algoritmo em uma classe base e permite que as subclasses forneçam detalhes específicos. Em Java, o padrão Template Method é frequentemente implementado usando uma classe abstrata que define o método template e métodos abstratos que as subclasses devem implementar. O exemplo acima mostra como usar o padrão Template Method para criar diferentes jogos com estruturas semelhantes, mas detalhes específicos diferentes.

##

### <a name="visitor"></a> Visitor

O padrão Visitor é um padrão de projeto comportamental que permite adicionar novas operações a uma estrutura de objetos existente sem modificar a própria estrutura. Ele separa as operações dos objetos em classes separadas, chamadas visitantes, permitindo que novas operações sejam adicionadas ao sistema sem modificar as classes existentes.

O padrão Visitor é **útil quando se tem uma estrutura de objetos complexa que contém muitos tipos diferentes de objetos e muitas operações que podem ser executadas nesses objetos**. Em vez de adicionar essas operações diretamente aos objetos, o padrão Visitor adiciona-as como visitantes, que visitam os objetos e executam as operações.

Em Java, o padrão Visitor é frequentemente implementado usando interfaces para os visitantes e as classes que serão visitadas. As classes visitadas implementam um método accept que recebe um visitante como argumento e chama o método apropriado do visitante. Cada visitante implementa métodos para executar as operações nos objetos que visita.

Aqui está um exemplo simples de como usar o padrão Visitor em Java:

```java
interface Visitor {
    void visit(Circle circle);
    void visit(Square square);
}

interface Shape {
    void accept(Visitor visitor);
}

class Circle implements Shape {
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class Square implements Shape {
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class AreaVisitor implements Visitor {
    public void visit(Circle circle) {
        System.out.println("Calculating area of circle");
    }
    public void visit(Square square) {
        System.out.println("Calculating area of square");
    }
}

class PerimeterVisitor implements Visitor {
    public void visit(Circle circle) {
        System.out.println("Calculating perimeter of circle");
    }
    public void visit(Square square) {
        System.out.println("Calculating perimeter of square");
    }
}

public class VisitorExample {
    public static void main(String[] args) {
        Shape[] shapes = {new Circle(), new Square()};
        Visitor areaVisitor = new AreaVisitor();
        Visitor perimeterVisitor = new PerimeterVisitor();

        for (Shape shape : shapes) {
            shape.accept(areaVisitor);
            shape.accept(perimeterVisitor);
        }
    }
}
```

Neste exemplo, a interface `Shape` define o método `accept`, que recebe um visitante como argumento. As classes `Circle` e `Square` implementam o método `accept`, chamando o método apropriado do visitante.

As interfaces `Visitor`, `AreaVisitor` e `PerimeterVisitor` definem as operações que podem ser executadas nos objetos visitados. Cada uma das classes visitantes implementa os métodos definidos na interface `Visitor`, executando as operações nos objetos visitados.

A classe `VisitorExample` cria um array de objetos `Shape` e dois visitantes, `AreaVisitor` e `PerimeterVisitor`. Ela itera pelo array de objetos `Shape`, chamando o método `accept` em cada um deles, passando os visitantes como argumentos. O método `accept` chama o método apropriado do visitante, que executa a operação apropriada no objeto visitado.

Em resumo, o padrão `Visitor` é um padrão de projeto comportamental que permite adicionar novas operações a uma estrutura de objetos existente sem modificar a própria estrutura. Em Java, o padrão Visitor é frequentemente implementado usando interfaces para os visitantes e as classes que serão visitadas. O exemplo acima ilustra como o padrão Visitor pode ser usado para adicionar uma nova operação a uma hierarquia de classes existente, sem modificar as próprias classes.

#

### <a name="interpreter"></a> Interpreter

O padrão Interpreter é um padrão de projeto comportamental que define uma gramática para uma linguagem e fornece uma maneira de avaliar as expressões dessa linguagem. O padrão Interpreter é útil quando você tem uma linguagem que precisa ser avaliada em tempo de execução.

O padrão Interpreter usa uma árvore de sintaxe para representar as expressões da linguagem. Cada nó na árvore é um objeto que representa uma expressão. O Interpreter percorre a árvore, avaliando cada nó e retornando o resultado.

Vamos supor que você está trabalhando em um sistema que avalia expressões aritméticas simples. Você tem uma classe chamada "Expression" que define uma interface para as expressões e duas classes concretas "Number" e "Addition" que implementam a interface.

```java
public interface Expression {
    int evaluate();
}

public class Number implements Expression {
    private int value;

    public Number(int value) {
        this.value = value;
    }

    public int evaluate() {
        return value;
    }
}

public class Addition implements Expression {
    private Expression left;
    private Expression right;

    public Addition(Expression left, Expression right) {
        this.left = left;
        this.right = right;
    }

    public int evaluate() {
        return left.evaluate() + right.evaluate();
    }
}
```

Nesse exemplo, a interface `Expression` define o método `evaluate` que avalia a expressão e retorna o resultado. A classe `Number` implementa a interface `Expression` e representa um número inteiro. A classe `Addition` também implementa a interface `Expression` e representa uma expressão de adição.

Para avaliar a expressão `2 + 3`, você cria uma instância de `Number` para representar o número 2, uma instância de `Number` para representar o número 3 e uma instância de `Addition` para representar a operação de adição. Então, você chama o método `evaluate` na instância de `Addition` para obter o resultado.

```java
Expression expression = new Addition(new Number(2), new Number(3));
int result = expression.evaluate(); // Resultado é 5
```

## Parabéns, você chegou no final do Guia GoF!! 🥳

Parabéns por completar este guia abrangente dos 23 padrões de projeto definidos pelo Gang of Four! Esperamos que você o tenha achado informativo e útil em seu trabalho de desenvolvimento.

Ao entender e implementar esses padrões, você será capaz de escrever código mais flexível, reutilizável e fácil de manter. Esses padrões são soluções testadas e comprovadas para problemas comuns âmbito de desenvolvimento software, e seu uso pode melhorar significativamente a qualidade de suas aplicações.

Gostaríamos de agradecer por dedicar seu tempo para ler este guia e esperamos que ele tenha ajudado você a se tornar um desenvolvedor melhor. Se você achou útil, ficaríamos muito gratos se pudesse dar uma estrela ao repositório e compartilhá-lo com seus amigos e colegas.

Segue algumas das minhas redes sociais:

* Instagram: [@ivii.ns](https://www.instagram.com/ivii.ns/)
* Linkedin: [Dev-Ivi](https://www.linkedin.com/in/ivisson-pereira-b301aa250/)
> Obrigado novamente por ler este guia e boa sorte no desenvolvimento!!
