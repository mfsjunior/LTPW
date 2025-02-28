# Questões e Respostas

1. **O que é a JVM e qual seu papel na execução de um programa Java?**

    JVM é uma máquina virtual que interpreta/traduz bytecode (que por sua vez são um conjunto de instruções previamente compiladas a partir do código fonte) em código nativo de máquina (Assembly), para garantir portabilidade através de sistemas operacionais. É fornecida uma especificação dela, mas existem diferentes implementações.

2. **Explique a diferença entre JDK, JRE e JVM.**

    JDK é o conjunto de ferramentas necessárias para desenvolver em Java e JRE é o ambiente necessário para executar programas Java, que por consequência inclui a JVM.

3. **O que é um construtor em Java? Como ele funciona?**

     Construtor é um tipo especial de método utilizado para inicializar o objeto de uma classe e fornecido por padrão sem argumentos, mas podendo ser personalizado com argumentos e instruções.

    ```java
    class Exemplo {
        // Adicionando construtor com argumento
        public Exemplo(String texto) {
            System.out.println(texto);
        }

        // Adicionando construtor padrão, já que uma implementação diferente foi criada
        public Exemplo() { }
    }

    Exemplo obj1 = new Exemplo(); // Construtor padrão
    Exemplo obj2 = new Exemplo("exemplo"); // Construtor com argumento adicional
   ```

4. **Qual é a diferença entre tipos primitivos e objetos em Java?**

    Tipos primitivos são comuns a diversas linguagens e utilizados para declarar variáveis, armazenadas na memória _stack_ (estática). Objetos são instanciações de classes, que por sua vez podem ser compreendidas como "tipos" definidos pelo desenvolvedor e são armazenados na memória _heap_ (dinâmica).

    ```java
    class Inteiro {
        private int valor;

        public Inteiro(int valor) {
            this.valor = valor;
        }
    }

    int inteiro = 2; // Inicializa uma variável do tipo primitivo int
    Inteiro objeto = new Inteiro(2); // Inicializa uma variável com o mesmo valor, porém como um objeto da classe Inteiro
    ```

5. **O que é sobrecarga de métodos em Java?**

    Sobrecarga é a modificação da assinatura de um método através da declaração de outro com mesmo nome.

    ```java
    // Faz a soma de dois argumentos inteiros
    int soma(int fator1, int fator2) {
        return fator1 + fator2;
    }

    // Faz a soma de dois argumentos em ponto flutuante
    float soma(float fator1, float fator2) {
        return fator1 + fator2;
    }
    ```

6. **Qual a diferença entre ArrayList e LinkedList?**

    `ArrayList` é simplesmente uma coleção dinâmica de itens com acesso geralmente mais rápido do que na `LinkedList`, que por sua vez é uma coleção dinâmica de itens vinculados/ligados, ou seja, possuem uma referência para o endereço do próximo item e por isso permite melhor desempenho na adição e remoção de itens, principalmente na primeira e na última posição.

    ```java
    // Inicia cada estrutura com 100 zeros
    ArrayList<Integer> arrayList = new ArrayList<Integer>(Collections.nCopies(100, 0));
    LinkedList<Integer> linkedList = new LinkedList<Integer>(Collections.nCopies(100, 0));

    // Acessa um elemento no meio
    arrayList.get(50); // Mais rápido
    linkedList.get(50); // Mais lento

    // Adiciona um 0 na primeira posição
    arrayList.add(0, 0); // Mais lento
    linkedList.addFirst(0); // Mais rápido

    // Remove o primeiro elemento
    arrayList.remove(0); // Mais lento
    linkedList.removeFirst(); // Mais rápido

    // Adiciona um 0 na última posição
    arrayList.add(100, 0); // Mais lento
    linkedList.addLast(0); // Mais rápido

    // Remove o último elemento
    arrayList.remove(100); // Mais lento
    linkedList.removeLast(); // Mais rápido
    ```

7. **O que é herança em Java e como funciona?**

    Herança é a passagem de atributos e métodos não privados de uma classe para a que extende ela, potencializando o reuso de código.

    ```java
    class Superclasse { }

    class Subclasse extends Superclasse { }
    ```

