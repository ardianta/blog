---
title: "[Solved] Fix: Hugo Instagram Embed Shortcode"
slug: fix-hugo-instagram
date: 2020-11-24T02:20:03+08:00
draft: false

type: post

tags:
    - Hugo
    - Instagram
    - Problem Solved

image: "/img/fix-hugo-instagram/error-embed-instagram.png"
description: "Mengatasi Error karena Shortcode instagram tidak lagi bisa melakukan embed"
typora-root-url: ../../static
---

Beberapa hari ini build website saya selalu gagal. Akhirnya beberapa artikel tertunda untuk terbit.

Errornya seperti ini:

![error embed instagram](/img/fix-hugo-instagram/error-embed-instagram.png)

Kalau diperhatikan, error ini disebabkan karena Github Action tidak bisa mengakses API oEmbed Instagram.

Jika saya buka link oEmbed secara manual dari browser, link tersebut bisa memberikan data JSON untuk embed post instagram.

Tapi entah mengapa gagal di akses dari Github Action..

Hmmmm..

Saya coba googling dan mencari solusi, akhirnya ketemu [issue #7879](https://github.com/gohugoio/hugo/issues/7879) di repository Hugo.

Sepertinya Facebook sudah menutup akses untuk mengakses oEmbed Instagram secara publik.

Mau tidak mau kita dipaksa menggunakan APPID dan Client Token.

Solusi yang diberikan [Toni](https://github.com/gohugoio/hugo/issues/7879#issuecomment-719992749) sudah saya coba dengan menambahkan APPID dan Client Token, tapi tidak berhasil.

Akhirnya mencoba cara sendiri.

Dulu pernah tau, kalau kita tambahkan parameter `__a=1` di URL instagram, maka kita akan dapat data JSON dari page tersebut.

Misalnya, kita punya URL seperti ini:

```txt
https://www.instagram.com/p/CH04mIdlmxg/
```

Tinggal tambahkan `__a=1` di belakangnya, sehingga menjadi seperti ini:

```txt
https://www.instagram.com/p/CH04mIdlmxg/?__a=1
```

Maka kita akan mendapatkan JSON seperti ini:

![json instagram](/img/fix-hugo-instagram/json-instagram.png)

Dengan begini, kita bisa membuat custom shortcode untuk embed gambar dari instagram.

Berikut ini shotcode yang saya buat: `layouts/shortcodes/instagram.html`

```go
{{- $pc := .Page.Site.Config.Privacy.Instagram -}}
{{- if not $pc.Disable -}}
    {{- if $pc.Simple -}}
            {{ template "_internal/shortcodes/instagram_simple.html" . }}
    {{- else -}}
            {{ $id := .Get 0 }}
            {{ $hideCaption := cond (eq (.Get 1) "hidecaption") "1" "0" }}
            {{ with getJSON "https://instagram.com/p/" $id "?__a=1" }}
                <figure>
                    <img src="{{ .graphql.shortcode_media.display_url }}" alt="{{ .graphql.shortcode_media.accessibility_caption }}" />
                    {{- if eq $hideCaption "0" -}}
                    {{ $caption := (index .graphql.shortcode_media.edge_media_to_caption.edges 0).node.text }}
                    <figcaption>{{ $caption }}</figcaption>
                    {{ end }}
                </figure>    
            {{ end }}
    {{- end -}}
{{- end -}}
```

Akhirnya masalah ini solved.. yay :tada:

Tapi saya kurang yakin..

Karena mungkin saja link gambar yang didapat dari data JSON ini memiliki session dan hotlink. Sehingga suatu saat akan membuat gambarnya tidak tampil..

..dan jika pihak instagram tau trik ini, mungkin parameter `__a=1` akan diganti dengan yang lain.

Ahh.. yang penting saat ini masalah saya terselesaikan.

## Update — 24/11/2020 02:46 AM

Setelah saya push ke Github dan deploy dengan Github Action, ternyata masih gagal. Huft..

![error-invalid-character](/img/fix-hugo-instagram/error-invalid-character.png)

Error:

```txt
Failed to get JSON resource "https://instagram.com/p/BJaTBjwDXQW?__a=1": invalid character '<' looking for beginning of value
If you feel that this should not be logged as an ERROR, you can ignore it by adding this to your site config:
```

Tapi kalau di localhost bisa.. hmm :thinking:

Mulai ngatuk.. :sleepy:

Besok dilanjutkan.

## Update — 24/11/2020 01:06 PM

Setelah memberikan suara di [issue #7879](https://github.com/gohugoio/hugo/issues/7879) ada yang merespon, bahwa menggunakan *hack* parameter `__a=1` sudah tidak berfungsi lagi.

Berdasarkan infromasi yang saya dapatkan..

Pada tanggal 24 Oktober lalu, akses API untuk oEmbed secara publik memang sudah tidak dibuka oleh Facebook.

Satu-satunya cara adalah dengan memberikan APPID dan Client Token sebagai `access_token`.

Setelah membaca [dokumentasi oEmbed](https://developers.facebook.com/docs/instagram/oembed/), akhirnya paham cara pakainya.

Pertama, kita butuh `access_token` yang terdiri dari APPID dan Client Token.

Untuk APP ID, kita bisa dapatkan dari dashboard Facebook Developer.

![app id](/img/fix-hugo-instagram/app-id.png)

Untuk Client Token, bisa didapatkan dari Settings->Advanced->Security.

![client token](/img/fix-hugo-instagram/client-token.png)

Lalu kita bisa membuatnya menjadi `access_token` dengan format seperti ini:

```txt
<APP_ID>|<client_token>
```

Contoh:

```txt
152759108115365|1aa308265ed111113356557778886
```

Untuk mengetes token ini, bisa dilakukan di [Facebook Debugger](https://developers.facebook.com/tools/debug/accesstoken/).

Contoh hasil tesnya:

![debug token](/img/fix-hugo-instagram/debug-token.png)

Dengan `access_token` ini, serakang kita bisa akses oEmbed API milik Facebook. Pastikan di dashboard app Facebook, oEmbed dalam keadaan aktif.

![oembed aktif](/img/fix-hugo-instagram/oembed-aktif.png)

Cara mengaktifkannya:

Buka saja dashboard lalu klik ***set up*** pada oEmbed.

Terakhir..

Kita bisa buat shortcode instagram untuk Hugo, jadinya seperti ini:

```go
{{- $pc := .Page.Site.Config.Privacy.Instagram -}}
{{- if not $pc.Disable -}}
{{- if $pc.Simple -}}
{{ template "_internal/shortcodes/instagram_simple.html" . }}
{{- else -}}
{{ $id := .Get 0 }}
{{ $access_token := "<APP_ID>|<client_token>" }}
{{ $hideCaption := cond (eq (.Get 1) "hidecaption") "1" "0" }}
{{ with getJSON "https://graph.facebook.com/v9.0/instagram_oembed?url=https://www.instagram.com/p/" $id "/&hidecaption=" $hideCaption "&access_token=" $access_token }}
    {{ .html | safeHTML }}
{{ end }}
{{- end -}}
{{- end -}}
```

Jangan lupa ganti `<APP_ID>` dan `<client_token>`.

Akhirnya, sekarang build dan deploy website saya menjadi lancar.

## Update — 24/07/2021 11:36 AM

Facebook melakukan update lagi dengan API Oembed, sehinga membuat solusi-solusi
di atas tidak berkerja.

Tapi saya coba melakukan embed langsung dari endpoint instagram.

Jadi, berikut ini kode untuk shortcode instagram miliki saya:

```html
{{ $id := .Get 0 }}
{{ $hideCaption := cond (eq (.Get 1) "hidecaption") "1" "0" }}

{{ if not hugo.IsServer }}
{{ with getJSON "https://api.instagram.com/oembed/?url=https://www.instagram.com/p/" $id "/&hidecaption=" $hideCaption }}
    {{ .html | safeHTML }}
{{ end }}
{{ else }}
<style>
  .instagram-embed-placeholder {
    display: flex; 
    align-items: center; 
    justify-content: center;
    gap: .5em; 
    border: 2px dashed silver; 
    height: 360px; 
    margin: 2em 0; 
    border-radius: 8px;
  }
</style>
<div class='instagram-embed-placeholder'>
  <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-instagram" viewBox="0 0 16 16">
    <path d="M8 0C5.829 0 5.556.01 4.703.048 3.85.088 3.269.222 2.76.42a3.917 3.917 0 0 0-1.417.923A3.927 3.927 0 0 0 .42 2.76C.222 3.268.087 3.85.048 4.7.01 5.555 0 5.827 0 8.001c0 2.172.01 2.444.048 3.297.04.852.174 1.433.372 1.942.205.526.478.972.923 1.417.444.445.89.719 1.416.923.51.198 1.09.333 1.942.372C5.555 15.99 5.827 16 8 16s2.444-.01 3.298-.048c.851-.04 1.434-.174 1.943-.372a3.916 3.916 0 0 0 1.416-.923c.445-.445.718-.891.923-1.417.197-.509.332-1.09.372-1.942C15.99 10.445 16 10.173 16 8s-.01-2.445-.048-3.299c-.04-.851-.175-1.433-.372-1.941a3.926 3.926 0 0 0-.923-1.417A3.911 3.911 0 0 0 13.24.42c-.51-.198-1.092-.333-1.943-.372C10.443.01 10.172 0 7.998 0h.003zm-.717 1.442h.718c2.136 0 2.389.007 3.232.046.78.035 1.204.166 1.486.275.373.145.64.319.92.599.28.28.453.546.598.92.11.281.24.705.275 1.485.039.843.047 1.096.047 3.231s-.008 2.389-.047 3.232c-.035.78-.166 1.203-.275 1.485a2.47 2.47 0 0 1-.599.919c-.28.28-.546.453-.92.598-.28.11-.704.24-1.485.276-.843.038-1.096.047-3.232.047s-2.39-.009-3.233-.047c-.78-.036-1.203-.166-1.485-.276a2.478 2.478 0 0 1-.92-.598 2.48 2.48 0 0 1-.6-.92c-.109-.281-.24-.705-.275-1.485-.038-.843-.046-1.096-.046-3.233 0-2.136.008-2.388.046-3.231.036-.78.166-1.204.276-1.486.145-.373.319-.64.599-.92.28-.28.546-.453.92-.598.282-.11.705-.24 1.485-.276.738-.034 1.024-.044 2.515-.045v.002zm4.988 1.328a.96.96 0 1 0 0 1.92.96.96 0 0 0 0-1.92zm-4.27 1.122a4.109 4.109 0 1 0 0 8.217 4.109 4.109 0 0 0 0-8.217zm0 1.441a2.667 2.667 0 1 1 0 5.334 2.667 2.667 0 0 1 0-5.334z"/>
  </svg>
    <a href='https://www.instagram.com/p/{{ $id }}/' target="_blank" rel="noopener">
      Instagram Embed: {{ $id }}
    </a>
</div>
{{ end }}
```

Seperti yang kamu lihat, di sana saya menggunakan endpoin:

```url
https://api.instagram.com/oembed/?url=https://www.instagram.com/p/
```

Entah ini akan bekerja sampai kapan, saya tidak bisa memastikan.

Namun...

Yang terpenting saat ini adalah, saya bisa embed post instagram
dan build dan deploy website saya berhasil. Hehe..