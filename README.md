<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ganzer Estoque</title>
	<link rel="icon" type="image/png" href="..\img\icone_estoque.png">

    <style>
	

        body {
			font-family: Arial, sans-serif;
			background-color: black;
			color: white;
			margin: 0;
			padding: 120px 40px 40px 40px;
			text-align: center;
		}
		
		html {
			scroll-behavior: smooth;
		}

        h1 {
            text-align: center;
        }

        .section {
            margin-bottom: 5px;
            padding: 10px;
            border: 2px solid #444;
            background-color: #222;
            border-radius: 10px;
        }

        input {
            margin: 5px;
            padding: 5px;
            border: 1px solid #aaa;
            border-radius: 4px;
            background-color: #333;
            color: white;
        }

        button {
            padding: 5px 15px;
            margin: 5px;
            background-color: red;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
        }

        button:hover {
            background-color: darkred;
        }

        pre {
            background-color: #111;
            padding: 10px;
            border-radius: 5px;
            white-space: pre-wrap;
            color: white;
            text-align: center;
        }

        /* MENU LATERAL */

        #menuBotao {
            position: fixed;
            top: 15px;
            left: 15px;
            font-size: 35px;
            cursor: pointer;
            color: white;
            z-index: 1001;
        }

        #menuLateral {
            position: fixed;
            top: 0;
            left: -350px;
            width: 320px;
            height: 100%;
            background-color: #111;
            overflow-y: auto;
            transition: 0.3s;
            padding: 20px;
            box-sizing: border-box;
            border-right: 2px solid #444;
            z-index: 1000;
        }

        #menuLateral h2 {
            margin-top: 50px;
        }

        #menuLateral input {
            width: 90%;
            margin-bottom: 15px;
        }
		
		#logoSistema1 {
		
			position: fixed;

			top: 10px;

			right: 20px;

			width: 100px;

			height: auto;

			z-index: 99999;

			pointer-events: none;
		}
		
		#logoSistema2 {

			position: fixed;

			top: 30px;

			left: 80px;

			width: 150px;

			height: auto;

			z-index: 99999;

			pointer-events: none;
		}

        .itemLista {
            background-color: #222;
            border: 1px solid #444;
            border-radius: 8px;
            padding: 10px;
            margin-bottom: 10px;
            text-align: left;
        }

        .itemLista strong {
            color: red;
        }
		
		#contadorItens {

			font-size: 13px;

			color: #aaa;

			margin-bottom: 10px;

			text-align: left;

			padding-left: 5px;
		}

    </style>
</head>

