
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Raízes do Sabor</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600&family=Poppins&display=swap" rel="stylesheet">
    <style>
        body {
            margin: 0;
            font-family: 'Poppins', sans-serif;
            background-image: url('https://i.imgur.com/2YcFzzS.jpg'); /* fundo de madeira com vinhos */
            background-size: cover;
            background-attachment: fixed;
            color: #fff;
        }
        header {
            background-color: rgba(33, 20, 10, 0.85);
            padding: 1.5rem;
            text-align: center;
        }
        header h1 {
            font-family: 'Playfair Display', serif;
            font-size: 3rem;
            margin: 0;
            color: #e0c79f;
        }
        .container {
            max-width: 1100px;
            margin: auto;
            padding: 2rem;
            background-color: rgba(255, 255, 255, 0.9);
            color: #222;
            border-radius: 10px;
        }
        .produtos {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 1.5rem;
        }
        .produto {
            border: 1px solid #ccc;
            border-radius: 10px;
            padding: 1rem;
            background: #faf3e0;
            text-align: center;
        }
        .produto img {
            width: 100%;
            height: 180px;
            object-fit: cover;
            border-radius: 6px;
        }
        .produto h3 {
            font-family: 'Playfair Display', serif;
            color: #6e2c00;
        }
        button {
            background-color: #8B4513;
            color: #fff;
            padding: 0.5rem 1rem;
            border: none;
            margin-top: 0.5rem;
            cursor: pointer;
            border-radius: 6px;
        }
        #carrinho {
            margin-top: 2rem;
        }
        footer {
            background-color: rgba(33, 20, 10, 0.85);
            text-align: center;
            padding: 1rem;
            color: #fff;
        }
        .whatsapp-button {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #25D366;
            color: white;
            border-radius: 50px;
            padding: 1rem 1.5rem;
            font-size: 16px;
            text-decoration: none;
        }
    </style>
</head>
<body>
    <header>
        <h1>Raízes do Sabor</h1>
    </header>
    <div class="container">
        <h2>Produtos em destaque</h2>
        <div class="produtos" id="lista-produtos">
            <!-- Produtos inseridos via JavaScript -->
        </div>

        <div id="carrinho">
            <h2>🛒 Carrinho</h2>
            <ul id="itens-carrinho"></ul>
            <p><strong>Total:</strong> R$ <span id="total">0.00</span></p>
            <button onclick="finalizarPedido()">Finalizar Pedido via WhatsApp</button>
        </div>
    </div>

    <a href="#" class="whatsapp-button" onclick="finalizarPedido()">📲 WhatsApp</a>

    <footer>
        <p>&copy; 2025 Raízes do Sabor. Todos os direitos reservados.</p>
    </footer>

    <script>
        const produtos = [
            { nome: "Vinho Tinto Seco", preco: 75.90, imagem: "https://i.imgur.com/vRQpmQ0.jpg" },
            { nome: "Queijo Parmesão", preco: 45.50, imagem: "https://i.imgur.com/oShNdiT.jpg" },
            { nome: "Vinho Branco Suave", preco: 65.90, imagem: "https://i.imgur.com/YRkQ0ff.jpg" },
            { nome: "Geleia de Uva Artesanal", preco: 18.90, imagem: "https://i.imgur.com/1sOdHJX.jpg" },
            { nome: "Salame Italiano", preco: 34.90, imagem: "https://i.imgur.com/n6wK7TJ.jpg" },
            { nome: "Queijo Brie", preco: 52.00, imagem: "https://i.imgur.com/HInYFIm.jpg" },
            { nome: "Vinho Rosé", preco: 69.90, imagem: "https://i.imgur.com/9T3pjf4.jpg" },
            { nome: "Queijo Gouda", preco: 40.00, imagem: "https://i.imgur.com/pUOZldx.jpg" }
        ];

        const listaProdutos = document.getElementById('lista-produtos');
        const itensCarrinho = document.getElementById('itens-carrinho');
        const totalSpan = document.getElementById('total');

        let carrinho = [];

        produtos.forEach((produto, index) => {
            const div = document.createElement('div');
            div.className = 'produto';
            div.innerHTML = `
                <img src="${produto.imagem}" alt="${produto.nome}">
                <h3>${produto.nome}</h3>
                <p>R$ ${produto.preco.toFixed(2)}</p>
                <button onclick="adicionarAoCarrinho(${index})">Adicionar</button>
            `;
            listaProdutos.appendChild(div);
        });

        function adicionarAoCarrinho(index) {
            carrinho.push(produtos[index]);
            atualizarCarrinho();
        }

        function atualizarCarrinho() {
            itensCarrinho.innerHTML = '';
            let total = 0;
            carrinho.forEach(item => {
                const li = document.createElement('li');
                li.textContent = `${item.nome} - R$ ${item.preco.toFixed(2)}`;
                itensCarrinho.appendChild(li);
                total += item.preco;
            });
            totalSpan.textContent = total.toFixed(2);
        }

        function finalizarPedido() {
            if (carrinho.length === 0) {
                alert("Seu carrinho está vazio!");
                return;
            }
            let mensagem = "Olá! Gostaria de fazer o seguinte pedido:%0A";
            carrinho.forEach(item => {
                mensagem += `- ${item.nome} (R$ ${item.preco.toFixed(2)})%0A`;
            });
            const total = carrinho.reduce((acc, item) => acc + item.preco, 0);
            mensagem += `%0ATotal: R$ ${total.toFixed(2)}`;
            window.open(`https://wa.me/5500000000000?text=${mensagem}`, "_blank");
        }
    </script>
</body>
</html>
