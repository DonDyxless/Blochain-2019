class Block {
    constructor(timestamp = "", data = []) {
        this.timestamp = timestamp;
        // в this.data должна содержаться информация наподобие сведений о транзакциях.
        this.data = data;
    }
}
const crypto = require("crypto"), SHA256 = message => crypto.createHash("sha256").update(message).digest("hex");
const crypto = require("crypto"), SHA256 = message => crypto.createHash("sha256").update(message).digest("hex");

class Block {
    constructor(timestamp = "", data = []) {
        this.timestamp = timestamp;
        this.data = data;
        this.hash = this.getHash();
        this.prevHash = ""; // хеш предыдущего блока
    }

    // Наша хеш-функция.
    getHash() {
        return SHA256(this.prevHash + this.timestamp + JSON.stringify(this.data));
    }
}
class Blockchain {
    constructor() {
        // В этом свойстве будут содержаться все блоки.
        this.chain = [];
    }
}
class Blockchain {
    constructor() {
        // Создаём первичный блок
        this.chain = [new Block(Date.now().toString())];
    }
}
 getLastBlock() {
        return this.chain[this.chain.length - 1];
    }
    addBlock(block) {
        // Так как мы добавляем новый блок, prevHash будет хешем предыдущего последнего блока
        block.prevHash = this.getLastBlock().hash;
        // Так как теперь в prevHash имеется значение, нужно пересчитать хеш блока
        block.hash = block.getHash();
        this.chain.push(block);
    }
    isValid() {
        // Перед перебором цепочки блоков нужно установить i в 1, так как до первичного блока никаких блоков нет. В результате мы начинаем со второго блока.
        for (let i = 1; i < this.chain.length; i++) {
            const currentBlock = this.chain[i];
            const prevBlock = this.chain[i-1];

            // Проверка
            if (currentBlock.hash !== currentBlock.getHash() || prevBlock.hash !== currentBlock.prevHash) {
                return false;
            }
        }

        return true;
    }
    class Block {
    constructor(timestamp = "", data = []) {
        this.timestamp = timestamp;
        this.data = data;
        this.hash = this.getHash();
        this.prevHash = ""; // хеш предыдущего блока
        this.nonce = 0;
    }

    // Наша хеш-функция.
    getHash() {
        return SHA256(this.prevHash + this.timestamp + JSON.stringify(this.data) + this.nonce);
    }

    mine(difficulty) {
        // Тут запускается цикл, работающий до тех пор, пока хеш не будет начинаться со строки 
        // 0...000 длины <difficulty>.
        while (!this.hash.startsWith(Array(difficulty + 1).join("0"))) {
            // Инкрементируем nonce, что позволяет получить совершенно новый хеш.
            this.nonce++;
            // Пересчитываем хеш блока с учётом нового значения nonce.
            this.hash = this.getHash();
        }
    }
}
this.difficulty = 1;
addBlock(block) {
        block.prevHash = this.getLastBlock().hash;
        block.hash = block.getHash();
        block.mine(this.difficulty);
        this.chain.push(block);
    }
module.exports = { Block, Blockchain };
const { Block, Blockchain } = require("./your-blockchain-file.js");

const JeChain = new Blockchain();
// Добавим новый блок
JeChain.addBlock(new Block(Date.now().toString(), { from: "John", to: "Bob", amount: 100 }));
// (Это - всего лишь интересный эксперимент, для создания настоящей криптовалюты обычно нужно сделать намного больше, чем сделали мы).

// Вывод обновлённого блокчейна
console.log(JeChain.chain);
 addBlock(block) {
        block.prevHash = this.getLastBlock().hash;
        block.hash = block.getHash();
        block.mine(this.difficulty);
        this.chain.push(block);

        this.difficulty += Date.now() - parseInt(this.getLastBlock().timestamp) < this.blockTime ? 1 : -1;
    }
