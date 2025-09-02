# 🚀 Guía de Instalación y Configuración de ANTLR4

## 📥 Instalación
1. Descarga el archivo **antlr-4.13.2-complete.jar** desde la página oficial:  
   👉 [https://www.antlr.org/download.html](https://www.antlr.org/download.html)

2. Copia el archivo descargado a la carpeta `/usr/local/lib`:
   ```bash
   cp /Carpeta_de_descargas/antlr-4.13.2-complete.jar /usr/local/lib


⸻

⚙️ Configuración del Terminal

Debes agregar el classpath en la configuración de tu terminal y definir alias para ejecutar ANTLR4.
	1.	Abre tu archivo de configuración (.zshrc o .bashrc):
``` Terminal 
nano ~/.zshrc
```

	2.	Agrega al final del archivo lo siguiente:

# 🔧 Configuración ANTLR4
export CLASSPATH=".:/usr/local/lib/antlr-4.13.2-complete.jar:$CLASSPATH"

# Alias principales
alias antlr4='java -Xmx500M -cp "$CLASSPATH" org.antlr.v4.Tool'
alias grun='java -Xmx500M -cp "$CLASSPATH" org.antlr.v4.gui.TestRig'


	3.	Guarda y recarga la configuración:
```terminal
source ~/.zshrc

```

⸻

🧮 Uso: Ejemplo de Calculadora

Definimos la gramática con prog, stat y expr:
```
prog: stat+ ;

stat: expr NEWLINE              # printExpr
    | ID '=' expr NEWLINE       # assign
    | NEWLINE                   # blank
    ;

expr: expr op=('*'|'/'|'%'|'^') expr # MulDiv
    | expr op=('+'|'-') expr        # AddSub
    | INT                           # Int
    | ID                            # Id
    | '(' expr ')'                  # Parens
    ;
```
📌 Esta gramática define un conjunto de statements (stat) que permiten:
	•	Asignar variables (ID '=' expr).
	•	Imprimir expresiones.
	•	Saltos de línea en blanco.

Cada expresión puede ser:
	•	Una operación matemática.
	•	Un número entero.
	•	Una variable.
	•	Una subexpresión entre paréntesis.

⸻

🔤 Léxico (Tokens)

El conjunto de reglas léxicas necesarias para la calculadora:

``` antlr
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
```
