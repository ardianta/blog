---
title: "Mulai Menggunakan VSNote"
slug: vsnote
date: 2021-08-22T11:57:23+08:00
draft: false

type: post

tags:
    - note
    - Tool

image: "/img/vsnote/vsnote.png"
description: "Akhirnya saya mulai mencoba menggunakan VSNote sebagai catatan pribadi"

typora-root-url: ../../static
---

Hari ini saya mulai menggunakan [VSNote](https://marketplace.visualstudio.com/items?itemName=patricklee.vsnotes) 
untuk mengelola catatan pribadi.

Saya sudah coba beberapa tools, seperti Evernote dan Notion, tapi sepertinya
menulis di teks editor terasa lebih menyenangkan dibandingkan editor berbasis
grafik.

## Apa yang akan saya tulis di VSNote?

Buku catatan pribadi, ya tentunya berisi catatan-catatan penting dan tidak penting
yang ingin saya catat.

Seperti: Diary, Jurnal Mimpi, Ide, Daily Meeting/Standup, dll.

Intinya, tulisan ini tidak akan disebarkan di internet. Hanya saya yang boleh
baca isinya. Hehehe.

Mungkin ada beberapa yang akan saya terbitkan ke internet,
jika itu bermanfaat untuk dibagikan ke banyak orang.

Tetapi untuk hal yang bersifat private, saya tidak akan sebar.

## Giamana Cara Menggunakan VSNote?

Cara menggunakannya sama seperti menulis markdown seperti biasa. Akan tetapi
ada beberapa setup yang perlu dilakukan saat baru pertama kali menginstalnya.

Seperti:

- Setup Folder untuk menyimpan semua catatan
- Setup template untuk beberapa notes

Untuk folder saya menyimpannya di dalam `~/Documents/notes` karena di sana juga
sudah ada catatan-catan sebelumnya.

Cara setup-nya, tekan `Ctrl`+`Shift`+`P` lalu ketik `VSNote: Run stup`.

Maka akan keluar jendela seperti ini:

![Setup awal VSnote](/img/vsnote/vsnote-setup.png)

Tinggal pilih saja folder yang diinginkan untuk menyimpan semua catatan VSNote.

Lalu untuk Template, saya baru membuat template untuk `dialystandup` saja.

Cara membuat template, bisa dibuka pada menu VS Code **Preferences** > **User Snippets** > **Markdown**.

Lalu membuat snippet seperti ini:

```json
{
	// Place your snippets for markdown here. Each snippet is defined under a snippet name and has a prefix, body and 
	// description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	// "Print to console": {
	// 	"prefix": "log",
	// 	"body": [
	// 		"console.log('$1');",
	// 		"$2"
	// 	],
	// 	"description": "Log output to console"
	// }

	"vsnote_template_dailystandup": {
		"prefix": "vsnote_template_dailystandup",
		"body": [
			"---",
			"date: $CURRENT_DATE/$CURRENT_MONTH/$CURRENT_YEAR",
			"tags:",
			"\t- dailystandup",
			"---",
			"\n# Apa yang sudah dikerjakan kemarin?",
			"\n# Apa saja kendala yang dihadapi?",
			"\n# Apa yang bisa dilakukan untuk improve?",
			"\n# Apa yang akan dikerjakan hari ini?",
		],
		"description": "Daily Standup Meeting Template",
	},
}
```

Setelah itu baru digunakan pada konfigurasi VSNote:

```json
"vsnotes.templates": [
  "dailystandup",
],
```

## Menyimpan Catatan ke Git

VSNote menyediakan fitur untuk melakukan commit dan push catatan ke repository Git.

Kita bisa gunakan Github dan juga Gitlab untuk menyimpan catatan.

Caranya:

Setup repository git di dalam folder tempat kita menyimpan catatan.

```bash
cd ~/Documents/notes
git init .
git add .
git coomit -m "initial commit"
git branch -m master main # ini opsional
git remote add origin git@github.com:<username>/<repositorty>.git
git push --all
```

Setelah itu, coba buat catatan baru.

Lalu simpan dan tekan `Ctrl`+`Shift`+`P` dan ketik `VSNote: Commit and Push`.
Maka perubahan atau catatan akan otomatis disimpan ke dalam repository Git.

## Kendala yang dihadapi

Saat menjalanakan scan folder, saya mendapatkan error seperti ini:

![Permission error](/img/vsnote/permission-error.png)

Ini disebabakan karena user yang saya gunakan belum memiliki akses ke folder tersebut.

✅ Solusinya:

Berdasarkan jawaban yang saya dapatkan di [Stackoverflow](https://stackoverflow.com/a/49975558),
kita harus mengatur owrnership dari folder tersebut.

```bash
sudo chown -R $USER:$GROUP ~/.cache/dconf
```

Maka sekarang masalah ini sudah teratasi.

## Apa Selanjutnya?

Saat berpindah dari Notion ke VSNote, saya berpikir:

"Gimana caranya sinkronkan catatan yang di Notion dengan VSNote?"

Mungkin saat ini saya belum tahu caranya, tapi mungkin bisa.

Untuk saat ini saya bisa menulis dailystandup, diary, jurnal mimpi, dan
catatan-catatan lainnya tanpa harus membuka Notions dan terknoeksi internet.

Lalu kalau mau menulis dari Hp, tinggal clone repositorynya lewat Termux
dan menulis dengan aplikasi editor Markdown di HP.

Tapi saya jarang nulis dari HP, lebih enak nulis di Komputer hehe.