8. **Explique a diferença entre == e .equals() em Java.**

    `==` é um operador que compara a referência de dois valores e `.equals()` é um método, portanto passível de sobrecarga e sobrescrita, que compara o estado/valor de objetos.

    ```java
    String valor1 = "valor";
    String valor2 = "valor";
    String valor3 = new String("valor");

    System.out.println(valor1 == valor2); // true
    System.out.println(valor1 == valor3); // false
    System.out.println(valor1.equals(valor3)); // true
    System.out.println(valor1.equals(valor2)); // true
    ```

9. **O que é o tratamento de exceções e como ele é feito em Java?**

    É a captura de condições anômalas com a possibilidade de instruções específicas para caso elas ocorram.

    ```java
    try {
        int vetor[] = {1, 2, 3};

        System.out.println(vetor[4]);
    } catch (Exception excecao) {
        System.out.println(excecao.getMessage());
    }
    ```

10. **O que são classes abstratas e interfaces em Java? Qual a diferença entre elas?**

    Classes abstratas podem possuir tanto métodos já implementados quanto abstratos, que precisam ser implementados nas classes que herdá-las (extendê-las), e seus elementos são suscetíveis a qualquer modificador. Já interfaces são estruturas puramente abstratas com elementos implicitamente públicos, não podendo possuir métodos implementados (a não ser que tenham o modificador `default`), sendo que todos são estáticos (globalmente acessíveis) por padrão, e os atributos são necessariamente finais (constantes) e estáticos. Por fim, interfaces são implementadas e não extendidas.

    ```java
    abstract class Moda {
        public void criarTendecia() {
            System.out.println("Tendência atual: cores quentes");
        }
        
        public abstract void criarPeça();
    }

    interface Estilo {
        int qtdMinPecas = 3;

        default void criarReferência() {
            System.out.println("Referência na mídia criada");
        }

        void criarPadrao();
    }

    class Vintage extends Moda implements Estilo {
        public void criarPeça() {
            System.out.println("Calça boca de sino vermelha");
        }

        public void criarPadrao() {
            System.out.println("Padrão criado: peças com características antigas/retrô");
        }

        public void alterarQtdMinPecas(int novaQtd) {
            Estilo.qtdMinPecas = novaQtd; // Erro de compilação por ser uma constante
        }
    }
    ```

11. **O que é encapsulamento e como ele é implementado em Java?**

    É a limitação do acesso direto aos atributos de uma classe através do fornecimento de uma interface pública que independe da implementação, portanto aumenta a manutenibilidade do código. Em Java é implementado através de métodos get (leitura) e set (escrita), o que também aumenta a integridade dos dados, ao possibilitar a validação dos mesmos, e o reuso.

    ```java
    import java.time.LocalDate;
    import java.time.Period;

    class Documento {
        private LocalDate dataValidade;

        // Define a data de validade a partir do tempo de validade
        public void setTempoValidade(Period idade) {
            this.dataValidade = LocalDate.now().plus(idade);
        }

        // Calcula o tempo de validade a partir da data de validade
        public LocalDate getTempoValidade() {
            return Period.between(LocalDate.now(), this.dataValidade);
        }
    }
    ```

13. **Qual é a diferença entre sobrecarga e sobrescrita de métodos?**

    Diferentemente do que foi conceituado na questão 5 para sobrecarga, sobrescrita é a declaração de um método com a mesma assinatura que outro, porém com implementação diferente.

    ```java
    class PrimeiroGrau {
        // Soma de dois inteiros
        int soma(int fator1, int fator2) {
            return fator1 + fator2;
        }
    }

    class SegundoGrau extends PrimeiroGrau {
        // Soma do quadrado de dois inteiros
        @Override
        int soma(int fator1, int fator2) {
            return Math.pow(fator1, 2) + Math.pow(fator2, 2);
        }
    }
    ```

    14. **O que é polimorfismo e como ele se manifesta em Java?**

    Polimorfismo é a variação de implementações de um método com mesmo nome em diferentes classes, potencializando também o reuso e a manutenibilidade de código, além da legibilidade.

    ```java
    import java.time.LocalDate;
    import java.time.temporal.ChronoUnit;

    interface Reptil {
        void trocarPele();
    }

    class Serpente implements Reptil {
        LocalDate ultimaTroca;

        public Serpente() {
            this.ultimaTroca = LocalDate.now();
        }

        public void trocarPele() {
            long diasDesdeUltimaTroca = ChronoUnit.DAYS.between(ultimaTroca, LocalDate.now());

            if (diasDesdeUltimaTroca > 60) {
                System.out.println("Pele trocada!");
            } else {
                System.out.println("Ainda não é hora de trocar a pele.");
            }
        }
    }

    class Sucuri extends Serpente {
        @Override
        public void trocarPele() {
            long diasDesdeUltimaTroca = ChronoUnit.DAYS.between(ultimaTroca, LocalDate.now());

            if (diasDesdeUltimaTroca > 120) {
                System.out.println("Pele trocada!");
            } else {
                System.out.println("Ainda não é hora de trocar a pele.");
            }
        }
    }
    ```

