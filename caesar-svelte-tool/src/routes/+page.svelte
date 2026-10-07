<script>
    function showContent(id) {
        try {
            document.querySelectorAll(".content").forEach((block) => {
                block.classList.remove("active");
            });

            const selectedBlock = document.getElementById(id);
            const button1 = document.querySelectorAll(".btn1");
            const button2 = document.querySelectorAll(".btn2");
            if (id === "encryption") {
                button1.forEach((btn) => btn.classList.add("active"));
                button2.forEach((btn) => btn.classList.remove("active"));
            } else if (id === "decryption") {
                button2.forEach((btn) => btn.classList.add("active"));
                button1.forEach((btn) => btn.classList.remove("active"));
            }
            if (selectedBlock) {
                selectedBlock.classList.add("active");
            }
        } catch (error) {
            console.error("Error showing content:", error);
        }
    }
</script>

<nav class="navigation">
    <button class="btn active" onclick={() => showContent("encryption")}
        >KRYPTERING</button
    >
    <button class="btn" onclick={() => showContent("decryption")}
        >DEKRYPTERING</button
    >
</nav>

<div id="encryption" class="content active">
    <h2>KRYPTERING</h2>
    <p>Dette er innholdet i den første blokken.</p>
</div>

<div id="decryption" class="content">
    <h2>DEKRYPTERING</h2>
    <p>Dette er innholdet i den andre blokken.</p>
</div>

<style>
    @font-face {
        font-family: "Google Sans";
        font-style: normal;
        font-weight: 700;
        src: url("https://fonts.cdnfonts.com/s/14495/GoogleSans-Bold.woff")
            format("woff");
    }
    *{
        font-family: "Google Sans", sans-serif;

    }
    :global(body) {
        margin: 0px;
        background-color: #303a47;
    }
    .content {
        display: none;
    }
    .content.active {
        display: block;
    }
    .btn {
        margin: 0px;
        padding: 10px ;
        border: none;
        cursor: pointer;
    }
    .btn.active {
        margin: 0px;
        padding: 10px ;
        border: none;
        cursor: pointer;
        background-color: #4caf50;
        color: white;
    }

    .navigation {
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
    }
</style>
