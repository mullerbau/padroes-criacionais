# Padrão de Projeto: Prototype

O **Prototype** é um padrão de projeto criacional que permite a cópia ou "clonagem" de objetos existentes, sem que o código que faz a cópia precise conhecer as classes específicas desses objetos.

Isso reduz dependências e melhora o encapsulamento, já que o objeto original não precisa ser exposto ou modificado a todo momento; em vez disso, trabalhamos com seus clones.

---

## Como ele faz isso?

O padrão funciona definindo um método **`clone()`** no objeto que servirá como protótipo.

Quando um novo objeto é necessário, em vez de criá-lo do zero (com o operador `new`), simplesmente chamamos o método **`clone()`** do protótipo. Este método é responsável por criar uma nova instância e copiar os dados do objeto original para a nova.

Assim, o clone nasce com o mesmo estado do original, pronto para ser usado ou modificado de forma independente.

---

## Exemplo de código:

Este exemplo em **Java** mostra a implementação clássica usando a interface `Cloneable` em uma classe `Carro`.

```java
// 1. A classe protótipo deve implementar a interface Cloneable
class Carro implements Cloneable {
    private String modelo;
    private String cor;

    public Carro(String modelo, String cor) {
        this.modelo = modelo;
        this.cor = cor;
    }

    // Métodos para modificar os dados dos clones
    public void setModelo(String modelo) { this.modelo = modelo; }
    public void setCor(String cor) { this.cor = cor; }

    @Override
    public String toString() {
        return "Carro[modelo=" + modelo + ", cor=" + cor + "]";
    }

    // 2. Sobrescrevemos o método clone() para que seja público
    @Override
    public Carro clone() {
        try {
            // super.clone() faz a cópia do objeto
            return (Carro) super.clone();
        } catch (CloneNotSupportedException e) {
            // Não deve acontecer se a classe implementa Cloneable
            return null;
        }
    }
}

// 3. Cliente que utiliza o padrão
public class Main {
    public static void main(String[] args) {
        // A criação original acontece apenas uma vez
        Carro prototipo = new Carro("Sedan Genérico", "preto");
        System.out.println("Protótipo Original Criado: " + prototipo);

        System.out.println("\n--- Usando clones a partir do protótipo ---");

        // Os clones são criados de forma rápida, sem chamar o construtor
        Carro carroDoJoao = prototipo.clone();
        carroDoJoao.setCor("azul"); // Modificamos apenas o clone

        Carro carroDaMaria = prototipo.clone();
        carroDaMaria.setModelo("Hatch Esportivo");
        carroDaMaria.setCor("vermelho"); // Modificamos apenas o clone

        System.out.println("Clone 1 (modificado): " + carroDoJoao);
        System.out.println("Clone 2 (modificado): " + carroDaMaria);
        System.out.println("Protótipo Original (inalterado): " + prototipo);
    }
}