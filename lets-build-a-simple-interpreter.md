<!-- TITLE: Lets Build A Simple Interpreter -->
<!-- SUBTITLE: Note About the online course -->

# Let's Build A Simple Interpreter
> Notes about the online course : [lsbasi](https://ruslanspivak.com/archives.html)

## Terminilogie

* Lexer cut the entry in token.
* Parser transform the tokens in Abstract Syntax Tree.
* Interpreter do action who are represented by the AST's nodes.

## Grammar

### Grammar sample

`expr : factor (( MUL | DIV )factor)*`

`factor : integer`

The line is a rule. The left hand side is 'head' the right hand side is 'body'.

'MUL' is terminal, 'factor' is non terminal.

* `|` represent alternative
* `()` is group
* `()*` is group repeated zero or more time

### Precedence

A rule with priority between the others is called last in the recursive succession of function calls.

## Abstract Syntax Tree (AST)

### Description

An AST is a compact parse tree, where operator are nodes and operand leaf. An operator with higher precedence is lower than the others.


### Syntax Error

### Symbole Table

## Interpreter

### Node Traversal

We use a post order traversal.
