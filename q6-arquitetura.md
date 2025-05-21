De modo abstrato, o compilador é um programa que converte código de uma
linguagem para outra. Como se fosse uma função do tipo `compilador(str) -> str`.
No caso de compiladores que emitem código de máquina ou bytecode, seria mais
preciso dizer `compilador(str) -> bytes`, mas a idéia básica é a mesma.

De forma geral o processo é dividido em etapas como abaixo

```python
def compilador(x1: str) -> str | bytes:
    x2 = lex(x1)        # análise léxica
    x3 = parse(x2)      # análise sintática
    x4 = analysis(x3)   # análise semântica
    x5 = optimize(x4)   # otimização
    x6 = codegen(x5)    # geração de código
    return x6
```

Defina brevemente o que cada uma dessas etapas realizam e marque quais seriam os
tipos de entrada e saída de cada uma dessas funções. Explique de forma clara o
que eles representam. Você pode usar exemplos de linguagens e/ou compiladores
conhecidos para ilustrar sua resposta. Salve sua resposta nesse arquivo.

# lex(texto contendo código na linguagem a ser compilada) -> lista de lexemas (tokens) obtidos do texto
Essa etapa é responsável por quebrar o conteúdo do texto nos lexemas esperados para a linguagem de entrada. Também é nessa etapa em que se verifica se foram usados caracteres não existentes ou inválidos.
 
# parse(tokens) -> árvore sintática abstrata AST
Essa etapa é responsável por sintetizar a sequência de tokens em uma estrutura lógica chamada árvore de sintaxe. Essa estrutura representa como o código deve ser "lido" pelas próximas etapas, representando
ordem de precedência de operações, chamadas e seus argumentos, estruturas e seus itens, variáveis e seus
valores, funções e seus argumentos, assim por diante. Essa etapa também verifica se os tokens não estão
sendo usados de maneira "errada", análogo a um erro de escrita no português.

# analysis(AST) -> Código intermediário
Essa etapa é responsável por verificar se a estrutura da árvore de sintaxe é válida, verificando tipos,
verificando se está logicamente correto, etc. A saída é o equivalente aos arquivos .o da linguagem C.
Nessa etapa que o borrow checker do Rust mais reclama.

# optimize(Código intermediário) -> Código intermediário otimizado
Essa etapa realiza otimizações como substituir funções inline, desempacotar (unwrap?) os loops, simplificar
operações matemáticas, etc.

# codegen(Código intermediário) -> Código binário
Essa etapa converte o código otimizado em um executável.