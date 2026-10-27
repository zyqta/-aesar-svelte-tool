<script>
    let activeContent = $state("encryption");
    let encryptedText = $state([]);
    let decryptedText = $state([]);
    const alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZÆØÅ".split("");
    let keyLetter = $state("A");
    let encryptionCipher = $state("ceaser-cipher");
    let decryptionCipher = $state("ceaser-cipher");
    function showContent(element) {
        activeContent = element;
    }
    function GetEncryptText() {
        if (encryptionCipher === "vigenere-cipher") {
            GetVigenereEncryptText();
        } else if (encryptionCipher === "one-time-pad") {
            GetOneTimePadEncryptText();
        } else {
            GetCaesarEncryptText();
        }
    }
    function GetDecryptText() {
        if (decryptionCipher === "vigenere-cipher") {
            GetVigenereDecryptText();
        } else if (decryptionCipher === "one-time-pad") {
            GetOneTimePadDecryptText();
        } else {
            GetCaesarDecryptText();
        }
    }
    function GetCaesarEncryptText() {
        let keyIndex = alphabet.indexOf(keyLetter.toLocaleUpperCase());
        let inputText = document.getElementById("input-encryption").value.toUpperCase();
        document.getElementById("result-encryption").innerText = inputText.trim();
        let text = inputText.split("");
        let newText = [];
        for (let i in text){
            let letterKey = alphabet.indexOf(text[i])
            newText.push(alphabet[letterKey + keyIndex])
        }
        encryptedText.push(newText.join(""));
        
    }
    function GetCaesarDecryptText() {
        let keyIndex = alphabet.indexOf(keyLetter.toLocaleUpperCase());
        let inputText = document.getElementById("input-decryption").value.toUpperCase();
        document.getElementById("result-decryption").innerText = inputText.trim();
        let text = inputText.split("");
        let newText = [];
        for (let i in text){
            let letterKey = alphabet.indexOf(text[i])
            newText.push(alphabet[letterKey - keyIndex])
        }
        decryptedText.push(newText.join(""));
    }
    function GetVigenereEncryptText() {
        let keyText = document.getElementById("input-key-encryption").value.toUpperCase();
        let key = keyText.split("");
        let inputText = document.getElementById("input-encryption").value.toUpperCase();
        document.getElementById("result-encryption").innerText = inputText.trim();
        let text = inputText.split("");
        let newText = [];
        let keyPosition = 0;
        for (let i in text) {
            let letterKey = alphabet.indexOf(text[i]);
            if (letterKey === -1) {
                newText.push(text[i]);
            }
            else {
                let keyIndex = alphabet.indexOf(key[keyPosition % key.length]);
                newText.push(alphabet[(letterKey + keyIndex) % alphabet.length]);
                keyPosition++;
            }
        }
        encryptedText.push(newText.join(""));
    }
    function GetVigenereDecryptText() {
        let keyText = document.getElementById("input-key-decryption").value.toUpperCase();
        let key = keyText.split("");
        let inputText = document.getElementById("input-decryption").value.toUpperCase();
        document.getElementById("result-decryption").innerText = inputText.trim();
        let text = inputText.split("");
        let newText = [];
        let keyPosition = 0;
        for (let i in text) {
            let letterKey = alphabet.indexOf(text[i]);
            if (letterKey === -1) {
                newText.push(text[i]);
            }
            else {
                let keyIndex = alphabet.indexOf(key[keyPosition % key.length]);
                newText.push(alphabet[(letterKey - keyIndex + alphabet.length) % alphabet.length]);
                keyPosition++;
            }
        }
        decryptedText.push(newText.join(""));
    }
    function GetOneTimePadEncryptText() {
        //let keyLetter = Math.floor(Math.random() * alphabet.length);
        //keyLetter = alphabet[keyLetter];
        let keyText = document.getElementById("input-key-encryption").value.toUpperCase();
        let key = keyText.split("");
        let inputText = document.getElementById("input-encryption").value.toUpperCase();
        document.getElementById("result-encryption").innerText = inputText.trim();
        let text = inputText.split("");
        let newText = [];
        for (let i in text) {
            let letterKey = alphabet.indexOf(text[i]);
            if (letterKey === -1) {
                newText.push(text[i]);
            }
            else {
                let keyIndex = alphabet.indexOf(key[i % key.length]);
                newText.push(alphabet[(letterKey + keyIndex) % alphabet.length]);
            }
        }
        encryptedText.push(newText.join(""));
    }
    function GetOneTimePadDecryptText() {
        let keyText = document.getElementById("input-key-decryption").value.toUpperCase();
        let key = keyText.split("");
        let inputText = document.getElementById("input-decryption").value.toUpperCase();
        document.getElementById("result-decryption").innerText = inputText.trim();
        let text = inputText.split("");
        let newText = [];
        for (let i in text) {
            let letterKey = alphabet.indexOf(text[i]);
            if (letterKey === -1) {
                newText.push(text[i]);
            }
            else {
                let keyIndex = alphabet.indexOf(key[i % key.length]);
                newText.push(alphabet[(letterKey - keyIndex + alphabet.length) % alphabet.length]);
            }
        }
        decryptedText.push(newText.join(""));
    }
