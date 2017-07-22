.. title: HolaMundo con ethereum
.. slug: holamundo-ethereum
.. date: 2017-07-18 23:00:00 UTC-06:00
.. tags: ethereum, jaquerespeis, smart contracts
.. author: Alvaro Segura Del Barco, Edgar Barrantes Brais
.. link: https://getnikola.com/
.. description: Como hacer un simple contrato inteligente
.. category: guias

# Lista de herramientas
* testRPC
* nvm
* web3
* geth
* solc
* web3

# Instalación

## Linux

Los siguientes pasos muestras como instalar las herramientas necesarias en Ubuntu 17.04

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
nvm ls-remote
nvm install <la ultima LTS>
npm install -g ethereumjs-testrpc
npm install solc
npm install web3

```
## Mac

Para instalar nvm es necesario tener [brew](https://brew.sh/)

```
brew install nvm
nvm ls-remote
nvm install <la ultima LTS>
npm install -g ethereumjs-testrpc
npm install solc
npm install web3

```
# Desarrollo

Con el editor preferido, escribir el contrato, para esto se va a utilizar el lenguage [**solidity**](https://solidity.readthedocs.io/en/develop/), sin embargo existen otras opciones como [**serpent**](https://github.com/ethereum/wiki/wiki/Serpent).

Para compilar el contrato vamos a utilizar el comando `solc --bin --optimize <archivo.sol>`

Escribit el siguiente contrato en un archivo llamado Voting.sol

```solidity
pragma solidity ^0.4.11;
// We have to specify what version of compiler this code will compile with

contract Voting {
  /* mapping field below is equivalent to an associative array or hash.
  The key of the mapping is candidate name stored as type bytes32 and value is
  an unsigned integer to store the vote count
  */
  
  mapping (bytes32 => uint8) public votesReceived;
  
  /* Solidity doesn't let you pass in an array of strings in the constructor (yet).
  We will use an array of bytes32 instead to store the list of candidates
  */
  
  bytes32[] public candidateList;

  /* This is the constructor which will be called once when you
  deploy the contract to the blockchain. When we deploy the contract,
  we will pass an array of candidates who will be contesting in the election
  */
  function Voting(bytes32[] candidateNames) {
    candidateList = candidateNames;
  }

  // This function returns the total votes a candidate has received so far
  function totalVotesFor(bytes32 candidate) returns (uint8) {
    if (validCandidate(candidate) == false) throw;
    return votesReceived[candidate];
  }

  // This function increments the vote count for the specified candidate. This
  // is equivalent to casting a vote
  function voteForCandidate(bytes32 candidate) {
    if (validCandidate(candidate) == false) throw;
    votesReceived[candidate] += 1;
  }

  function validCandidate(bytes32 candidate) returns (bool) {
    for(uint i = 0; i < candidateList.length; i++) {
      if (candidateList[i] == candidate) {
        return true;
      }
    }
    return false;
  }
}
```

## Pasos para desplegar el contrato
*Ejecutar node*

Mientras se ejecutan los comandos, se puede ver su salida y analizarla.

```javascript
Web3 = require('web3')
web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
```

Listar las cuentas existentes en la red
```javascript
web3.eth.accounts
```
Compilar el código 
```javascript
code = fs.readFileSync('Voting.sol').toString()
solc = require('solc')
compiledCode = solc.compile(code)
```

```javascript
abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface)
VotingContract = web3.eth.contract(abiDefinition)
byteCode = compiledCode.contracts[':Voting'].bytecode
deployedContract = VotingContract.new(['Rama','Nick','Jose'],{data: byteCode, from: web3.eth.accounts[0], gas: 4700000})
deployedContract.address
contractInstance = VotingContract.at(deployedContract.address)
```

```javascript
> contractInstance.totalVotesFor.call('Rama')

{ [String: '0'] s: 1, e: 0, c: [ 0 ] }

> contractInstance.voteForCandidate('Rama', {from: web3.eth.accounts[0]})

'0xdedc7ae544c3dde74ab5a0b07422c5a51b5240603d31074f5b75c0ebc786bf53'

> contractInstance.voteForCandidate('Rama', {from: web3.eth.accounts[0]})

'0x02c054d238038d68b65d55770fabfca592a5cf6590229ab91bbe7cd72da46de9'

> contractInstance.voteForCandidate('Rama', {from: web3.eth.accounts[0]})

'0x3da069a09577514f2baaa11bc3015a16edf26aad28dffbcd126bde2e71f2b76f'

> contractInstance.totalVotesFor.call('Rama').toLocaleString()

