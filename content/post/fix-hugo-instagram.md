---
title: "[Solved] Fix: Hugo Instagram Embed Shortcode"
slug: fix-hugo-instagram
date: 2020-11-24T02:20:03+08:00
draft: false

type: post

tags:
    - Hugo
    - Instagram

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