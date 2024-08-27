# **Oque são Erros em Python?** ❌

Na programação no geral, inevitavelmente nos deparamos com situações imprevistas, como erros e exceções.

Imagine que você está construindo um sistema bancário e alguém insere um texto no lugar de um número. Quando você vai tentar realizar alguma operação aritmética com esse texto, um erro será gerado *(TypeError)* e seu programa quebrará.

Uma outra situação por exemplo, é por alguma falta de atenção durante a escrita do código, esquecer de fechar um parênteses, nesse caso um código de erro *(SyntaxError)* será gerado e, mais uma vez, o programa será quebrado.

***

## **1. Exemplos de Erros em Código**
Código que representa três tipos de erros diferentes: de sintaxe, de tipo e de uma divisão por 0.

```
# Erro de sintaxe.
print("olá"     # SyntaxError: unexpected EOF while parsing

# Erro de tipo.
3 + "olá"       # TypeError: unsupported operand type(s) for +: 'int' and 'str'

# Erro de divisão por zero.
10/0            # ZeroDivisionError: division by zero

```

## **2. Mantendo o Controle**
Como esses erros podem aparecer, precisamos de uma estrutura para poder lidar com eles. E é justamente isso que o bloco **try-except** do Python faz. Ele nos permite tratar exceções de maneira controlada.

**Exemplo** <br>
Imagine que estamos criando um programa onde o usuário digita um número que será o denominador da divisão por 10. Há inúmeros problemas que podem acontecer, o primeiro deles é caso a pessoa digitasse 0, pois há o erro da divisão por zero. O segundo erro é caso ela não
digitasse um número, isso também geraria um problema. Note que há diversas situações que podem dar errado!

```
# Inicializa com o try.
try:                            # O try é o bloco de código que você insere o código sujeito a acontecer algum erro. 
  numero = int(input("Digite um número: "))
  resultado = 10/numero

except ZeroDivisionError:       # Verificará se o erro gerado foi do tipo ZeroDivisionError.
  print("Erro ao dividir por zero!")

except ValueError:              # Verificará se o erro gerado foi do tipo ValueError.
  print("Digite um número inteiro!")

else:                           # Caso não dê nenhum erro.
  print("O resultado da divisão é {resultado:.2}")

finally:                        # O finally acontece independentemente de haver erros ou não.
  print("Fim da execução.")
```

## **3. Gerando Exceções**
Além de tratar as exceções, o Python assim como outras linguagens, permite também que o programador crie as próprias exceções, isto é, de forma **personalizada**. Isso acontece porque pode haver a necessidade de lidar com situações específicas no código.

**Exemplo** <br>
Imagine que estamos criando uma função chamada divide(a:int, b:int) que recebe dois números inteiros e retorna a/b. Podemos lançar uma exceção personalizada caso o parâmetro B seja incorreto.

```
def divide(a:int, b:int) -> int:
  if b==0:
    raise ZeroDivisionError("Você NÃO pode dividir por zero!")  # O raise não é um print, ele cria uma mensagem de erro.

  return a/b

# Bloco try-except
try:
  resultado = divide(1/0)
except ZeroDivisionError as e: # Aqui estamos apelidando a mensagem do ZeroDivisionError como 'e' e colocando no print.
  print(f"Vish...{e}")
except Exception as e:         # Exception é quando é um erro não especificado, será algo mais geral.
  print(f"Mensagem de erro: e")
else:
  print(f"O resultado da divisão é: {resultado}")

```
## **4. Múltiplas Exceções**
Ao invés de tratar uma exceção por vez, porque poderia ter várias e isso levaria muito tempo, podemos lidar com várias exceções no mesmo bloco except e notificar exceçoes não relacionadas.

Continuando no mesmo exemplo da divisão, imagine que queiramos apenas digitar ao usuário: "Deu erro!"

Para fazer isso, podemos criar um bloco except para cada erro, mas de uma forma mais enxuta e elegante podemos tratar as duas exceções juntas.

```
try:
  resultado = divide(1/0)
except (ZeroDivisionError, ValueError): # Aqui, para qualquer erro especificado dentro da tupla, será escrito "Deu Erro" ao usuário.
  print("Deu erro!")
except Exception as e:
  print(e)
else:
  print(f"O resultado da divisão é: {resultado}")

```
