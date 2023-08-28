---
title: "⚠️ Ujicoba"
author: Qauland
description: "PERINGATAN: Beberapa bagian dari pos ini membutuhkan kuki, serta mungkin berat untuk dimuat dan/atau tidak bekerja sebagaimana mestinya."
date   : 2020-03-22
lastmod: 2023-08-28
---

> PERINGATAN: Anda memasuki pos ujicoba. Beberapa bagian dari pos ini membutuhkan kuki, serta mungkin berat untuk dimuat dan/atau tidak bekerja sebagaimana mestinya.

## Kode sebaris

`If text1.Text = "elementary" Then label1.Caption = "elementaryOS" End If`

## Kode multibaris

```css
@media screen and (min-width:1500px) {
    html { font-size:18px; } /* Increase the font size on higher resolutions */
    .container {max-width:80%;}
}
.mainheading {
    padding: 1rem 0rem;
}

.sidebar {
  position: fixed;
  top: 0;
  bottom: 0;
  left: -14rem;
  width: 14rem;
  visibility: hidden;
  overflow-y: auto;
  font-family: "Inria Sans", Helvetica, Arial, sans-serif;
  font-size: .875rem; /* 15px */
  color: rgba(255,255,255,.6);
  background-color: #202020;
  -webkit-transition: all .3s ease-in-out;
          transition: all .3s ease-in-out;
}

a {
    color: #00ab6b;
    transition: all 0.2s;
}

a:hover {
    color: #038252;
    text-decoration: none;
}

code, kbd, pre, samp {
    font-family: "JetBrains Mono", monospace; /* Sekarang Cascadia Code */
    font-size: 1em;
}
```

## Gambar

Salin pranala gambar yang ingin ditambahkan, lalu ketik `![](<pranala-gambar-di-sini.ekstensi>)` dalam `post.md`. Sebagai contoh:

```
![](<https://i.postimg.cc/L5YGCB75/IMG-20181025-173658.jpg>)
```

![](<https://i.postimg.cc/L5YGCB75/IMG-20181025-173658.jpg>)

<p align="center"><i>©Nitroplus/Norimitsu Kaihou, Sadoru Chiba, Houbunsha/Gakkougurashi Production Committee</i></p>

Untuk menambahkan keterangan hak cipta (seperti di atas), gunakan `<p align="center">`:

```html
<p align="center"><i>©Nitroplus/Norimitsu Kaihou, Sadoru Chiba, Houbunsha/Gakkougurashi Production Committee</i></p>
```

### Khusus untuk situs yang menggunakan tema Minimal Mistakes:

```html
{% capture fig_img %}
![](<https://i.postimg.cc/L5YGCB75/IMG-20181025-173658.jpg>)
{% endcapture %}

{% capture fig_caption %}
©Nitroplus/Norimitsu Kaihou, Sadoru Chiba, Houbunsha/Gakkougurashi Production Committee
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>{{ fig_caption | markdownify | remove: "<p>" | remove: "</p>" }}</figcaption>
</figure>
```

<!--
{% capture fig_img %}
![](<https://i.postimg.cc/L5YGCB75/IMG-20181025-173658.jpg>)
{% endcapture %}

{% capture fig_caption %}
©Nitroplus/Norimitsu Kaihou, Sadoru Chiba, Houbunsha/Gakkougurashi Production Committee
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>{{ fig_caption | markdownify | remove: "<p>" | remove: "</p>" }}</figcaption>
</figure>
-->

Satu pos yang memiliki dua atau lebih gambar *kemungkinan* harus menggunakan lebih dari satu `id` (`fig_img`, `fig_img2`, `fig_img3`, ...)

## Embedded tweet

<blockquote class="twitter-tweet" data-dnt="true" data-theme="dark"><p lang="in" dir="ltr">Ngeliatin orang nangkap cebong <a href="https://t.co/mbDXaX4evU">pic.twitter.com/mbDXaX4evU</a></p>&mdash; Qauland (@kyunode) <a href="https://twitter.com/kyunode/status/1241220387326705666?ref_src=twsrc%5Etfw">March 21, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## Embedded YouTube video

<iframe width="560" height="315" src="https://www.youtube.com/embed/U9nYG2k_z3w" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Embedded Chart.js

<script src="http://cdnjs.cloudflare.com/ajax/libs/moment.js/2.13.0/moment.min.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.4.0/Chart.bundle.js"></script>
<canvas id="canvas" width="100%" height="65%"></canvas>
<script> //Code adapted from https://embed.plnkr.co/JOI1fpgWIS0lvTeLUxUp/
	
    var timeFormat = 'YYMMDD';
    
	Chart.defaults.global.defaultFontFamily = 'Signika Negative';
	
    var config = {
        type:    'line',
        data:    {
            datasets: [
                {
                    label: "Orange",
                    data: [{
                        x: "230804", y: 41.4
                    }, {
                        x: "230807", y: 31.3
                    }, {
                        x: "230530", y: 38
                    }, {
                        x: "230725", y: 41.7
                    }],
                    fill: false,
                    borderColor: 'orange'
                },
                {
                    label: "Skyblue",
                    data:  [{
                        x: "230804", y: 26.9
                    }, {
                        x: "230807", y: 19.2
                    }, {
                        x: "230530", y: 18.9
                    }, {
                        x: "230725", y: 21
                    }],
                    fill:  false,
                    borderColor: 'skyblue'
                }
            ]
        },
        options: {
            responsive: true,
            title:      {
                display: true,
                text:    "Chart.js Time Scale"
            },
            scales:     {
                xAxes: [{
                    type:       "time",
                    time:       {
                        unit: 'day',
                        displayFormats: {
                        	hour: 'DD MMM'
                        },
                        format: timeFormat,
                        tooltipFormat: 'DD MMMM YYYY'
                    },
                    scaleLabel: {
                        display:     true,
                        labelString: 'Date'
                    }
                }],
                yAxes: [{
                    scaleLabel: {
                        display:     true,
                        labelString: 'value'
                    }
                }]
            },
            elements: {
            	line: {
                	tension: 0 // disables bezier curves
            	}
        	}
        }
    };

    window.onload = function () {
        var ctx       = document.getElementById("canvas").getContext("2d");
        window.myLine = new Chart(ctx, config);
    };
</script>

<!--
## Embedded flourish.studio chart

<div class="flourish-embed" data-src="visualisation/308009" data-height="500px"></div><script src="https://public.flourish.studio/resources/embed.js"></script>
-->

## Embedded Google Sheets chart

<iframe width="100%" height="470" style="overflow-x:auto;font-family:'Bitter';" seamless frameborder="0" scrolling="yes" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vR9kIQtLrsjwC9ppMmK5mDaUDQrD9UnEBtba50o5775l-KqvLZ1bmwcFOb1HWyvzA/pubchart?oid=2107131299&amp;format=interactive"></iframe>
