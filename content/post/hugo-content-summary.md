---
title: "[Solved] Hugo Content Summary Rendering"
slug: hugo-content-summary
date: 2025-01-25T15:49:15+08:00
draft: false

type: post

tags:
    - tag

image: "/img/hugo-content-summary/hugo-summary-return-html.png"
description: "Sekarang Hugo akan menghasilkan kode HTML begitu kita pakai variabel `.Summary`.
Dulunya cuma menghasilkan plain text aja. Tapi setelah saya upgrade versi Hugo,
template di blog saya menjadi berubah dan rusak"
---

Sekarang Hugo akan menghasilkan kode HTML begitu kita pakai variabel `.Summary`.
Dulunya cuma menghasilkan plain text. Tapi setelah saya upgrade versi Hugo,
template di blog saya menjadi seperti ini:

![Hugo summary return HTML](/img/hugo-content-summary/hugo-summary-return-html.png)

Saya belum tau, perubahan ini terjadi di versi berapa. Karena saya belum cek semua release notes Hugo hehe.

Perubahan ini membuat template blog saya jadi rusak dan tidak konsisten.
Kode Hugo yang menampilkan bagian itu seperti ini:

```html
<p class="text-slate-600 line-clamp-3 text-sm mb-2">
  {{ with .Description }}{{ . }}{{ else }}{{ .Summary | markdownify | strings.Truncate 42 }}{{ end }}
</p>
```

Meskipun di sini saya sudah menggunakan fungsi `markdownify` dan `string.Truncate` untuk memotongnya,
tapi tetap saja hasilnya berupa HTML.

Hasil rendernya jika di-inspect jadi seperti ini:

![Hasil render summary di inspect element](/img/hugo-content-summary/hasil-render-summary.png)

Terlihat aneh di sini. Saya coba cek di [dokumentasi](https://gohugo.io/methods/page/summary/), 
ternyata variabel `.Summary` sekarang menhasilkan output `template.HTML`.

Kalau dulu sih cuma menghasilkan plain text aja.

Lalu gimana cara memperbaikinya?

## Cara Pertama 

Cara pertama bisa menggunakan fungsi `plaintify` pada `.Summary` jadi seperti ini:

```
<p class="text-slate-600 line-clamp-3 text-sm mb-2">
  {{ with .Description }}{{ . }}{{ else }}{{ .Summary | plaintify }}{{ end }}
</p>
```

Fungsi `plaintify` akan mengubah hasil `.Summary` yang berupa HTML menjadi plain text.

## Cara Kedua

Cara kedua saya memperbaikinya dengan menggunakan variabel `.Plain`.
Variabel ini akan menghasilkan plain text dari content secara full.
Lalu menggunakan fungsi `strings.Truncate` untuk memotongnya.

Sehingga template layoutnya jadi seperti ini:

```html
<p class="text-slate-600 line-clamp-3 text-sm mb-2">
  {{ with .Description }}{{ . }}{{ else }}{{ .Plain | strings.Truncate 128 }}{{ end }}
</p>
```

`128` adalah panjang maksimal teks dari content (plain) yang akan dipakai sebagai summary.

Maka hasilnya:

![Hasil render .Plan](/img/hugo-content-summary/hasil-render-plain.png)

## Cara Ketiga

Cara lain, kita bisa tambahkan font-matter `summary` di semua post yang belum ada `summary`
atauapun `description` nya.

Contohnya seperti ini:

```markdown
---
summary: "Berisi teks ringkasan tentang post atau konten"
---
```

## Akhir Kata..

Selamat mencoba!