</script>

<link href="https://fonts.googleapis.com/css2?family=Google Sans:wght@400;700&display=swap" rel="stylesheet"> 

<nav class="navigation">
    <button class="btn" class:active={activeContent === "encryption"} onclick={() => showContent("encryption")}><h1>KRYPTERING</h1></button>
    <button class="btn" class:active={activeContent === "decryption"} onclick={() => showContent("decryption")}><h1>DEKRYPTERING</h1></button>
</nav>

<div class="content" style="background-color: #171717; color: white;" class:active={activeContent === "encryption"}>
    <h2>KRYPTERING</h2>
    <p>Skriv inn teksten som skal krypteres:</p>
    <select id="cipher-type-encryption" bind:value={encryptionCipher}>
        <option disabled>Velg chiffer</option>
        <option value="ceaser-cipher">Caesar-chiffer</option>
        <option value="vigenere-cipher">Vigenere-chiffer</option>
        <option value="one-time-pad">One-Time Pad</option>
    </select>
    <br>
    <input type="text" id="input-key-encryption" placeholder="Skriv inn nøkkelord" bind:value={keyLetter} /><br>
    <input type="text" id="input-encryption" placeholder="Skriv inn teksten her" />
    <button id="btn-krypter" class="btn-krypter" onclick={GetEncryptText}>Krypter</button>
    <h2 id="result-encryption"></h2>
    <h2>HISTORIKK</h2>
    <ul>
        {#each encryptedText as text}
            <li>{text}</li>
        {/each}
    </ul>
</div>

<div class="content" style="background-color: #171717; color: white;" class:active={activeContent === "decryption"}>
    <h2>DEKRYPTERING</h2>
    <p>Skriv inn teksten som skal dekrypteres:</p>
    <select id="cipher-type-decryption" bind:value={decryptionCipher}>
        <option disabled>Velg chiffer</option>
        <option value="ceaser-cipher">Caesar-chiffer</option>
        <option value="vigenere-cipher">Vigenere-chiffer</option>
        <option value="one-time-pad">One-Time Pad</option>
    </select>
    <br>
    <input type="text" id="input-key-decryption" placeholder="Skriv inn nøkkelord" bind:value={keyLetter} /><br>
    <input type="text" id="input-decryption" placeholder="Skriv inn teksten her" />
    <button id="btn-dekrypter" class="btn-dekrypter" onclick={GetDecryptText}>Dekrypter</button>
    <h2 id="result-decryption"></h2>
    <h2>HISTORIKK</h2>
    <ul>
        {#each decryptedText as text}
            <li>{text}</li>
        {/each}
    </ul>
</div>

<style>
    * {
        font-family: "Google Sans", sans-serif;
    }
    :global(body) {
        margin: 0px;
        background-color: #171717;
    }
    .content {
        display: none;
    }
    .content.active {
        display: block;
    }
    .btn {
        margin: 0px;
        padding: 10px;
        background-color: #f25623;
        border: none;
        cursor: pointer;
    }
    .btn.active {
        flex: 1;
        margin: 0px;
        padding: 10px;
        border: none;
        cursor: pointer;
        background-color: #171717;
        color: white;
    }
    .btn.active:hover {
        box-shadow: 0px 1px 0px #000000;
    }
    .btn:hover {
        box-shadow: 0px 1px 0px  #000000;
    }
    .navigation {
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
    }
    input {
        width: 300px;
        padding: 10px;
        margin-top: 10px;
        border: none;
    }
    .btn-dekrypter, .btn-krypter {
        width: 100px;
        margin-top: 10px;
        padding: 10px;
        background-color: #f25623;
        border: none;
        cursor: pointer;
    }
    .btn-krypter:hover, .btn-dekrypter:hover {
        box-shadow: 1px 0px 0px  #000000;
    }
    ul {
        list-style-type: none;
        padding: 0px;
    }
    li {
        margin-bottom: 5px;
    }
    select {
        width: 300px;
        padding: 10px;
        margin-top: 10px;
        border: none;
    }
</style>