<body>
	
	<!-- LOGO DO SISTEMA -->

	<img src="..\img\logo_estoque1.png"
     id="logoSistema1">
	 
	 <img src="..\img\logo_estoque2.png"
     id="logoSistema2">

    <!-- BOTÃO MENU -->

    <div id="menuBotao" onclick="toggleMenu()">
        ☰
    </div>

    <!-- MENU LATERAL -->

    <div id="menuLateral">

        <h2>Itens em Estoque</h2>

        <input type="text"
		id="pesquisaEstoque"
		placeholder="Pesquisar item..."
		onkeyup="filtrarItens()">

		<div id="contadorItens">
			Total de itens: 0
		</div>

		<div id="listaEstoque"></div>

    </div>

    <h1>Ganzer Estoque</h1>

    <div class="section">

        <h3>Adicionar Item</h3>

		<input type="number" id="itemId" placeholder="ID do Item">

		<input type="text" id="itemNome" placeholder="Nome do Item">

		<input type="number" id="itemQuantidade" placeholder="Quantidade">

		<input type="number" id="itemPreco" placeholder="Preço">

		<button onclick="adicionarItem()">
			Adicionar
		</button>

    </div>

    <div class="section">

        <h3>Remover Quantidade de Item</h3>

        <input type="number" id="itemIdRemover" placeholder="ID do item">

        <input type="number" id="quantidadeRemover" placeholder="Quantidade a remover">

        <button onclick="removerQuantidade()">
            Remover
        </button>

    </div>

    <div class="section">

        <h3>Consultar Item</h3>

        <input type="number" id="itemIdConsultar" placeholder="ID do item">

        <button onclick="consultarPorId()">
            Consultar por ID
        </button>

        <br>

        <input type="text" id="itemNomeConsultar" placeholder="Nome do item">

        <button onclick="consultarPorNome()">
            Consultar por Nome
        </button>

        <button onclick="limparCampos()">
            Limpar
        </button>

    </div>

    <div class="section">

        <h3>Salvar Estoque</h3>

        <button onclick="exportarTXT()">
            Exportar Estoque
        </button>

        <button onclick="document.getElementById('arquivoImportar').click()">
            Importar Estoque
        </button>

        <button onclick="limparEstoque()">
            Limpar Estoque
        </button>

        <input type="file"
               id="arquivoImportar"
               accept=".txt"
               style="display:none"
               onchange="importarTXT(event)">

    </div>

    <pre id="resultado"></pre>

    <script>

        let estoque =
            JSON.parse(localStorage.getItem('estoque')) || [];

        let contador =
            estoque.length > 0
            ? Math.max(...estoque.map(item => item.id)) + 1
            : 1;

        let menuAberto = false;

        function salvarEstoque() {

            localStorage.setItem(
                'estoque',
                JSON.stringify(estoque)
            );
        }

        function adicionarItem() {

    const id =
        parseInt(document.getElementById('itemId').value);

    const nome =
        document.getElementById('itemNome').value.trim();

    const quantidade =
        parseInt(document.getElementById('itemQuantidade').value);

    const preco =
        parseFloat(document.getElementById('itemPreco').value);

    // VALIDAÇÃO
    if (
        isNaN(id) ||
        nome === "" ||
        isNaN(quantidade) ||
        quantidade <= 0 ||
        isNaN(preco) ||
        preco < 0
    ) {

        mostrarMensagem(
            'Preencha todos os campos corretamente.'
        );

        return;
    }

    // PROCURA ITEM COM MESMO ID
    const itemExistente =
        estoque.find(item => item.id === id);

    // SE JÁ EXISTE UM ITEM COM O MESMO ID
    if (itemExistente) {

        // SE NOME E PREÇO FOREM IGUAIS
        if (
            itemExistente.nome.toLowerCase() === nome.toLowerCase()
            &&
            itemExistente.preco === preco
        ) {

            // SOMA QUANTIDADE
            itemExistente.quantidade += quantidade;

            salvarEstoque();

            atualizarListaEstoque();

            mostrarMensagem(
                `Quantidade adicionada ao item '${nome}'.`
            );

        } else {

            mostrarMensagem(
                'ERRO: Já existe outro item com este ID.'
            );
        }

        return;
    }

    // CRIA NOVO ITEM
    estoque.push({
        id,
        nome,
        quantidade,
        preco
    });

    salvarEstoque();

    atualizarListaEstoque();

    mostrarMensagem(
        `Item '${nome}' adicionado com sucesso!`
    );

    // LIMPA CAMPOS
    document.getElementById('itemId').value = "";
    document.getElementById('itemNome').value = "";
    document.getElementById('itemQuantidade').value = "";
    document.getElementById('itemPreco').value = "";
}

        function removerQuantidade() {

            const id =
                parseInt(document.getElementById('itemIdRemover').value);

            const quantidadeRemover =
                parseInt(document.getElementById('quantidadeRemover').value);

            const item =
                estoque.find(item => item.id === id);

            if (item && quantidadeRemover > 0) {

                if (item.quantidade >= quantidadeRemover) {

                    item.quantidade -= quantidadeRemover;

                    mostrarMensagem(
                        `Removido ${quantidadeRemover} unidades do item '${item.nome}'.`
                    );

                    if (item.quantidade === 0) {

                        const index = estoque.indexOf(item);

                        estoque.splice(index, 1);

                        mostrarMensagem(
                            `O item '${item.nome}' foi totalmente removido.`
                        );
                    }

                    salvarEstoque();

                    atualizarListaEstoque();

                } else {

                    mostrarMensagem(
                        'Quantidade insuficiente para remover.'
                    );
                }

            } else {

                mostrarMensagem(
                    'Item não encontrado ou quantidade inválida.'
                );
            }
        }

        function consultarPorId() {

            const id =
                parseInt(document.getElementById('itemIdConsultar').value);

            const item =
                estoque.find(item => item.id === id);

            if (item) {

                mostrarMensagem(
                    `ID: ${item.id} | Nome: ${item.nome} | Quantidade: ${item.quantidade} | Preço: R$ ${item.preco.toFixed(2)}`
                );

            } else {

                mostrarMensagem(
                    'Item não encontrado.'
                );
            }
        }

        function consultarPorNome() {

            const nome =
                document.getElementById('itemNomeConsultar').value;

            const item =
                estoque.find(item =>
                    item.nome.toLowerCase() === nome.toLowerCase()
                );

            if (item) {

                mostrarMensagem(
                    `ID: ${item.id} | Nome: ${item.nome} | Quantidade: ${item.quantidade} | Preço: R$ ${item.preco.toFixed(2)}`
                );

            } else {

                mostrarMensagem(
                    'Item não encontrado.'
                );
            }
        }

        function mostrarMensagem(mensagem) {

            const resultado =
                document.getElementById('resultado');

            resultado.innerHTML += mensagem + "<br>";
        }

        function limparCampos() {

            document.querySelectorAll('input').forEach(input => {

                if (input.type !== "file") {

                    input.value = '';
                }
            });

            document.getElementById('resultado').innerHTML = '';
        }

        async function exportarTXT() {

    if (estoque.length === 0) {

        mostrarMensagem(
            "O estoque está vazio."
        );

        return;
    }

    let conteudo =
        "======= ESTOQUE =======";

    estoque.forEach(item => {

        conteudo +=
`
ID: ${item.id}
Nome: ${item.nome}
Quantidade: ${item.quantidade}
Preço: ${item.preco}
-------------------------`;
    });

    try {

        const arquivo =
            await window.showSaveFilePicker({

                suggestedName: "estoque.txt",

                types: [{
                    description: "Arquivo de Texto",
                    accept: {
                        "text/plain": [".txt"]
                    }
                }]
            });

        const gravador =
            await arquivo.createWritable();

        await gravador.write(conteudo);

        await gravador.close();

        mostrarMensagem(
            "Backup salvo com sucesso!"
        );

    } catch (erro) {

        mostrarMensagem(
            "Salvamento cancelado."
        );
    }
}

        function importarTXT(event) {

            const arquivo = event.target.files[0];

            if (!arquivo) return;

            const leitor = new FileReader();

            leitor.onload = function(e) {

                let texto = e.target.result;

                texto =
                    texto.replace("======= ESTOQUE =======", "");

                const blocos =
                    texto.split("-------------------------");

                estoque = [];

                blocos.forEach(bloco => {

                    const linhas =
                        bloco.trim().split("\n");

                    const linhasValidas =
                        linhas.filter(
                            linha => linha.trim() !== ""
                        );

                    if (linhasValidas.length >= 4) {

                        const id =
                            parseInt(
                                linhasValidas[0].replace("ID: ", "")
                            );

                        const nome =
                            linhasValidas[1].replace("Nome: ", "");

                        const quantidade =
                            parseInt(
                                linhasValidas[2].replace("Quantidade: ", "")
                            );

                        const preco =
                            parseFloat(
                                linhasValidas[3].replace("Preço: ", "")
                            );

                        if (!isNaN(id)) {

                            estoque.push({
                                id,
                                nome,
                                quantidade,
                                preco
                            });
                        }
                    }
                });

                salvarEstoque();

                atualizarListaEstoque();

                contador =
                    estoque.length > 0
                    ? Math.max(...estoque.map(item => item.id)) + 1
                    : 1;

                mostrarMensagem(
                    "Estoque importado com sucesso!"
                );
            };

            leitor.readAsText(arquivo);
        }

        function limparEstoque() {

            if (confirm("Deseja apagar todo o estoque salvo?")) {

                estoque = [];

                localStorage.removeItem('estoque');

                contador = 1;

                atualizarListaEstoque();

                mostrarMensagem(
                    "Estoque apagado com sucesso!"
                );
            }
        }

        // MENU LATERAL

        function toggleMenu() {

            const menu =
                document.getElementById("menuLateral");

            if (!menuAberto) {

                menu.style.left = "0";

                atualizarListaEstoque();

            } else {

                menu.style.left = "-350px";
            }

            menuAberto = !menuAberto;
        }

        // MOSTRAR ITENS

        function atualizarListaEstoque() {

    const lista =
        document.getElementById("listaEstoque");

    const contador =
        document.getElementById("contadorItens");

    lista.innerHTML = "";

    contador.innerHTML =
        `Total de itens: ${estoque.length}`;

    if (estoque.length === 0) {

        lista.innerHTML =
            "<p>Estoque vazio.</p>";

        return;
    }

    estoque.forEach(item => {

        lista.innerHTML +=
`
<div class="itemLista">

<strong>ID:</strong> ${item.id}<br>

<strong>Nome:</strong> ${item.nome}<br>

<strong>Quantidade:</strong> ${item.quantidade}<br>

<strong>Preço:</strong> R$ ${item.preco}

</div>
`;
    });
}

        // PESQUISAR

        function filtrarItens() {

    const pesquisa =
        document.getElementById("pesquisaEstoque")
        .value
        .toLowerCase();

    const lista =
        document.getElementById("listaEstoque");

    const contador =
        document.getElementById("contadorItens");

    lista.innerHTML = "";

    const itensFiltrados =
        estoque.filter(item =>

            item.nome.toLowerCase().includes(pesquisa) ||
            item.id.toString().includes(pesquisa)
        );

    contador.innerHTML =
        `Total de itens: ${itensFiltrados.length}`;

    if (itensFiltrados.length === 0) {

        lista.innerHTML =
            "<p>Nenhum item encontrado.</p>";

        return;
    }

    itensFiltrados.forEach(item => {

        lista.innerHTML +=
`
<div class="itemLista">

<strong>ID:</strong> ${item.id}<br>

<strong>Nome:</strong> ${item.nome}<br>

<strong>Quantidade:</strong> ${item.quantidade}<br>

<strong>Preço:</strong> R$ ${item.preco}

</div>
`;
    });
}

        atualizarListaEstoque();

    </script>

</body>
</html>
