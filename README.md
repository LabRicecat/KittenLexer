# KittenLexer
A minimalistic kitten themed lexer

## Example
```cpp
// create a lexer
KittenLexer lexer = KittenLexer()
    .add_capsule('(',')') // ignore text inside `()` and merge them
    .add_ignore(' ') // set whitespaces
    .add_ignore('\t')
    .add_extract('!') // extract `!` as an extra token
    .add_stringq('"') // define string quotes
    .add_stringq('\'')
    .add_linebreak('\n') // define what begins a new line/increases the line counter
    .add_lineskip(';') // comment-like single token
    .add_backslashopt('n','\n') // handle backslashes
    .add_backslashopt('t','\t')
    .erase_empty(); // erase empty tokens

lexed_kittens lexed = lexer.lex("this 'is some' cool text! (It really is!)\nThis is another line!\\nThis isnt?");
```
The tokens you will get back will look like this:
```
string?|line : <text>
0|1 : this
1|1 : is some
0|1 : cool
0|1 : text
0|1 : !
0|1 : (It really is!)
0|2 : This is another line
0|2 : !
0|2 : \nThis
0|2 : isnt?
```