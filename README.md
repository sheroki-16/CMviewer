<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>MiMa - Meme Token</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header>
    <img src="partridge-logo.png" alt="MiMa Logo" class="logo" />
    <h1>MiMa</h1>
    <p class="slogan">Money Meowments</p>
  </header>

  <section class="about">
    <h2>What is MiMa?</h2>
    <p><strong>MiMa</strong> is a meme-powered crypto token led by a partridge mascot — bringing fun, freedom, and financial mischief to the blockchain. Built for community, designed to fly!</p>
  </section>

  <section class="tokenomics">
    <h2>Tokenomics</h2>
    <ul>
      <li><strong>Token Name:</strong> MiMa</li>
      <li><strong>Symbol:</strong> MIMA</li>
      <li><strong>Total Supply:</strong> 1,000,000,000</li>
      <li><strong>Network:</strong> Solana or BSC</li>
      <li><strong>Contract Address:</strong> [Coming Soon]</li>
    </ul>
  </section>

  <section class="roadmap">
    <h2>Roadmap</h2>
    <ol>
      <li>🚀 Launch MiMa token</li>
      <li>📢 Meme campaign (X, Reddit, Discord)</li>
      <li>📈 Listing on DEX (Raydium / PancakeSwap)</li>
      <li>🎁 Airdrops, contests & NFTs</li>
      <li>🌍 Build the MiMa DAO & utility features</li>
    </ol>
  </section>

  <section class="cta">
    <h2>Join the Meme-ment</h2>
    <p>Follow us, hodl strong, and meme your way to the moon!</p>
    <div class="socials">
      <a href="#">Telegram</a>
      <a href="#">Twitter</a>
      <a href="#">Discord</a>
    </div>
  </section>

  <footer>
    <p>© 2025 MiMa Coin. All rights reserved.</p>
  </footer>
</body>
</html>
body {
  font-family: 'Segoe UI', sans-serif;
  margin: 0;
  background-color: #1e1e1e;
  color: #f5f5f5;
  text-align: center;
  padding: 0 20px;
}

header {
  padding: 2rem 0;
  background-color: #292929;
}

.logo {
  width: 120px;
  border-radius: 50%;
  margin-bottom: 10px;
}

.slogan {
  font-style: italic;
  color: #ff9800;
}

section {
  margin: 3rem auto;
  max-width: 700px;
}

ul, ol {
  text-align: left;
  margin: 0 auto;
  display: inline-block;
}

.socials a {
  margin: 0 10px;
  color: #ff9800;
  text-decoration: none;
  font-weight: bold;
}

footer {
  margin-top: 50px;
  font-size: 0.8em;
  color: #aaa;
}
<section class="market">
  <h2>📊 Live Market Watch</h2>
  <div id="prices">
    <p>Loading prices...</p>
  </div>
</section>
<script>
  async function fetchPrices() {
    const url = 'https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum,solana,bonk,dogwifhat&vs_currencies=usd';
    try {
      const res = await fetch(url);
      const data = await res.json();
      const container = document.getElementById('prices');
      container.innerHTML = `
        <p><strong>Bitcoin (BTC):</strong> $${data.bitcoin.usd}</p>
        <p><strong>Ethereum (ETH):</strong> $${data.ethereum.usd}</p>
        <p><strong>Solana (SOL):</strong> $${data.solana.usd}</p>
        <p><strong>Bonk (BONK):</strong> $${data.bonk.usd}</p>
        <p><strong>dogwifhat (WIF):</strong> $${data.dogwifhat.usd}</p>
      `;
    } catch (error) {
      document.getElementById('prices').innerHTML = '<p>Failed to load prices. 😢</p>';
    }
  }

  fetchPrices();
  setInterval(fetchPrices, 60000); // Refresh every 60 sec
</script>
.market {
  background-color: #111;
  padding: 2rem;
  border-radius: 10px;
  margin: 2rem auto;
  max-width: 600px;
  box-shadow: 0 0 10px rgba(255, 152, 0, 0.2);
}

.market p {
  font-size: 1.1rem;
  margin: 0.5rem 0;
}
<script>
  async function fetchPrices() {
    const url = 'https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum,solana,xrp,zebec-protocol,dogecoin,shiba-inu,pepe,bonk,dogwifhat&vs_currencies=usd';
    try {
      const res = await fetch(url);
      const data = await res.json();
      const container = document.getElementById('prices');
      container.innerHTML = `
        <p><strong>Bitcoin (BTC):</strong> $${data.bitcoin.usd}</p>
        <p><strong>Ethereum (ETH):</strong> $${data.ethereum.usd}</p>
        <p><strong>Solana (SOL):</strong> $${data.solana.usd}</p>
        <p><strong>XRP:</strong> $${data.xrp.usd}</p>
        <p><strong>Zebec (ZBCN):</strong> $${data["zebec-protocol"].usd}</p>
        <p><strong>Dogecoin (DOGE):</strong> $${data.dogecoin.usd}</p>
        <p><strong>Shiba Inu (SHIB):</strong> $${data["shiba-inu"].usd}</p>
        <p><strong>PEPE:</strong> $${data.pepe.usd}</p>
        <p><strong>Bonk (BONK):</strong> $${data.bonk.usd}</p>
        <p><strong>dogwifhat (WIF):</strong> $${data.dogwifhat.usd}</p>
      `;
    } catch (error) {
      document.getElementById('prices').innerHTML = '<p>Failed to load prices. 😢</p>';
    }
  }

  fetchPrices();
  setInterval(fetchPrices, 60000); // Refresh every 60 seconds
</script>
