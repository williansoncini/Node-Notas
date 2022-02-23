# Bora estudar um Node 📚

E ai beleza? Esse é meu repositório de anotações de node. Sinta-se bem vindo para estudar e contribuir com anotações :3 🚀

# init

Inicializar o package.json

```js
npm init
npm init -y // Parar criar o package.json com as configurações padrões
```

# Module

Objeto do Node

## Exports

Exportação de dados de um arquivo pelo Node. Assim outro arquivo pode usar os dados, como classes ou objetos.

```js
module.exports.name('Name') // { name : 'Nome' }
exports.name('Name') // { name : 'Nome' }
module.exports = { name : 'name', }
//exemplo
module.exports = () => consol.log('É só me importar e usar')
```

> Exports é uma referencia a module.exports

É possível fazer a exportação utilizando o this, pois ele também faz referencia ao module.exports

```js
this.name = 'Name'

console.log(module.exports) // { name : 'Name'}
```

## Import

> Pode se utilizar o caminho absoluto, quanto o caminho completo

> na navegação de pastas utilize . para ir para frente e .. para voltar a pasta

```js
const module_imported = require('./file.js') // Pode ou não conter .js
const module_imported = require('./file')
const name = require('../../path/file').name //Importar somente o nome
const {name} =  require('./file')
```

## __fileName

Variavel padrão do node

> Retorna o caminho absoluto do arquivo

## __dirname

Variavél padrão do nome

> Retorna o caminho absoluto da pasta


# NPM - Node package manager

Gerenciador de pacotes do node

## npm install

Instalar pacotes de terceiros em sua aplicação

### Instalar como depencia

```js
npm install express
npm i express
npm i express -E // Para sempre baixar sempre a versão informatada do modulo - No caso vai pegar sempre a verão que está sendo utilizado atualmente. Mas não pegara as versões futuras
npm i express@version // Instalar versão expecifica

npm i pacote_1 pacote_2 pacote_3
```

### instalar em modo de desenvolvimento

Em modo de desenvolvimento não vai para produção

> a flag --dev permite realizar essa instalação

```js
npm install express --dev
npm i express --dev
```

### Mudar versões do modulo - Alternar em modulos para desenvolvimento e produção

```js
npm i express --save-prod // Salvar em produção
npm i express --save-dev // Salvar em desenvolvimento
```

### npm update

Atualizar pacote

```js
npm update // atualizar versão dos modulos de terceiros ( Que permitirem serem atualizados - Estiverem com ^informando sua versão)
```

### npm unistall

Desinstalar pacote

```js
npm unistall express
```

### npm ls

Listar pacotes instalados

```js
npm ls
npm ls -deph=0 // Para limitar a profundidade das pastas na listagem
```

### npm outdated

Listar pacotes desatualizados

```js
npm outdated 
```


# packge.json

> ^ na frente de uma dependencia, significa que essa dependencia sempre pegara a versão mais atual do modulo do terceiro

> Para sempre usar uma versão expecifica utilize apenas o número da versão

> ^ Permite atualizar as versões MINOR e PATCH, não atualizado somente a versão MAJOR - Sequencia MAJOR.MINOR.PATCH, exemplo: 2.1.1

> ~ Permite ataulizar somente a versão PATCH

```json
{
  "name": "name",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies":{
      "express": "^4.0.0" // Atualiza as versões MINOR.PATCH
    //   "express": "~4.0.0" // Atualiza a versão PATCH
    //   "express": "4.0.0" // Não atualiza versão
  }
}
```

# fs - File System

```js
const fs = require('fs')
const fs = require('fs').promises
```

> Aqui quase sempre se usa `require('fs').promises` por conta de podermos aguarda o nosso comando ser executado, forçando um funcionamento assincrono.

## Lendo o conteudo de um arquivo

```js
const fs = require('fs').promises
fs.readFile('pathFile', 'utf8')
```

## Escrevendo conteudo em arquivos

> As flags indicam como o arquivo sera escrito

> w - Ira apagar todo conteudo do arquivo e inserir o conteudo que está passando no wrileFile

> a - Append - Irá incluir o conteudo que você está passando, mantendo o conteudo atual

```js
const fs = require('fs').promises
const path = require('path')

const caminhoArquivo  = path.resolve(__dirname, 'filename.txt')

fs.writeFile(caminhoArquivo, 'Texto', {flag: 'w'})
```

## Listar arquivos em pastas

```js
const fs = require('fs').promises
const path = require('path')

fs.readdir(path.resolve(__dirname))
    .then(files => console.log(files))
    .catch(e => console.log(e))
```

## caminhando nas pastas

Voltar duas pastas, independente do sistema operacional

```js
const path = require('path').promises
path.resolve(__dirname, '..', '..', '..')
```

## Lendo pastas

```js
const fs = require('fs').promises
const path = require('path')

const files = fs.readdir(__dirname) // arquivos da pasta
```

