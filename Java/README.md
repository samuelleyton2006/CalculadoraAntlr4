## Compilamos la gramatica g4 
```bash
antlr4 -visitor LabeledExpr.g4
```
La flag -visitor, permite que antlr, ademas de compilar el parser y el scanner, permite la creacion de las interfaces para utilizar con EvalVisitor
## Compilamos los archivos .java
```bash
javac -cp .:antlr-4.13.2-complete.jar *.java
```
## Ejecutamos el main class y agregamos el input

```bash
java -cp .:antlr-4.13.2-complete.jar Calc input.txt
```
