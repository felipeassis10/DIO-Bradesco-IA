# Skill: Python OOP

## Objetivo
Explicar a lógica de Orientação a Objetos em Python de um jeito direto e prático, focado em cenários reais de desenvolvimento e dados.

---

## Exemplos de Código

### 1. Classe Base e Encapsulamento (`__init__`, `self` e atributos protegidos)
python
class ContaBancaria:
    def __init__(self, titular: str, saldo_inicial: float = 0.0):
        self.titular = titular
        self._saldo = saldo_inicial  # Atributo protegido

    def depositar(self, valor: float) -> None:
        if valor > 0:
            self._saldo += valor
            print(f"Depósito de R$ {valor:.2f} realizado com sucesso!")
        else:
            print("Valor de depósito inválido.")

    @property
    def saldo(self) -> float:
        return self._saldo

    class ContaCorrente(ContaBancaria):
    def __init__(self, titular: str, saldo_inicial: float = 0.0, limite: float = 500.0):
        super().__init__(titular, saldo_inicial)
        self.limite = limite

    def sacar(self, valor: float) -> bool:
        if valor <= (self._saldo + self.limite):
            self._saldo -= valor
            return True
        return False
