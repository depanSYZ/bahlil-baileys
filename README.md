WhatsApp Baileys

<p align="center">
  <img src="https://files.catbox.moe/369pux.jpg" alt="Thumbnail" width="400" />
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&color=22C55E&center=true&vCenter=true&width=435&lines=Lightweight+%E2%9A%A1%EF%B8%8F;No+Browser+Required+%F0%9F%9A%80;Full+Features+%F0%9F%94%A5;Multi-Device+Ready+%F0%9F%93%B1" alt="Typing Animation" />
</p>

<div align="center">

https://img.shields.io/github/stars/WhiskeySockets/Baileys?style=for-the-badge&color=yellow
https://img.shields.io/npm/dm/@whiskeysockets/baileys?style=for-the-badge&color=blue
https://img.shields.io/github/issues/WhiskeySockets/Baileys?style=for-the-badge
https://img.shields.io/badge/TypeScript-Ready-3178C6?style=for-the-badge

</div>

WhatsApp Baileys adalah library open-source yang dirancang untuk membantu developer membangun solusi otomatisasi dan integrasi dengan WhatsApp secara efisien dan langsung. Menggunakan teknologi websocket tanpa memerlukan browser, library ini mendukung berbagai fitur seperti manajemen pesan, penanganan chat, administrasi grup, serta pesan interaktif dan tombol aksi untuk pengalaman pengguna yang lebih dinamis.

Dikembangkan dan dipelihara secara aktif, baileys terus menerima pembaruan untuk meningkatkan stabilitas dan performa. Salah satu fokus utama adalah meningkatkan proses pairing dan autentikasi agar lebih stabil dan aman. Fitur pairing dapat disesuaikan dengan kode Anda sendiri, membuat proses lebih andal dan kurang rentan terhadap gangguan.

Library ini sangat cocok untuk membangun bot bisnis, sistem otomatisasi chat, solusi layanan pelanggan, dan berbagai aplikasi otomatisasi komunikasi lainnya yang membutuhkan stabilitas tinggi dan fitur komprehensif. Dengan desain yang ringan dan modular, baileys mudah diintegrasikan ke berbagai sistem dan platform.

---

👨‍💻 Tentang Saya

Halo! Saya depannn 👋

· 📍 Developer WhatsApp Baileys
· 📱 Telegram: @depanncapee
· 💻 Fokus: WhatsApp API, Bot Development, Automation
· 🚀 Motto: "Build fast, scale faster"
· 🗿 Vibes: console.log('Hello World 🗿')

✨ Fitur Utama & Keunggulan

<div align="center">

Fitur Status Keterangan
📱 Pairing Custom ✅ Stabil Proses pairing yang dapat disesuaikan
🔄 Multi-Device ✅ Full Support Kompatibel dengan fitur WhatsApp terbaru
🎨 Pesan Interaktif ✅ Lengkap Tombol, menu, album, polling
💾 Session Management ✅ Otomatis Penyimpanan sesi yang efisien
📊 Poll & Event ✅ Tersedia Polling dan undangan acara
💰 Payment Request ✅ Support Permintaan pembayaran
🛍️ Product Catalog ✅ Ready Katalog produk lengkap
🚀 WebSocket ✅ No Browser Ringan tanpa browser

</div>

🚀 Memulai

Instalasi

```bash
# Menggunakan npm
npm install @whiskeysockets/baileys

# Menggunakan yarn
yarn add @whiskeysockets/baileys

# Menggunakan pnpm
pnpm add @whiskeysockets/baileys
```

Kode Contoh Dasar

```javascript
const makeWASocket = require('@whiskeysockets/baileys').default;
const { useSingleFileAuthState } = require('@whiskeysockets/baileys');

const { state, saveState } = useSingleFileAuthState('./auth_info.json');

const sock = makeWASocket({
  auth: state,
  printQRInTerminal: true
});

sock.ev.on('connection.update', (update) => {
  const { connection, lastDisconnect } = update;
  if (connection === 'close') {
    const shouldReconnect = lastDisconnect.error?.output?.statusCode !== 401;
    if (shouldReconnect) {
      // Reconnect logic here
    }
  } else if (connection === 'open') {
    console.log('✅ Terhubung ke WhatsApp!');
  }
});

sock.ev.on('messages.upsert', async (m) => {
  const msg = m.messages[0];
  if (!msg.key.fromMe && m.type === 'notify') {
    await sock.sendMessage(msg.key.remoteJid, { 
      text: "Halo! Saya bot dari depannn 🗿" 
    });
  }
});
```

📚 Dokumentasi SendMessage

1. 🖼️ Album Message (Multiple Images)

```javascript
await sock.sendMessage(jid, { 
    albumMessage: [
        { image: buffer1, caption: "Foto pertama" },
        { image: { url: "https://example.com/image.jpg" }, caption: "Foto kedua" }
    ] 
}, { quoted: m });
```

2. 📅 Event Message

```javascript
await sock.sendMessage(jid, { 
    eventMessage: { 
        name: "Meetup Developer", 
        description: "Diskusi tentang Baileys", 
        location: { name: "Virtual Meeting" }, 
        startTime: "1763019000", 
        endTime: "1763026200" 
    } 
});
```

3. 📊 Poll Result Message

