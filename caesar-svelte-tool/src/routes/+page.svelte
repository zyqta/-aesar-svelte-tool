<script>
    let activeContent = $state("encryption");
    let encryptedText = $state([]);
    let decryptedText = $state([]);
    const alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZÆØÅ";
    let keyLetter = $state("F");

    /** @param {"encryption" | "decryption"} element */
    function showContent(element) {
        activeContent = element;
    }
    function GetEncryptText(text) {
        text = document.getElementById("input-encryption").value.toUpperCase();
        document.getElementById("result-encryption").innerText = text.trim();
        encryptedText.push(text);
        //let keyIndex = alphabet.indexOf(keyLetter);
        
    }
    function GetDecryptText(text) {
        text = document.getElementById("input-decryption").value.toUpperCase();
        document.getElementById("result-decryption").innerText = text.trim();
        decryptedText.push(text);
        //let keyIndex = alphabet.indexOf(keyLetter.toUpperCase());
    }
</script>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Google Sans:wght@400;700&display=swap" rel="stylesheet"> 

<nav class="navigation">
    <button
        class="btn"
        class:active={activeContent === "encryption"}
        onclick={() => showContent("encryption")}><h1>KRYPTERING</h1></button
    >
    <button
        class="btn"
        class:active={activeContent === "decryption"}
        onclick={() => showContent("decryption")}><h1>DEKRYPTERING</h1></button
    >
</nav>

<div
    class="content"
    style="background-color: #171717; color: white;"
    class:active={activeContent === "encryption"}
>
    <h2>KRYPTERING</h2>
    <p>Skriv inn tekst som skal krypteres: </p>
    <input type="text" id="input-key" placeholder="Skriv inn nøkkel" bind:value={keyLetter} /><br>
    <input type="text" id="input-encryption" placeholder="Skriv inn tekst her" /> 
    <button id="btn-krypter" class="btn-krypter" onclick={GetEncryptText}>Krypter</button>
    <h2 id="result-encryption"></h2>
    <h2>HISTORIKK</h2>
    <ul>
        {#each encryptedText as text}
            <li>{text}</li>
        {/each}
    </ul>
</div>

<div
    class="content"
    style="background-color: #171717; color: white;"
    class:active={activeContent === "decryption"}
>
    <h2>DEKRYPTERING</h2>
    <p>Skriv inn tekst som skal dekrypteres:</p>
    <input type="text" id="input-key" placeholder="Skriv inn nøkkel" bind:value={keyLetter} /><br>
    <input type="text" id="input-decryption" placeholder="Skriv inn tekst her" /> 
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
        box-shadow: 0px 1px 0px #f25623;
    }
    .btn:hover {
        box-shadow: 0px 1px 0px  #f25623;
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
        box-shadow: 1px 0px 0px  #f25623;
    }
    ul {
        list-style-type: none;
        padding: 0px;
    }
    li {
        margin-bottom: 5px;
    }
</style>
