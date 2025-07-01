# 🏭 Padrão de Projeto: Factory Method

## 📚 O que é?

Padrão de projeto criacional que define um método para criar objetos,  
permitindo que as subclasses escolham qual classe concreta será instanciada.

Evita que o código cliente fique responsável por instanciar objetos diretamente.

## 💡 Problema sem Factory Method

O código cliente precisa conhecer as classes concretas e decidir qual objeto criar,  
gerando acoplamento e dificuldade de manutenção.

```typescript
if (tipo === "cartao") {
  pagamento = new PagamentoCartao();
} else if (tipo === "boleto") {
  pagamento = new PagamentoBoleto();
}
```

## ✅ Solução com Factory Method

```typescript
abstract class PagamentoFactory {
  abstract criarPagamento(): Pagamento;
}

class PagamentoCartaoFactory extends PagamentoFactory {
  criarPagamento(): Pagamento {
    return new PagamentoCartao();
  }
}
```

Centraliza a criação dos objetos em um método especializado, deixando o código cliente desacoplado.

O código cliente só usa o método de criação e não precisa conhecer as classes concretas.

## 🎯 Quando Usar

✔ Quando o sistema precisa ser flexível e fácil de expandir;  
✔ Quando há variação no tipo de objeto a ser criado;  
✔ Quando queremos deixar o código mais organizado e desacoplado.

## ⚠️ Atenção

⚡ Pode gerar complexidade desnecessária em projetos simples;  
⚡ Exige mais classes no sistema.

## 🧠 Resumo

O Factory Method melhora a organização e flexibilidade do código,  
evitando que o cliente precise se preocupar com a criação de objetos concretos.
