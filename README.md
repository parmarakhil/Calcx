# Calcx

This is an extension of interepter for CalcZeta language written in java. 
Keyword in CalcZeta language are written entirely in UPPER CASE eg : INT whereas variables are written in lower case eg: foo.
White spaces like space, tab, new line are ignored.

Currently it supports only following data types
- INT

Variables and their type must be declared first and assigned a value. A semi-colon is used after declaration of each variable. 
You can't declare variables with same name more than once. 
Currenlty the language doesn't allow user inputs, all variables must me declared within the program directly

Supported operations are
- addition (+)
- subtraction (-)
- Modulo (%)

There are no precedence of operation other than expressions are evaluated right to left for the binary operations '+' and '-'. 
eg: expression 'x+y-z+y' will ve evaluated as 'x+(y-(z+y)).
There are no parenthesis support currently

A program (prog) in CalcZeta is made up of declarations (decls), with each declaration (decl) being a single
variable, which is assigned a unsigned integer value. The assignment operator is denoted ‘=’.
Each declaration is ended by a semicolon ‘;’. After the declarations, we have a colon character ‘:’ followed
by a single expression (expr).

An expression (expr) is a sequence of lexemes, each of which is a variable name or an operation, written
in infix notation (for example x+y-z+x). Therefore, each operation has a variable on its left and right.
At the end of the expression is a single ‘$’ character to denote the end of the
‘program’. An expression produces a signed (i.e. positive or negative) integer as the output of the program.

The following is an example valid program written in Calclnt.
INT x=7; INT y=3; : x+x-y$

The output of the program is to evaluate the expression according to the precedence rules explained
earlier (right-to-left only). So for example, the program just written would produce output “11”, since
7+(7-3) is 11. Remember that $ denotes the end of the program and does not affect the output.

We now give a Context Free Grammar (CFG) for CalcINT.
                prog    ->   decls ‘:’ expr ‘$’
                decls   ->   decl decls
                        |   €
                del     ->  ‘INT’ var ‘=’ intnum ‘;’
                expr    ->  var op expr
                        |   var
                var     ->  [a-z]+
                intnum  ->  [-]?[0-9][0-9]*
                op      ->  '+'|'-'

For example, a program (prog) is made up of declarations (decls), followed by a colon, followed by an
expression (expr), followed by a dollar symbol etc.

We may also write this as a Syntax Directed Translation Scheme (SDTS) by adding semantic actions to
be carried out at each stage of parsing
                prog    ->  decls ‘:’ expr ‘$’              { Print expr.val(); }
                decls   ->  decl decls
                        |    €
                del     ->  ‘INT’ var ‘=’ intnum ‘;’        { var.val() = intnum.val(); }
                expr    ->  var Op expr2                    { expri.val() = var.val() op expr2.val(); }
                        |   var                             { expri.val() = var.val(); }
                var     ->  [a-z]+
                intnum  ->  [-]?[0-9][0-9]*
                op      ->  '+' | '-'
                
#### Activity Diagram
<p>  <img src="https://github.com/parmarakhil/Calcx/blob/main/Activity%20Diagram.png" alt=“activity diagram” /></p>