```javascript
await sock.sendMessage(jid, { 
    pollResultMessage: { 
        name: "Poll Favorite Language", 
        pollVotes: [
            { optionName: "JavaScript", optionVoteCount: "75" },
            { optionName: "Python", optionVoteCount: "25" }
        ] 
    } 
});
```

4. 🎯 Interactive Message (Simple)

```javascript
await sock.sendMessage(jid, {
    interactiveMessage: {
        header: "Menu Utama",
        title: "Pilih opsi:",
        footer: "Telegram: @depanncapee 🗿",
        buttons: [
            {
                name: "cta_copy",
                buttonParamsJson: JSON.stringify({
                    display_text: "📋 Copy Code",
                    copy_code: "BAILEYS-ROCKS"
                })
            }
        ]
    }
});
```

5. 🛍️ Product Message

```javascript
await sock.sendMessage(jid, {
    productMessage: {
        title: "WhatsApp Bot Service",
        description: "Layanan bot WhatsApp custom",
        thumbnail: { url: "https://example.com/product.jpg" },
        productId: "BOT-001",
        priceAmount1000: 500000,
        currencyCode: "IDR",
        buttons: [
            {
                name: "cta_url",
                buttonParamsJson: JSON.stringify({
                    display_text: "🛒 Pesan Sekarang",
                    url: "https://wa.me/628xxx"
                })
            }
        ]
    }
});
```

6. 💰 Request Payment Message

```javascript
await sock.sendMessage(jid, {
    requestPaymentMessage: {
        currency: "IDR",
        amount: 100000,
        from: "628xxx@whatsapp.net",
        note: "Pembayaran layanan bot"
    }
});
```

7. 📄 Document dengan Buffer

```javascript
const fs = require('fs');

await sock.sendMessage(jid, {
    document: fs.readFileSync("./file.pdf"),
    mimetype: "application/pdf",
    fileName: "document.pdf",
    caption: "📄 Document dari depannn"
});
```

🏗️ Struktur Proyek Contoh

```
my-baileys-bot/
├── 📁 node_modules/
├── 📁 src/
│   ├── 📄 index.js          # Entry point utama
│   ├── 📄 handler.js        # Handler pesan
│   └── 📄 utils.js          # Utilities
├── 📄 auth_info.json        # Session storage
├── 📄 package.json
└── 📄 README.md
```

🔧 Konfigurasi Lanjutan

```javascript
const sock = makeWASocket({
  auth: state,
  printQRInTerminal: true,
  mobile: false, // false untuk desktop mode
  browser: ["Baileys Bot", "Chrome", "1.0.0"],
  patchMessageBeforeSending: (message) => {
    const requires = message;
    return requires;
  },
  getMessage: async (key) => {
    // Implementasi caching message
    return {};
  }
});
```

🚨 Troubleshooting

Masalah Solusi
QR Code tidak muncul Pastikan tidak ada session aktif di auth_info.json
Koneksi sering putus Gunakan shouldReconnect logic
Pesan tidak terkirim Periksa format JID (xxx@whatsapp.net)
Session expired Hapus auth_info.json dan scan ulang

📈 Contoh Response Handler

```javascript
sock.ev.on('messages.upsert', async ({ messages }) => {
  const msg = messages[0];
  
  if (msg.message?.conversation?.toLowerCase() === 'ping') {
    await sock.sendMessage(msg.key.remoteJid, { text: 'Pong! 🏓' });
  }
  
  if (msg.message?.imageMessage) {
    await sock.sendMessage(msg.key.remoteJid, { 
      text: 'Gambar diterima! 📸' 
    });
  }
  
  if (msg.message?.buttonsResponseMessage) {
    const selected = msg.message.buttonsResponseMessage.selectedButtonId;
    await sock.sendMessage(msg.key.remoteJid, { 
      text: `Anda memilih: ${selected} ✅` 
    });
  }
});
```

🌟 Kenapa Pilih WhatsApp Baileys?

<div align="center">

```javascript
const reasons = [
  "⚡ Ringan & Cepat",
  "🔒 Aman & Stabil",
  "🔄 Multi-Device Support",
  "🎨 Fitur Lengkap",
  "📚 Dokumentasi Detail",
  "🛠️ Mudah Dikustomisasi",
  "👨‍💻 Komunitas Aktif",
  "🗿 Dikembangkan oleh depannn"
];

console.log(reasons.join('\n'));
```

</div>

🤝 Kontribusi

1. Fork repository
2. Buat branch fitur (git checkout -b fitur-keren)
3. Commit perubahan (git commit -m 'Menambah fitur keren')
4. Push ke branch (git push origin fitur-keren)
5. Buat Pull Request

📞 Kontak & Support

· Developer: depannn
· Telegram: @depanncapee
· Issues: GitHub Issues

<p align="center">
  <b>Dibuat dengan ❤️ oleh depannn</b><br>
  <i>Telegram: @depanncapee 🗿</i>
</p>

<p align="center">
  <img src="https://profile-counter.glitch.me/baileys-readme/count.svg" alt="Visitor Count" />
</p>

<div align="center">

```javascript
// Special thanks to:
const contributors = [
  "WhiskeySockets Team",
  "All Contributors",
  "WhatsApp Web Protocol",
  "You, the awesome user! 🚀"
];
```

</div>

⭐ Jangan lupa star repository ini jika membantu!
🐛 Laporkan bug di GitHub Issues
💡 Punya ide? Join discussion!

Terakhir diperbarui: $(new Date().toLocaleDateString('id-ID'))
