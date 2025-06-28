# Prototype

## **Prototype:**

A intenção do prototype, é copiar objetos existentes, sem ter uma dependência adicional de suas classes. Além de ter várias outras vantagens em usar esse pattern, o prototype ajuda também a ter um melhor encapsulamento dentro do código, já que clona o objeto original, para ele não precisar ser acessado a todo momento.

## **Como ele faz isso?**

O Prototype é implementado criando um construtor que recebe o próprio objeto como parâmetro, herdando e "copiando" seus dados para um novo objeto. A partir desse clone, conseguimos criar novas classes sem interferir no objeto original, tornando o código mais seguro, simples e com melhor encapsulamento.

 

## **Exemplo de código:** 

```
function exemploSemPadrao(int):
    return int;
```

```
function exemploComPadrao(num):
    return num;
```


**Sem o padrão**, mostrar um código com Getters e Setters para acessar uma classe privada, na intenção de ‘copiar’ a classe existente.

**Com o padrão**, dar o exemplo de criação de uma nova classe, com o parâmetro da classe que deseja copiar

