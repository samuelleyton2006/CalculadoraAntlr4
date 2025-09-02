# 🚀 Guía Completa de ANTLR4

## 📌 ¿Qué es ANTLR4?
ANTLR4 (**ANother Tool for Language Recognition**) es un **generador de analizadores léxicos y sintácticos** muy usado en compiladores, intérpretes y procesamiento de lenguajes formales.  
Permite definir **gramáticas** en un archivo `.g4` y a partir de ellas genera código en múltiples lenguajes de programación (Java, Python, C#, Go, entre otros).

---

## 🛠️ ¿Qué genera ANTLR4?
A partir de una gramática, ANTLR4 produce:
- **Lexer** → se encarga de dividir el texto en tokens (unidades léxicas).  
- **Parser** → organiza los tokens en una estructura jerárquica (árbol sintáctico).  
- **Árbol de análisis (Parse Tree)** → representa la estructura lógica de la entrada.  
- **Visitors / Listeners** → permiten recorrer el árbol y definir la semántica (qué hace el programa con esa estructura).

En pocas palabras: **tomas una gramática, ANTLR4 te entrega código fuente que interpreta y analiza cadenas según esas reglas.**

---

## 📥 Instalación de ANTLR4
1. Descarga el archivo **antlr-4.13.2-complete.jar** desde la página oficial:  
   👉 [https://www.antlr.org/download.html](https://www.antlr.org/download.html)

2. Copia el archivo a `/usr/local/lib`:
   ```bash
   cp /Carpeta_de_descargas/antlr-4.13.2-complete.jar /usr/local/lib


⸻

⚙️ Configuración de ANTLR4 en la Terminal
	1.	Abre el archivo de configuración de tu terminal (.zshrc o .bashrc):

nano ~/.zshrc


	2.	Añade lo siguiente al final del archivo:

# 🔧 Configuración ANTLR4
export CLASSPATH=".:/usr/local/lib/antlr-4.13.2-complete.jar:$CLASSPATH"

# Alias para ejecutar ANTLR4
alias antlr4='java -Xmx500M -cp "$CLASSPATH" org.antlr.v4.Tool'
alias grun='java -Xmx500M -cp "$CLASSPATH" org.antlr.v4.gui.TestRig'


	3.	Guarda los cambios y actualiza la configuración:

source ~/.zshrc



⸻

🧮 Funcionamiento de la Calculadora (Lógica en ANTLR4)

La calculadora se construye a partir de gramáticas que definen:
	1.	La estructura lógica de los programas (parser rules).
	2.	El vocabulario básico (lexer rules o tokens).

📖 Reglas de Parser (Sintaxis)

Ejemplo de gramática para la calculadora:

prog: stat+ ;

stat: expr NEWLINE              # printExpr
    | ID '=' expr NEWLINE       # assign
    | NEWLINE                   # blank
    ;

expr: expr op=('*'|'/'|'%'|'^') expr # Operaciones multiplicativas
    | expr op=('+'|'-') expr        # Operaciones aditivas
    | INT                           # Números enteros
    | ID                            # Variables
    | '(' expr ')'                  # Expresiones entre paréntesis
    ;

🔎 Explicación lógica:
	•	prog → un programa es un conjunto de statements.
	•	stat → un statement puede ser: imprimir una expresión, asignar una variable o estar vacío.
	•	expr → define las expresiones matemáticas, que pueden ser operaciones, números, variables o expresiones agrupadas.

⸻

🔤 Reglas Léxicas (Tokens)

Los tokens definen el alfabeto de la calculadora:

MUL : '*' ;
DIV : '/' ;
MOD : '%' ;
POW : '^' ;
ADD : '+' ;
SUB : '-' ;

INT : [0-9]+ ;
ID  : [a-zA-Z]+ ;
NEWLINE:'\r'? '\n' ;
WS  : [ \t]+ -> skip ;

👉 Aquí se definen los operadores, números y variables que la calculadora reconocerá.

⸻

📌 En conclusión:
La calculadora en ANTLR4 funciona porque:
	1.	El lexer convierte la entrada en tokens (+, *, ID, INT, etc.).
	2.	El parser interpreta la secuencia de tokens según las reglas (expr, stat, prog).
	3.	El árbol de análisis muestra la estructura lógica de la operación.
	4.	Con un Visitor/Listener, se implementa la semántica para realizar los cálculos.