16. **O que é associação, composição e agregação em POO?**

    Associação é a relação na qual uma classe A utiliza de alguma forma um objeto da classe B. Se essa utilização é de forma que, conceitualmente, A contém B ou é uma coleção de B, a associação se caracteriza especificamente como uma agregação. Se essa agregação é de tal modo que o objeto da classe B é instanciado dentro de A, uma relação mais forte de pertencimento e dependência passa a existir, de tal modo que se um objeto instanciado da classe A for destruído, o(s) objeto(s) da classe B instaciado(s) dentro dele também será(ão), caracterizando uma composição.

    ```java
    class Universidade {
        private ArrayList<Estudante> estudantes;

        public Universidade() {
            this.estudantes = new ArrayList<>();
        }

        // Associação entre Universidade e Estudante
        public void matricular(Estudante estudante) {
            estudantes.add(estudante);
        }
    }

    class Estudante {
        private Filiacao[] filiacao = new Filiacao[2];

        // Agregação entre Estudante e Filiacao
        public Estudante(Filiacao filiacao1, Filiacao filiacao2) {
            this.filiacao[0] = filiacao1;
            this.filiacao[1] = filiacao2;
        }
    }

    class Filiacao {
        private Documento documento;

        public Filiacao(String numeroDocumento) {
            this.documento = new Documento(numeroDocumento); // Composição entre Filiacao e Documento
        }
    }

    class Documento {
        private String nome;

        public Documento(String nome) {
            this.nome = nome;
        }
    }
    ```

17. **O que acontece se uma classe implementar duas interfaces que possuem métodos com a mesma assinatura?**

    Esta classe precisará implementar somente 1x o método, que já servirá como implementação para ambas as interfaces.

    ```java
    interface Animal {
        public void movimentoArticulado();
    }

    interface Mamifero {
        public void movimentoArticulado();
    }

    class Vaca implements Animal, Mamifero {
        public void movimentoArticulado() {
            System.out.println("Se movendo de forma articulada");
        }
    }
    ```

18. **O que é a palavra-chave super em Java e quando ela deve ser usada?**

    `super` é utilizada para se referenciar à superclasse. Com essa restrição de escopo, é possível utilizar os elementos da classe que foi extendida/herdada.

    ```java
    class Carro {
        public void ativarEsguicho() {
            System.out.println("Esguichos acionados!");
        }
    }

    class CarroModerno extends Carro {
        public void limparVidro() {
            super.ativarEsguicho();

            System.out.println("Limpadores acionados!");
        }
    }
    ```

19. **Como funciona o conceito de classes aninhadas (_inner classes_) em Java?**

    São classes declaradas dentro de outras por não terem sentido de existência fora delas, sendo suscetíveis aos modificadores de acesso, ampliando a possibilidade de representação do contexto da solução e facilitando a leitura de _namespaces_, por exemplo. Essas _inner classes_ podem acessar diretamente a _outer class_ e, portanto, modificá-la.

    ```java
    class Corrente {
        int tamanho;

        class Elo {
            int posicao;

            public void restante() {
                return "Restam " + (tamanho - posicao) + " elos até o fim da corrente!"; // Acessando diretamente um atributo da classe externa
            }
        }
    }
    ```

20. **O que é um método final e uma classe final em Java?**

    Um método `final` não pode ser sobrescrito por outros e uma classe `final` não pode ser herdada/extendida por outras.

    ```java
    class Toyota {
        public final void ligarFarois() {
            return "Faróis ligados atrás do volante!";
        }
    }

    final class Etios extends Toyota {
        public void ligarFarois() {
            return "Faróis ligados ao lado do volante!"; // Erro de compilação
        }
    }

    final class EtiosXLS extends Etios { } // Erro de compilação
    ```
