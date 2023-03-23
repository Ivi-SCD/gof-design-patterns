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

## Padrões Estruturais
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
## Padrões Comportamentais
