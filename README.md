# Retornando-Propriedades-do-Sistema-Operacional-com-Node.js

Para criar um projeto prático em Node.js que retorna propriedades do sistema operacional, como o uso da memória RAM, vamos seguir alguns passos básicos. Vou criar um servidor simples que, ao receber uma requisição, retorna essas informações.

### Descrição do Projeto:
Desenvolver um servidor em Node.js que forneça informações do sistema operacional, como uso de memória RAM, para clientes que fizerem requisições HTTP.

### Passos para Implementação:

#### Passo 1: Configuração do Projeto
Certifique-se de ter o Node.js instalado. Crie um diretório para o projeto e inicialize um projeto Node.js utilizando o npm (Node Package Manager):

```bash
mkdir sistema-operacional-node
cd sistema-operacional-node
npm init -y
```

#### Passo 2: Instalação de Dependências
Vamos utilizar o pacote `express` para criar o servidor e o pacote `os-utils` para obter informações do sistema operacional:

```bash
npm install express os-utils
```

#### Passo 3: Implementação do Servidor
Crie um arquivo `index.js` para escrever o código do servidor:

```javascript
// index.js
const express = require('express');
const os = require('os-utils');

const app = express();
const port = 3000;

app.get('/', (req, res) => {
    const totalMemory = os.totalmem();
    const freeMemory = os.freemem();
    const usedMemory = totalMemory - freeMemory;
    const memoryUsagePercentage = (usedMemory / totalMemory) * 100;

    res.json({
        totalMemory: `${(totalMemory / 1024).toFixed(2)} MB`,
        freeMemory: `${(freeMemory / 1024).toFixed(2)} MB`,
        usedMemory: `${(usedMemory / 1024).toFixed(2)} MB`,
        memoryUsagePercentage: `${memoryUsagePercentage.toFixed(2)}%`
    });
});

app.listen(port, () => {
    console.log(`Servidor rodando em http://localhost:${port}`);
});
```

#### Passo 4: Executando o Servidor
Para iniciar o servidor, execute o seguinte comando no terminal:

```bash
node index.js
```

#### Passo 5: Testando o Servidor
Abra um navegador ou utilize ferramentas como `curl` ou `Postman` para fazer uma requisição HTTP para `http://localhost:3000/`. Você receberá uma resposta em formato JSON com as informações de uso da memória do sistema.

### Explicação do Código:
- **Express (`const express = require('express')`)**: É um framework para Node.js que simplifica a criação de servidores HTTP.
- **os-utils (`const os = require('os-utils')`)**: É um módulo que fornece funções para acessar informações do sistema operacional.
- **`app.get('/')`**: Define uma rota para o método GET na raiz do servidor. Quando essa rota é acessada, calculamos e retornamos as informações de memória.
- **`os.totalmem()`**: Retorna a quantidade total de memória RAM do sistema em bytes.
- **`os.freemem()`**: Retorna a quantidade de memória RAM livre no sistema em bytes.
- **`res.json({...})`**: Envia uma resposta JSON para o cliente com as informações calculadas.

### Considerações Finais:
Este projeto simples demonstra como utilizar Node.js para criar um servidor que retorna informações do sistema operacional. Podemos expandir este projeto adicionando mais funcionalidades, como retornar informações sobre CPU, espaço em disco, entre outros aspectos do sistema operacional. Isso proporciona uma boa base para explorar mais sobre Node.js e como ele pode ser utilizado para desenvolver aplicações de servidor eficientes e escaláveis.
