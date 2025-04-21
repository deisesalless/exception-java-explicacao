# Exceções em Java

Java utiliza um sistema robusto de tratamento de exceções para lidar com situações inesperadas durante a execução do programa. Aqui está uma visão geral simples das exceções em Java:

## Hierarquia de Exceções

![Hierarquia de Exceções em Java](https://github.com/deisesalless/exception-java-explicacao/blob/main/hierarquia-exception-java.png)

- **Throwable**: É a superclasse de todas as exceções e erros em Java.
  - **Error**: Indica problemas graves que geralmente não são recuperáveis, como `OutOfMemoryError` (quando a JVM fica sem memória) e `StackOverflowError` (quando há recursão infinita).
  - **Exception**: Representa condições que um programa Java deve tratar. Pode ser dividida em:
    - **Checked Exceptions**: Exceções que devem ser tratadas com `try-catch` ou `throws` na assinatura do método.
    - **Unchecked Exceptions**: Exceções que não precisam ser explicitamente tratadas, como `NullPointerException` ou `IllegalArgumentException`.

## Tratamento de Exceções

- **throw**: Utilizado para lançar explicitamente uma exceção em um método.
- **throws**: Utilizado na assinatura do método para indicar que o método pode lançar uma exceção e que o chamador deve lidar com ela.
- **try-catch**: Bloco usado para capturar exceções e fornecer tratamento para elas, evitando que o programa termine abruptamente.

## Vantagens de Criar uma Exceção Personalizada

Criar exceções personalizadas permite que você crie um tipo de exceção específico para seu domínio de problema. Isso melhora a legibilidade do código e facilita o tratamento de erros específicos. Veja um exemplo simples de criação e uso de uma exceção personalizada:

```java

// Exceção personalizada -> Boa prática fazer dessa forma
public class RegrasDeNegocio extends Exception {
    public RegrasDeNegocio(String mensagem) {
        super(mensagem);
    }
}


public class Exemplo {

    private List<String> listaDePessoas = new ArrayList<>();

    // Método para adicionar pessoa
    public void adicionarPessoa(String nome, int idade) throws RegrasDeNegocio {
        if (idade < 18) {
            throw new RegrasDeNegocio("Não é permitido adicionar " + nome + " na lista pois é menor de idade, possui: " + idade);
        }

        listaDePessoas.add(nome);
        System.out.println("Pessoa " + nome + " adicionada com sucesso");
    }

    public static void main(String[] args) {
        Exemplo exemplo = new Exemplo();

        try {
            exemplo.adicionarPessoa("Ana", 20); // Será adicionada
            exemplo.adicionarPessoa("João", 16); // Lança exceção
        } catch (RegrasDeNegocio e) {
            System.err.println("Exceção capturada: " + e.getMessage());
        }
    }
}

```

Neste exemplo, `RegrasDeNegocio` é uma exceção personalizada que herda de `Exception`, permitindo que sejam tratados exeções verificadas e não verificadas seguindo a lógica do projeto e as regras de negócio.

Espero que isso ajude a entender melhor o conceito de exceções em Java!

