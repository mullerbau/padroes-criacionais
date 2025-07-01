# 🏭 Padrão de Projeto: Factory Method

## 📚 O que é?
O **Factory Method** é um **padrão de projeto criacional** que define um método para criar objetos, permitindo que as **subclasses escolham qual classe concreta será instanciada**.

Ele evita que o **código cliente** fique responsável por instanciar objetos diretamente.

---

## 💡 Problema sem Factory Method

O código cliente precisa conhecer as classes concretas e decidir qual objeto criar, gerando **acoplamento** e **dificuldade de manutenção**.

```typescript
if (tipo === "cartao") {
  pagamento = new PagamentoCartao();
} else if (tipo === "boleto") {
  pagamento = new PagamentoBoleto();
}
