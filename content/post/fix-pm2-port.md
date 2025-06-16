---
title: "[Solved] PM2 Port Already in Use terosss!! 😡"
slug: fix-pm2-port
date: 2025-06-16T20:58:28+08:00
draft: true

type: post

tags:
    - tag

image: ""
description: ""
---

Masalah:

Tidak bisa run project di production maupun di development dengan PM2 dan file `ecosystem.config.js`.
Tapi kalau run dengan `pm2 start src/server.js` aman-aman saja.


```bash
8|api      | 2025-06-15 16:32 +00:00:     at process.processImmediate (node:internal/timers:485:21)
8|api      | 2025-06-15 16:32 +00:00:     at process.callbackTrampoline (node:internal/async_hooks:130:17) {
8|api      | 2025-06-15 16:32 +00:00:   code: 'EADDRINUSE',
8|api      | 2025-06-15 16:32 +00:00:   errno: -98,
8|api      | 2025-06-15 16:32 +00:00:   syscall: 'listen',
8|api      | 2025-06-15 16:32 +00:00:   address: '::',
8|api      | 2025-06-15 16:32 +00:00:   port: 4000
8|api      | 2025-06-15 16:32 +00:00: }
```

Solusi:

Ubah variabel PORT untuk Express server dan WebSocket.

Awalnya seperti ini:

```js
const port = process.env.PORT || 4000;
const socketPort = process.env.PORT || 4001;
```

Menjadi seperti ini:

```js
const port = process.env.PORT || 4000;
const socketPort = process.env.SOCKET_PORT || 4001;
```