<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="$PAI PRESALE - Buy Paimon ($PAI) tokens.">
    <meta name="keywords" content="PAI, presale, crypto, solana, SOL">
    <meta name="author" content="Paimon Team">
    <title>$PAI PRESALE</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:400,700&display=swap">
    <style>
        body {
            font-family: 'Roboto', Arial, sans-serif;
            background-color: #f0f8ff;
            color: #003366;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 51, 102, 0.2);
            max-width: 500px;
            width: 100%;
            text-align: center;
        }

        h1 {
            color: #003366;
            font-size: 24px;
        }

        p {
            font-size: 16px;
        }

        .social-buttons a {
            margin: 10px;
            padding: 10px 20px;
            border-radius: 5px;
            color: white;
            text-decoration: none;
            font-size: 16px;
        }

        .btn-twitter {
            background-color: #1DA1F2;
        }

        .btn-telegram {
            background-color: #0088cc;
        }

        input[type="number"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            border: 1px solid #007bff;
        }

        button {
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }

        button:hover {
            background-color: #0056b3;
        }

        #walletAddress {
            margin-top: 10px;
            font-size: 14px;
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/@solana/web3.js@latest/dist/solana-web3.min.js"></script>
    <script>
        const solToUSD = 20;  // Adjust the SOL to USD rate
        const paiPrice = 0.0007;

        document.addEventListener("DOMContentLoaded", function() {
            document.getElementById("solAmount").addEventListener("input", function(event) {
                let solAmount = parseFloat(event.target.value);
                let paiTokens = (solAmount * solToUSD) / paiPrice;
                document.getElementById("paiTokens").textContent = `You will receive: ${paiTokens.toFixed(2)} PAI Tokens`;
            });

            document.getElementById("presaleForm").addEventListener("submit", function(event) {
                event.preventDefault();
                let solAmount = parseFloat(document.getElementById("solAmount").value);
                let message = document.getElementById("message");
                if (solAmount >= 0.01 && solAmount <= 10) {
                    let paiTokens = (solAmount * solToUSD) / paiPrice;
                    message.textContent = `Success! You have purchased ${paiTokens.toFixed(2)} PAI Tokens.`;
                    message.style.color = "green";
                } else {
                    message.textContent = "Please enter a valid amount between 0.01 and 10 SOL.";
                    message.style.color = "red";
                }
            });

            const connectWalletBtn = document.getElementById('connectWalletBtn');
            const walletAddress = document.getElementById('walletAddress');
            
            connectWalletBtn.addEventListener('click', async () => {
                try {
                    if ('solana' in window) {
                        const provider = window.solana;
                        if (provider.isPhantom) {
                            await provider.connect();
                            const walletPublicKey = provider.publicKey.toString();
                            walletAddress.textContent = `Connected: ${walletPublicKey}`;
                        }
                    } else {
                        alert('Solana wallet not found! Please install Phantom.');
                    }
                } catch (err) {
                    console.error('Wallet connection error:', err);
                    walletAddress.textContent = 'Connection failed. Try again.';
                }
            });
        });
    </script>
</head>
<body>
    <div class="container">
        <h1>$PAI PRESALE</h1>
        <p>Get ready for the next level of cryptocurrency! Buy $PAI with SOL now!</p>
        <p><strong>Presale Price:</strong> $0.0007 per $PAI</p>
        <p><strong>Token Name:</strong> Paimon</p>
        <p><strong>Symbol:</strong> PAI</p>
        <p><strong>Decimals:</strong> 6</p>
        <p><strong>Min Contribution:</strong> 0.01 SOL</p>
        <p><strong>Max Contribution:</strong> 10 SOL</p>
        
        <form id="presaleForm">
            <label for="solAmount">Amount to Invest (SOL):</label>
            <input type="number" id="solAmount" name="solAmount" min="0.01" max="10" step="0.01" required>
            <p id="paiTokens">You will receive: 0 PAI Tokens</p>
            <button type="submit">Buy $PAI Tokens</button>
        </form>
        <p id="message"></p>

        <h2>Connect Your Wallet</h2>
        <button id="connectWalletBtn">Connect Wallet</button>
        <p id="walletAddress">Not connected</p>

        <div class="social-buttons">
            <h2>Join Us on Social Media</h2>
            <a href="https://x.com/PaimonCrypto" class="btn-twitter">Twitter</a>
            <a href="https://t.me/paimoncoin" class="btn-telegram">Telegram</a>
        </div>

        <footer>
            <p>&copy; 2024 Paimon Token. All rights reserved.</p>
        </footer>
    </div>
</body>
</html>