'3'
```

# Opcodes de la EVM

## 0s: Stop and Arithmetic Operations
```
0x00    STOP        Halts execution
0x01    ADD         Addition operation
0x02    MUL         Multiplication operation
0x03    SUB         Subtraction operation
0x04    DIV         Integer division operation
0x05    SDIV        Signed integer
0x06    MOD         Modulo
0x07    SMOD        Signed modulo
0x08    ADDMOD      Modulo
0x09    MULMOD      Modulo
0x0a    EXP         Exponential operation
0x0b    SIGNEXTEND  Extend length of two's complement signed integer
```
## 10s: Comparison & Bitwise Logic Operations
```
0x10    LT      Lesser-than comparison
0x11    GT      Greater-than comparison
0x12    SLT     Signed less-than comparison
0x13    SGT     Signed greater-than comparison
0x14    EQ      Equality  comparison
0x15    ISZERO  Simple not operator
0x16    AND     Bitwise AND operation
0x17    OR      Bitwise OR operation
0x18    XOR     Bitwise XOR operation
0x19    NOT     Bitwise NOT operation
0x1a    BYTE    Retrieve single byte from word
```
## 20s: SHA3
```
0x20    SHA3    Compute Keccak-256 hash
```
## 30s: Environmental Information
```
0x30    ADDRESS         Get address of currently executing account
0x31    BALANCE         Get balance of the given account
0x32    ORIGIN          Get execution origination address
0x33    CALLER          Get caller address. This is the address of the account that is directly responsible for this execution
0x34    CALLVALUE       Get deposited value by the instruction/transaction responsible for this execution
0x35    CALLDATALOAD    Get input data of current environment
0x36    CALLDATASIZE    Get size of input data in current environment
0x37    CALLDATACOPY    Copy input data in current environment to memory This pertains to the input data passed with the message call instruction or transaction
0x38    CODESIZE        Get size of code running in current environment
0x39    CODECOPY        Copy code running in current environment to memory
0x3a    GASPRICE        Get price of gas in current environment
0x3b    EXTCODESIZE     Get size of an account's code
0x3c    EXTCODECOPY     Copy an account's code to memory
```
## 40s: Block Information
```
0x40    BLOCKHASH   Get the hash of one of the 256 most recent complete blocks
0x41    COINBASE    Get the block's beneficiary address
0x42    TIMESTAMP   Get the block's timestamp
0x43    NUMBER      Get the block's number
0x44    DIFFICULTY  Get the block's difficulty
0x45    GASLIMIT    Get the block's gas limit
```
## 50s Stack, Memory, Storage and Flow Operations
```
0x50    POP         Remove item from stack
0x51    MLOAD       Load word from memory
0x52    MSTORE      Save word to memory
0x53    MSTORE8     Save byte to memory
0x54    SLOAD       Load word from storage
0x55    SSTORE      Save word to storage
0x56    JUMP        Alter the program counter
0x57    JUMPI       Conditionally alter the program counter
0x58    PC          Get the value of the program counter prior to the increment
0x59    MSIZE       Get the size of active memory in bytes
0x5a    GAS         Get the amount of available gas, including the corresponding reduction
0x5b    JUMPDEST    Mark a valid destination for jumps
```
## 60s & 70s: Push Operations
```
0x60    PUSH1   Place 1 byte item on stack
0x61    PUSH2   Place 2-byte item on stack
…
0x7f    PUSH32  Place 32-byte (full word) item on stack
```
## 80s: Duplication Operations
```
0x80    DUP1    Duplicate 1st stack item
0x81    DUP2    Duplicate 2nd stack item
…
0x8f    DUP16   Duplicate 16th stack item
```
## 90s: Exchange Operations
```
0x90    SWAP1   Exchange 1st and 2nd stack items
0x91    SWAP2   Exchange 1st and 3rd stack items
…   …
0x9f    SWAP16  Exchange 1st and 17th stack items
```
## a0s: Logging Operations
```
0xa0    LOG0    Append log record with no topics
0xa1    LOG1    Append log record with one topic
…   …
0xa4    LOG4    Append log record with four topics
```
## f0s: System operations
```
0xf0    CREATE          Create a new account with associated code
0xf1    CALL            Message-call into an account
0xf2    CALLCODE        Message-call into this account with alternative account's code
0xf3    RETURN          Halt execution returning output data
0xf4    DELEGATECALL    Message-call into this account with an alternative account's code, but persisting the current values for `sender` and `value`
```
## Halt Execution, Mark for deletion
```
0xff    SELFDESTRUCT    Halt execution and register account for later deletion
```

# Referencias

* https://github.com/creationix/nvm
* https://github.com/ethereumjs/testrpc
* https://en.wikipedia.org/wiki/Remote_procedure_call
* http://ethdocs.org/en/latest/network/test-networks.html
* https://medium.com/@doart3/ethereum-dapps-without-truffle-compile-deploy-use-it-e6daeefcf919
* https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2
* https://github.com/ethereum/yellowpaper

# Notas
testrpc -n5

