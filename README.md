C_Interpreter
=============


This started as C port of an old college assignment
in C++.  You can see that in the first commit though I
might have made some minor changes/improvements during
port.

The tests have been updated to match the current
state but not to extensively test the new functionality.
I'll get to thatI'll get to that.

Now my goal is to make something approaching scriptable
C.  I'll consider it done when it can run itself ...
so it'll probably never be completely done.

I'm using the 5th edition of C A Reference Manual for
all the nitty gritty details and the very convenient
complete C grammar/syntax in the appendix.

The grammar below is the current status more or less.
It'll be interesting to see how it grows and which
parts converge with full syntax first. 

I've also added a BNF spec for C I found online just
to have something for reference in the repository.


Current Grammar (work in progress)
==================================
```

program                   -> declaration_list body

declaration_list          -> declaration
                          -> declaration_list declaration

declaration               -> declaration_specifier initialized_declarator_list ';'

initialized_declarator_list     -> initialized_declarator
                                   initialized_declarator_list ',' initialized_declarator

initialized_declarator    -> identifier
                          -> identifier '=' assign_expr

declaration_specifier     -> int

body                      -> '{' stmt_list '}'

stmt_list                 -> expr_stmt
                             while_stmt
                             if_stmt
                             print_stmt
                             goto_stmt

while_stmt                -> while expr body
if_stmt                   -> if expr body
print_stmt                -> print identifier ';'

goto_stmt                 -> goto identifier ';' //unfinished

expr_stmt                 -> expr ';'

expr                      -> comma_expr

comma_expr                -> assign_expr
                             assign_expr ',' assign_expr

assign_expr               -> cond_expr
                          -> identifier assign_op assign_expr

assign_op                 -> one of '=' '+=' '-=' '*=' '/=' '%='

cond_expr                 -> logical_or_expr  //could add ternary here

logical_or_expr           -> logical_and_expr
                             logical_or_expr '||' logical_and_expr

logical_and_expr          -> equality_expr
                             logical_and_expr '&&' equality_expr

equality_expr             -> relational_expr
                             equality_expr '==' relational_expr
                             equality_expr '!=' relational_expr

relational_expr           -> add_expr
                             relational_expr relational_op add_expr

relational_op             -> one of '<' '>' '<=' '>='

add_expr                  -> mult_expr
                             add_expr add_op mult_expr

add_op                    -> one of '+' '-'

mult_expr                 -> primary_expr
                             mult_expr mult_op primary_expr

mult_op                   -> one of '*' '/' '%'

primary_expr              -> identifier
                             constant
                             '(' expr ')'
```
