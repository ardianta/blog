---
title: "Fix: Hugo Instagram Embed Shortcode"
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

Kalau diperhatikan, error ini disebabkan karena Github Action tidak bisa mengakses API OEmbed Instagram.

Jika saya buka link OEmbed secara manual dari browser, link tersebut bisa memberikan data JSON untuk embed post instagram.

Tapi entah mengapa gagal di akses dari Github Action..

Hmmmm..

Saya coba googling dan mencari solusi, akhirnya ketemu [issue #7879](https://github.com/gohugoio/hugo/issues/7879) di repository Hugo.

Sepertinya Facebook sudah menutup akses untuk mengakses OEmbed Instagram secara publik.

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

— update 24/11/2020 02:46 AM –

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