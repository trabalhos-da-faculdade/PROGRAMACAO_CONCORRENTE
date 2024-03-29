## PROGRAMAÇÃO CONCORRENTE

Utilizamos a Classe Thread de Java para fazer programas Concorrente

* Um programa concorrente é considerado **Justo** se ele conclui todos os Processos Iniciados nele
* **Interleaving** é quando os processos são escolhidos de forma aleatória para rodarem

### Exemplo de um programa simples com Threads

**Funções da Thread**

* Extendemos a Classe Thread em nosso Programa.

```java
public class Teste extends Thread{}
```

* Definimos o Construtor da Classe,entrando um valor.

```java
public class Teste extends Thread{
    int n;
    public Teste(int n){
        this.n = n;
    }
}
```

* O que será rodado em um Programa Concorrente fica dentro de uma Função chamada **run()**.

```java
public class Teste extends Thread{
    int n;
    public Teste(int n){
        this.n = n;
    }
    public void run(){
        while(n > 0){
            System.out.println("Valor Atual: " + n);
            n = n - 1;
        }
    }
}
```

* Agora temos nosso Programa Concorrente, para rodarmos ele devemos criar um Objeto da Classe e usar a Função **Start()** para iniciar o Processo.

```java
public static void main(String[] args){
    Teste teste = new Teste(10);
    teste.start();
}
```

* Podemos ter vários Processo sendo chamados e eles vão ser alternados de forma aleatória.
* Criamos a Classe chamando o ID do Processo como parâmetro.

```java
public class TesteInterleaving extends Thread{
    int max = 10;
    int id;

    public TesteInterleaving(int id){
        this.id = id;
    }

    public void run(){
        int value = 0
        for(int i = 0 ; i < max ; i++){
            value += i;
            System.out.prinln("Processo " + id + " : " + value);
        }
    }

    public static void main(String[] args){
        TesteInterleaving t1 = new TesteInterleaving(1);
        TesteInterleaving t2 = new TesteInterleaving(2);
        TesteInterleaving t3 = new TesteInterleaving(3);

        t1.start();
        t2.start();
        t3.start();
    }
}
```

* Os processos vão ser iniciados de forma aleatória e vão ser todos concluidos, dessa forma esse programa possui interleaving e é Justo.

### Sessão Crítica

* Quando duas Threads estão interagindo em uma única variável global pode acontecer problemas devido que as duas Threads podem *Intercalar* operações uma da outra no meio dos Processos.
* **Sessão Crítica** então é um sistema com N processos, sendo sempre um ou mais processos.
  * Cada Processo pode ter seu Próprio Código.
  * Os processos compartilham dados variáveis,de qualquer tipo.
  * Cada processo possui Sessão Crítica de Código,onde atualizam os dados compartilhados.

**Uma Sessão Crítica deve ter:**

1. Prover Exclusão Mútua, onde as Threads não podem alterar a mesma variável ao mesmo tempo.
2. Não pode bloquear o progresso de outros Processos
3. Um processo deve ter uma espera limitada quando estiver rodando, onde ja que duas ou mais Threads estão lutando para rodar um mesmo trecho de código elas possam acessar esse trecho de código com uma espera cada um
4. Não se tem como saber a velocidade de ação das Threads

