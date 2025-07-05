const mineflayer = require('mineflayer');

function createBot() {
  const bot = mineflayer.createBot({
    host: 'teerth123.aternos.me',
    port: 22159,
    username: 'BOT',
    version: '1.20.1'
  });

  bot.on('spawn', () => {
    console.log('✅ BOT has joined the server!');
    bot.chat('Hello! AFK BOT online ✅');

    // Optional: keep bot moving to prevent AFK kick
    setInterval(() => {
      bot.setControlState('jump', true);
      setTimeout(() => bot.setControlState('jump', false), 500);
    }, 10000);
  });

  bot.on('error', err => {
    console.log('❌ Error:', err.message);
  });

  bot.on('end', () => {
    console.log('🔁 Bot disconnected. Reconnecting...');
    setTimeout(createBot, 5000);
  });
}

createBot();
