# Intro to Script

### Script

Official Definition: stack-based programming language used to make locks and undo those locks in bitcoin.
scriptSig and the scriptPubKey "yin and yang" scripts.
script: \<scriptSig\> \<scriptPubKey\>

[Script](https://en.bitcoin.it/wiki/Script) is a stack based language. Script consists of data and opcodes. Data elements are sequentially pushed from the completed script, scriptSig then script PubKey, onto the stack. op_codes perform operations on data.

Data fields will always be preppended with an OP_PUSHBYTES for the data field size. This OP_PUSHBYTES is similar in concept to compact field sizes, but is a little different. Op_codes are 1 byte with a special meaning and perform operations on the data fields like OP_EQUAL which evaluates true/false whether 2 data fields are equal. There's a set number of op_codes, each maps to an "operation" that does stuff with the stack.

The single best resource for visualizing this process is [learnmeabitcoin.com(learnmeabitcoin.com/technical/script) . We highly recommend you read through that link and look at the various visualized scripts to see how script is evaluated as a stack based programming language.

### Validation Rules:

A script is valid if 
```
The top and only element left on the stack after evaluation is a truthy value (a data element greater than or equal to 1).
```

A script is invalid if 

    1. The stack is falsey after execution of the script, either empty or a 0.
    2. There is more than one element left on the stack at the end of execution.
    3. Or the script exits prematurely, by failing an OP_EQUAL for example.

## Exercise
We've written 3 custom scripts in the scripts.py file. For each script, 

    1. Translate the Script into human readable assembly like nifty did in class. e.g. '0101ac' translates to '01 OP_CHECKSIG'. 

Try doing the first one by hand using this wiki page https://en.bitcoin.it/wiki/Script to look up the op_codes yourself. 
For the latter 2, use the bitcoind and bitcoin-cli we set up in this repl to get the software to decode it for you. In the shell, start up a background regtest process with `bitcoind -regtest -daemon`. Then run `bitcoin-cli -regtest -decodescript your_hex_here`

    2. Write out a walkthrough of the script's stack evaluation and answer whether it evaluates to true. If it does not, answer where in the script the evaluation would end. (e.g. does it make it through to the end of the script? or does it exit early?)

### Extra Credit
In the 1 TX that fails evaluation before finishing the script, what's the 1 OP_CODE I can change which would make it not only finish evaluation, but evaluate to true? (Hint: what's the difference between OP_EQUAL & OP_EQUALVERIFY?)