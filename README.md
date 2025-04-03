<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Solicite crédito para investimentos com as melhores condições e parcelas acessíveis.">
    <meta name="keywords" content="crédito, investimento, financiamento, consórcio, parcelamento">
    <meta name="author" content="Seu Nome ou Empresa">
    <title>Crédito para Investimento</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .fade-in { animation: fadeIn 0.8s ease-in-out; }
    </style>
</head>
<body class="bg-cover bg-center bg-no-repeat min-h-screen flex items-center justify-center p-4" style="background-image: url('https://i.imgur.com/aPLuDmc.jpeg');">
    <div class="bg-white bg-opacity-90 p-6 rounded-lg shadow-lg max-w-md w-full fade-in">
        <h2 class="text-3xl font-bold text-gray-900 text-center mb-6">Crédito para Investimento</h2>
        <form id="creditoForm" class="space-y-4">
            <div>
                <label class="block text-gray-700 font-semibold">Seu Nome</label>
                <input type="text" id="nome" name="nome" required class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-green-500">
            </div>
            <div>
                <label class="block text-gray-700 font-semibold">Seu Telefone</label>
                <input type="tel" id="telefone" name="telefone" required class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-green-500">
            </div>
            <div>
                <label class="block text-gray-700 font-semibold">Cidade</label>
                <input type="text" id="cidade" name="cidade" required class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-green-500">
            </div>
            <div>
                <label class="block text-gray-700 font-semibold">Área de Investimento</label>
                <select id="investimento" name="investimento" required class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-green-500">
                    <option value="" disabled selected>Selecione uma opção</option>
                    <option value="Área Rural">Área Rural</option>
                    <option value="Veículo">Veículo</option>
                    <option value="Imóvel">Imóvel</option>
                    <option value="Construção">Construção</option>
                    <option value="Reforma">Reforma</option>
                    <option value="Loja/Ponto Comercial">Loja/Ponto Comercial</option>
                </select>
            </div>
            <div>
                <label class="block text-gray-700 font-semibold">Valor do Investimento</label>
                <select id="valor" name="valor" onchange="atualizarParcelas()" required class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-green-500">
                    <option value="" disabled selected>Selecione um valor</option>
                    <option value="100000">R$ 100.000</option>
                    <option value="200000">R$ 200.000</option>
                    <option value="500000">R$ 500.000</option>
                    <option value="1000000">R$ 1.000.000</option>
                </select>
            </div>
            <div>
                <label class="block text-gray-700 font-semibold">Valor da Parcela</label>
                <select id="parcela" name="parcela" required class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-green-500">
                    <option value="" disabled selected>Selecione o valor do investimento primeiro</option>
                </select>
            </div>
            <button type="button" onclick="enviarWhatsApp(); enviarParaCRM();" class="w-full bg-green-500 text-white p-3 rounded-lg hover:bg-green-600 transition-all">Solicitar Crédito</button>
        </form>
    </div>
    <script>
        function atualizarParcelas() {
            var valor = document.getElementById("valor").value;
            var parcela = document.getElementById("parcela");
            parcela.innerHTML = '<option value="" disabled selected>Selecione uma opção</option>';
            var opcoesParcelas = {
                "100000": [590, 800, 1000],
                "200000": [1300, 1800, 2200],
                "500000": [4000, 6000, 7000],
                "1000000": [10000, 20000, 25000]
            };
            if (valor in opcoesParcelas) {
                opcoesParcelas[valor].forEach(function(p) {
                    var option = document.createElement("option");
                    option.value = p;
                    option.text = "R$ " + p.toLocaleString();
                    parcela.appendChild(option);
                });
            }
        }

        function enviarParaCRM() {
            var data = {
                fields: [
                    { name: "nome", value: document.getElementById("nome").value },
                    { name: "telefone", value: document.getElementById("telefone").value },
                    { name: "cidade", value: document.getElementById("cidade").value },
                    { name: "investimento", value: document.getElementById("investimento").value },
                    { name: "valor", value: document.getElementById("valor").value },
                    { name: "parcela", value: document.getElementById("parcela").value }
                ]
            };

            fetch("https://api.hubapi.com/forms/v2/submissions", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    "Authorization": "Bearer pat-na1-ee476d6a-036a-416c-aeed-36aa70bc1bf0"
                },
                body: JSON.stringify(data)
            }).then(response => response.json()).then(data => {
                console.log("Dados enviados para o HubSpot:", data);
            }).catch(error => {
                console.error("Erro ao enviar para o HubSpot:", error);
            });
        }
    </script>
</body>
</html>
