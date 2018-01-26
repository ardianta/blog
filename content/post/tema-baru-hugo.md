---
title: "Membuat Tema Hugo Sendiri"
slug: tema-baru-hugo
date: 2017-12-18T15:49:46+08:00
draft: false

tags:
    - blog
    - hugo

image: "img/tema-baru/index.png"
description: "Menggunakan tema orang lain, rasanya saya kurang bebas. Karena banyak yang tidak dipahami di stuktur tema mereka. Akhirnya saya membuat tema sendiri untuk blog ini."
---

Menggunakan tema orang lain, rasanya saya kurang bebas.
Karena banyak yang tidak dipahami di stuktur tema mereka.

Akhirnya saya membuat tema sendiri untuk blog ini.

### Tema Baru Ardianta

ini isi file `config.toml`:

```toml
baseurl = "https://ardianta.github.io/"
title = "Ardianta"
theme = "ardianta"

googleAnalytics = "UA-54154424-1"
disqusShortname = "ardianta"

[permalinks]
  post = "/blog/:slug/"
  page = "/:slug/"

[params]
  # Site Author
  author = "Dian"

  # Description/subtitle for homepage
  description = "Hello, saya Dian. Blog ini belum jadi. Sabar ya..."
```

ini isi file `archetypes/default.md`:

```markdown
---
title: "{{ replace .TranslationBaseName "-" " " | title }}"
slug: {{ .BaseFileName }}
date: {{ .Date }}
draft: true

meta:
    image: ""
    description: ""
---
```

Lalu untuk layout `index.html` dan `single.html` isinya seperti ini:

file: `themes/ardianta/layouts/index.html`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    {{ partial "head.html" . }}
</head>

<body class="bg-light">

    <div class="container">
        <div class="row align-items-center justify-content-center">
            <div class="col-md-8 mt-5">

                <div class="card rounded-0 post-content">
                    <div class="card-body p-5">


                        {{ partial "header.html" . }} {{ range (.Data.Pages.GroupByDate "2006") }}
                        <table>
                            <tr>
                                <td colspan="3">
                                    <h4>{{ .Key }}</h4>
                                </td>
                            </tr>
                            {{ range where .Pages "Section" "post"}}
                            <tr>
                                <td class="p-1">
                                    <time class="text-secondary small" title="{{ .Date }}">{{ .Date.Format "2 Jan 2006" }}</time>
                                </td>

                                <td class="p-1">
                                    <a class="text-success" href="{{ .RelPermalink }}">{{ .Title }}</a>
                                </td>
                            </tr>
                            {{ end }}
                        </table>
                        {{ end }}

                    </div>
                </div>

                {{ partial "footer.html" . }}
            </div>
        </div>
        <!-- /row -->
    </div>
    <!-- /container -->


</body>

</html>
```

Penampakannya:

![Halaman indeks](/img/tema-baru/index.png)

file: `themes/ardianta/layouts/_default/single.html`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    {{ partial "head.html" . }}
</head>

<body class="bg-light">

    <div class="container mt-5 mb-5">
        <div class="row align-items-center justify-content-center">
            <div class="col-md-8">
                <div class="card rounded-0 post-content">
                    <div class="card-body p-5">
                        {{ partial "header.html" . }}
                        <div class="post-header mb-3">
                            <h2>{{ .Title }}</h2>
                            <time class="text-secondary small" title="{{ .Date }}">{{ .Date.Format "2 Jan 2006" }}</time>
                        </div>
                        <div class="post-body">
                            {{ .Content }}
                        </div>
                        <div class="post-footer mt-5 py-4">
                            
                            {{ if eq .Type "post" }} {{ partial "disqus.html" . }} {{ end }}
                        </div>
                    </div>
                </div>

                 {{ partial "footer.html" . }}
            </div>
        </div>
    </div>

</body>

</html>
```

Penampakannya:

![Halaman Artikel](/img/tema-baru/single.png)

Untuk kode-kode yang lain seperti partial, dapat dilihat di repository ini: https://github.com/ardianta/blog

Untuk tampilan CSS, saya masih mengandalkan Bootstrap 4. Karena belum mampu
membuat CSS sendiri 😄.

## Tampilannya kok sederhana sekali?

Sederhana lebih bagus, karena blog ini akan saya fokuskan 
untuk mencatat saja. Apa yang akan dicatat? Ya, apa saja yang
menarik untuk diacat 😄.

Font yang digunakan sama seperti [Petanikode](https://www.petanikode.com/),
yaitu: Roboto dan Merriweather. Entah mengapa, saya begitu suka dengan kombinasi
dua font ini.

## Apa Selanjutnya?

Tema ini masih belum sempurna. Masih banyak yang harus diperbaiki dan ditambahkan.

Kita lihat saja nanti kelanjutannya.