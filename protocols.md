# Protocols

Enquanto programa em Elixir, você já deve te se deparado com um tipo de erro `Protocol.UndefinedError`. Esse erro é facil de reproduzir:

```elixir
iex(1)> Enum.map(200, fn x -> x + 1 end)
** (Protocol.UndefinedError) protocol Enumerable not implemented for 200 of type Integer
    (elixir 1.12.3) lib/enum.ex:1: Enumerable.impl_for!/1
    (elixir 1.12.3) lib/enum.ex:141: Enumerable.reduce/3
    (elixir 1.12.3) lib/enum.ex:3958: Enum.map/2
```

O erro está informando que o protocolo `Enumerable` não foi implementado para o valor `200`, que é do tipo inteiro. O que é o protocolo Enumerable? Onde eu posso olhar pra esse protocolo?

Existe uma forma de alcançar [polimorfismo](<https://en.wikipedia.org/wiki/Polymorphism_(computer_science)>) com Elixir. Com _Protocols_. Inclusive, o próprio nome vem do conceito de [protocols](<https://en.wikipedia.org/wiki/Interface_(object-oriented_programming)>) de Programação Orientada à Objetos.

## References

- Polimorfismo - https://en.wikipedia.org/wiki/Polymorphism_(computer_science)
