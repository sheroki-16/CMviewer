# CMviewer
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Crypto Market View</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
    };
  </script>
</head>
<body class="bg-gray-900 text-white">
  <header class="bg-gray-800 p-4">
    <h1 class="text-2xl font-bold">Crypto Market View</h1>
    <nav class="mt-2">
      <a href="index.html" class="mr-4 text-blue-400">Market</a>
      <a href="tracker.html" class="mr-4 text-blue-400">Tracker</a>
      <a href="charts.html" class="text-blue-400">Charts</a>
    </nav>
  </header>

  <main class="p-6">
    <h2 class="text-xl font-semibold mb-4">Live Prices</h2>
    <div id="price-container" class="grid grid-cols-1 md:grid-cols-3 gap-4"></div>
  </main>

  <script>
    async function loadPrices() {
      const res = await fetch('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd');
      const data = await res.json();
      const container = document.getElementById('price-container');
      container.innerHTML = data.slice(0, 9).map(coin => `
        <div class="bg-gray-800 p-4 rounded shadow">
          <h3 class="text-lg font-bold">${coin.name} (${coin.symbol.toUpperCase()})</h3>
          <p>Price: $${coin.current_price.toLocaleString()}</p>
          <p>24h Change: ${coin.price_change_percentage_24h.toFixed(2)}%</p>
        </div>
      `).join('');
    }
    loadPrices();
    setInterval(loadPrices, 60000); // refresh every 60 seconds
  </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Portfolio Tracker</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-900 text-white">
  <header class="bg-gray-800 p-4">
    <h1 class="text-2xl font-bold">Crypto Portfolio Tracker</h1>
    <nav class="mt-2">
      <a href="index.html" class="mr-4 text-blue-400">Market</a>
      <a href="tracker.html" class="mr-4 text-blue-400">Tracker</a>
      <a href="charts.html" class="text-blue-400">Charts</a>
    </nav>
  </header>

  <main class="p-6">
    <h2 class="text-xl font-semibold mb-4">Your Holdings</h2>
    <form id="tracker-form" class="mb-6 space-y-4">
      <div>
        <label class="block mb-1">Coin Symbol (e.g., BTC)</label>
        <input type="text" id="coin" class="w-full p-2 bg-gray-800 rounded" required />
      </div>
      <div>
        <label class="block mb-1">Amount</label>
        <input type="number" id="amount" class="w-full p-2 bg-gray-800 rounded" required />
      </div>
      <button type="submit" class="bg-blue-500 px-4 py-2 rounded">Add to Tracker</button>
    </form>

    <div id="portfolio" class="space-y-4"></div>
  </main>

  <script>
    let portfolio = [];

    async function fetchPrice(symbol) {
      const res = await fetch(`https://api.coingecko.com/api/v3/coins/${symbol.toLowerCase()}`);
      return await res.json();
    }

    function renderPortfolio() {
      const container = document.getElementById('portfolio');
      container.innerHTML = portfolio.map(entry => `
        <div class="bg-gray-800 p-4 rounded">
          <h3 class="text-lg font-bold">${entry.name} (${entry.symbol.toUpperCase()})</h3>
          <p>Amount: ${entry.amount}</p>
          <p>Current Price: $${entry.price.toLocaleString()}</p>
          <p>Total Value: $${(entry.price * entry.amount).toLocaleString()}</p>
        </div>
      `).join('');
    }

    document.getElementById('tracker-form').addEventListener('submit', async (e) => {
      e.preventDefault();
      const symbol = document.getElementById('coin').value;
      const amount = parseFloat(document.getElementById('amount').value);

      try {
        const coinData = await fetchPrice(symbol);
        portfolio.push({
          name: coinData.name,
          symbol: coinData.symbol,
          amount,
          price: coinData.market_data.current_price.usd
        });
        renderPortfolio();
      } catch (err) {
        alert('Coin not found. Try again.');
      }
    });
  </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Crypto Charts</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body class="bg-gray-900 text-white">
  <header class="bg-gray-800 p-4">
    <h1 class="text-2xl font-bold">Crypto Charts</h1>
    <nav class="mt-2">
      <a href="index.html" class="mr-4 text-blue-400">Market</a>
      <a href="tracker.html" class="mr-4 text-blue-400">Tracker</a>
      <a href="charts.html" class="text-blue-400">Charts</a>
    </nav>
  </header>

  <main class="p-6">
    <h2 class="text-xl font-semibold mb-4">Bitcoin Price (Last 7 Days)</h2>
    <canvas id="btcChart" class="w-full max-w-4xl mx-auto"></canvas>
  </main>

  <script>
    async function loadChartData() {
      const res = await fetch('https://api.coingecko.com/api/v3/coins/bitcoin/market_chart?vs_currency=usd&days=7');
      const data = await res.json();
      const prices = data.prices.map(p => p[1]);
      const labels = data.prices.map(p => new Date(p[0]).toLocaleDateString());

      const ctx = document.getElementById('btcChart').getContext('2d');
      new Chart(ctx, {
        type: 'line',
        data: {
          labels,
          datasets: [{
            label: 'BTC Price (USD)',
            data: prices,
            borderColor: 'rgb(59, 130, 246)',
            backgroundColor: 'rgba(59, 130, 246, 0.2)',
            fill: true,
            tension: 0.3,
          }]
        },
        options: {
          responsive: true,
          plugins: {
            legend: { labels: { color: 'white' } }
          },
          scales: {
            x: { ticks: { color: 'white' } },
            y: { ticks: { color: 'white' } }
          }
        }
      });
    }

    loadChartData();
  </script>
</body>
</html>
