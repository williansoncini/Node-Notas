# Bora estudar um Node 📚

E ai beleza? Esse é meu repositório de anotações de node. Sinta-se bem vindo para estudar e contribuir com anotações :3 🚀

# Tópicos

- [Bora estudar um Node 📚](#bora-estudar-um-node-)
- [Tópicos](#tópicos)
- [init](#init)
- [Module](#module)
  - [Exports](#exports)
  - [Import](#import)
  - [__fileName](#__filename)
  - [__dirname](#__dirname)
- [NPM - Node package manager](#npm---node-package-manager)
  - [npm install](#npm-install)
    - [Instalar como depencia](#instalar-como-depencia)
    - [instalar em modo de desenvolvimento](#instalar-em-modo-de-desenvolvimento)
    - [Mudar versões do modulo - Alternar em modulos para desenvolvimento e produção](#mudar-versões-do-modulo---alternar-em-modulos-para-desenvolvimento-e-produção)
    - [npm update](#npm-update)
    - [npm unistall](#npm-unistall)
    - [npm ls](#npm-ls)
    - [npm outdated](#npm-outdated)
- [packge.json](#packgejson)
- [fs - File System](#fs---file-system)
  - [Lendo o conteudo de um arquivo](#lendo-o-conteudo-de-um-arquivo)
  - [Escrevendo conteudo em arquivos](#escrevendo-conteudo-em-arquivos)
  - [Listar arquivos em pastas](#listar-arquivos-em-pastas)
  - [caminhando nas pastas](#caminhando-nas-pastas)
  - [Lendo pastas](#lendo-pastas)
- [Express](#express)
  - [instalação](#instalação)
  - [Configuração padrão](#configuração-padrão)
  - [Requisições básicas](#requisições-básicas)
  - [Requisições com parametros](#requisições-com-parametros)
  - [Requisições com query](#requisições-com-query)
  - [Requisições com body](#requisições-com-body)
  - [Rotas](#rotas)
  - [Controllers](#controllers)
  - [Express Views](#express-views)
    - [Instalação ejs](#instalação-ejs)
    - [Configuração básica](#configuração-básica)
    - [Arquivo da view - index.ejs](#arquivo-da-view---indexejs)
    - [Rendezirar uma view](#rendezirar-uma-view)
  - [Arquivos estáticos](#arquivos-estáticos)
  - [Express middleware](#express-middleware)
    - [Middleware](#middleware)
    - [Global middleware](#global-middleware)
- [Nodemon](#nodemon)
  - [instalação](#instalação-1)
  - [configuração package.json](#configuração-packagejson)

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

# Express

## instalação

```js
npm i express
```

## Configuração padrão

```js
const express = require('express')
const app = express()

app.liste(port_number, () => console.log('O pai ta on!'))
```

## Requisições básicas

```js
const express = require('express')
const app = express()

app.get('/route', (req, res) => { })
app.post('/route', (req, res) => { })
app.put('/route', (req, res) => { })
app.delete('/route', (req, res) => { })

app.listen(port_number, () => console.log('O pai ta on!'))
```

## Requisições com parametros

> Pode-se incluir um ? para indicar como parametro opcional

```js
const express = require('express')
const app = express()

app.get('/:parameter', (req, res) => {
  console.log(req.params)
  console.log(req.params.parameter)
})
//Exemplo parametro opcional
app.get('/:parameter?', (req,res) => {} )
app.listen(port_number, () => console.log('O pai ta on!'))
```

## Requisições com query

```js
const express = require('express')
const app = express()

// url: http://localhost:3000/?teste_um=valor_um&teste_dois=valor_dois

app.get('/', (req, res) => {
  console.log(req.query) // { teste_um : valor_um, teste_dois: valor_dois}
  console.log(req.query.teste_um) // valor_um
})

app.listen(port_number, () => console.log('O pai ta on!'))
```

## Requisições com body

```js
const express = require('express')
const app = express()

app.use(express.urlencoded({extended: true}))

//body enviado: {teste: 'teste'}

app.post('/route', (req, res) => {
  console.log(req.body) // { teste: 'teste'}
  console.log(req.body.teste)
})
```

## Rotas 

Escopo básico de um arquivo de rotas

```js
const express = require("express")
const router = express.Router()

router.get('/', homeController.homePage)

module.exports = router
```

## Controllers

Escopo básico de arquivo controlador

```js
exports.homeController = (req, res) => {
  //logic
  res.send('Mensagem')
}
```

## Express Views

Views são utilizadas para renderizar templates html

> Existem várias engines que podem ser utilizadas

### Instalação ejs

```js
npm i ejs
```

### Configuração básica

```js
const path = require('path')
const express = require('express')
const app = express()


// Setar o local que ficaram as views. 
// app.set('views', './path/views')
// Para uma melhor segurança é melhor utilizadar path.resolve
app.set('views', path.resolve(__dirname, 'src', 'views'))

// Setar qual view engine será utilizada
app.set('view engine', 'ejs')
```

### Arquivo da view - index.ejs

É um tipo de arquivo que aceita HTML e trechos JavaScript

> A extensão do arquivo deve ter .ejs

### Rendezirar uma view

```js
exports.homePage = (req, res) => {
  res.render('index')
}
```

## Arquivos estáticos

Podemos definir uma pasta para os arquivos estáticos da aplicação

```js
const path = require('path')
const express = require('express')
const app = express()

app.use(express.static(__dirname, 'public'))
// app.use(express.static('./public'))
```

## Express middleware

Um middleware é um intermediario que acontece quando você recebe uma requisição. Pode ser um middleware checando se o usuário está logado ou se o usuário tem permissão para realizar oque está requisitando

> Middlewares tem a função next, que permite passar para a próximo middleware ou controller.

> Pode exister mais de um middleware

### Middleware

```js
const express = require('express')
const app = express()

const middleware = (req, res, next) => {
  console.log('Sou um middleware')
  next()
}

app.get('/', middleware, homeController.homePage)

app.listen(3000)
```

### Global middleware

Quando configurado, todas as requisições vão passar por este middleware

```js
const express = require('express')
const app = express()

const middleware = (req, res, next) => {
  //logic
  next()
}

app.use('middleware', middleware)

app.get('/', homeControlle.homePage) // Ira passar pelo middleware global

app.listen(3000)
```

# Nodemon

Usado em ambiante de desenvolvimento para tornar automatico o reload do node.

## instalação

```js
npm i nodemon --save-dev
```

## configuração package.json

```json
"scripts": {
  "start" : "npx nodemon server.js"
}
```
