---
title: "Kumpulan Survei 3 Nama Paslon 2024"
author: Qauland
description: "PERINGATAN: Pos ini menggunakan Google Chart Embed."
date   : 2023-08-29
lastmod: 2024-02-01
---

Aktifkan mode *desktop* jika grafik terpotong di hape.

---

<iframe width="697" height="431" seamless frameborder="0" scrolling="yes" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vQuDrz4AkQuXAaUJMPCzkZp1gdK_KO89vRw-a274m3kkusQ83SB75ComB4Ir_xzNVNYcZ8KfWmjb767/pubchart?oid=1361067816&amp;format=interactive"></iframe>

<!--
<script src="http://cdnjs.cloudflare.com/ajax/libs/moment.js/2.13.0/moment.min.js"></script>
<script src="http://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.6.0/Chart.bundle.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-trendline@0.1.1/src/chartjs-plugin-trendline.min.js"></script>
<canvas id="chartjs-s3n-canvas" width="1400px" height="900px"></canvas>
<script> //Code adapted from https://embed.plnkr.co/JOI1fpgWIS0lvTeLUxUp/
	
    var timeFormat = 'YYMMDDHH';
    
    Chart.defaults.global.defaultFontColor = 'black';
    Chart.defaults.global.defaultFontFamily = 'sans-serif';
    Chart.defaults.global.defaultFontSize = 14;
	
    var config = {
        type: 'line',
        data: {
            datasets: [
                {
                    label: "Anies",
                    data: [
                        {x: "23040400", y: 25.3 },
                        {x: "23041500", y: 22.4 },
                        {x: "23043000", y: 23   },
                        {x: "23050200", y: 24.6 },
                        {x: "23050500", y: 21.8 },
                        {x: "23050700", y: 19.7 },
                        {x: "23050701", y: 23.6 },
                        {x: "23051000", y: 23.2 },
                        {x: "23051200", y: 21.5 },
                        {x: "23051400", y: 20.8 },
                        {x: "23053000", y: 18.9 },
                        {x: "23061300", y: 31.5 },
                        {x: "23061700", y: 27   },
                        {x: "23062400", y: 21.5 },
                        {x: "23062700", y: 17   },
                        {x: "23062800", y: 16.64},
                        {x: "23062900", y: 20.7 },
                        {x: "23070800", y: 21.4 },
                        {x: "23071900", y: 22.4 },
                        {x: "23072100", y: 23.9 },
                        {x: "23072500", y: 21   },
                        {x: "23080200", y: 26.4 },
                        {x: "23080400", y: 26.9 },
                        {x: "23080700", y: 19.2 },
                        {x: "23080900", y: 22.2 },
                        {x: "23081100", y: 20.4 },
                        {x: "23082000", y: 19.5 },
                        {x: "23082400", y: 20.9 }
                        ],
                    showLine: false,
                    backgroundColor: 'rgba(39, 64, 139, .5)',
                    borderColor: 'rgb(39, 64, 139)',
                    pointBackgroundColor: 'rgba(39, 64, 139, .5)',
                    pointBorderWidth: 1,
                    pointRadius: 5,
                    pointHoverRadius: 7
                },
                {
                    label: "Ganjar",
                    data: [
                        {x: "23040400", y: 26.9 },
                        {x: "23041500", y: 31.1 },
                        {x: "23043000", y: 36.6 },
                        {x: "23050200", y: 25.8 },
                        {x: "23050500", y: 34.4 },
                        {x: "23050700", y: 39.2 },
                        {x: "23050701", y: 38.2 },
                        {x: "23051000", y: 40   },
                        {x: "23051200", y: 34.4 },
                        {x: "23051400", y: 31.9 },
                        {x: "23053000", y: 34.2 }, // cek!
                        {x: "23061300", y: 26.8 },
                        {x: "23061700", y: 34   },
                        {x: "23062400", y: 35.7 },
                        {x: "23062700", y: 37.4 },
                        {x: "23062800", y: 32.4 },
                        {x: "23062900", y: 32.6 },
                        {x: "23070800", y: 32.2 },
                        {x: "23071900", y: 30.8 },
                        {x: "23072100", y: 35.2 },
                        {x: "23072500", y: 30.3 },
                        {x: "23080200", y: 30.4 },
                        {x: "23080400", y: 27   },
                        {x: "23080700", y: 34.1 },
                        {x: "23080900", y: 37   },
                        {x: "23081100", y: 35.9 },
                        {x: "23082000", y: 35.6 },
                        {x: "23082400", y: 33.1 }
                        ],
                    showLine: false,
                    backgroundColor: 'rgba(219, 32, 22, .5)',
                    borderColor: 'rgb(219, 32, 22)',
                    pointBackgroundColor: 'rgba(219, 32, 22, .5)',
                    pointBorderWidth: 1,
                    pointRadius: 5,
                    pointHoverRadius: 7
                },
                {
                    label: "Prabowo",
                    data: [
                        {x: "23040400", y: 30.3 },
                        {x: "23041500", y: 33   },
                        {x: "23043000", y: 33.2 },
                        {x: "23050200", y: 36.5 },
                        {x: "23050500", y: 34.8 },
                        {x: "23050700", y: 32.1 },
                        {x: "23050701", y: 31.1 },
                        {x: "23051000", y: 36.8 },
                        {x: "23051200", y: 35.8 },
                        {x: "23051400", y: 33.9 },
                        {x: "23053000", y: 38   },
                        {x: "23061300", y: 37.2 },
                        {x: "23061700", y: 33   },
                        {x: "23062400", y: 36.8 },
                        {x: "23062700", y: 42.3 },
                        {x: "23062800", y: 32.96},
                        {x: "23062900", y: 40.3 },
                        {x: "23070800", y: 35.8 },
                        {x: "23071900", y: 40.5 },
                        {x: "23072100", y: 33.2 },
                        {x: "23072500", y: 41.7 },
                        {x: "23080200", y: 36.5 },
                        {x: "23080400", y: 41.4 },
                        {x: "23080700", y: 31.3 },
                        {x: "23080900", y: 35.3 },
                        {x: "23081100", y: 33.6 },
                        {x: "23082000", y: 40.8 },
                        {x: "23082400", y: 40.8 }
                        ],
                    showLine: false,
                    backgroundColor: 'rgba(52, 43, 41, .5)',
                    borderColor: 'rgb(52, 43, 41)',
                    pointBackgroundColor: 'rgba(52, 43, 41, .5)',
                    pointBorderWidth: 1,
                    pointRadius: 5,
                    pointHoverRadius: 7
                }
            ]
        },
        options: {
            tooltips: {
                enabled: true,
                callbacks: {
                    label: function(tooltipItem, data) {
                        var label = data.datasets[tooltipItem.datasetIndex].label;
                        var val = data.datasets[tooltipItem.datasetIndex].data[tooltipItem.index];
                        return data.datasets[tooltipItem.datasetIndex].label + ': ' + tooltipItem.yLabel.toLocaleString("id-ID") + '%';
                        //return label + ': ' + val + '%';
                    }
                }
            },
            responsive: true,
            title: {
                display: false,
                text: "Chart.js Time Scale"
            },
            scales: {
                xAxes: [{
                    gridLines: {
                        enabled: true,
                        color: '#303030'
                    },
                    type: "time",
                    ticks: {
                        min: 230528,
                        callback: function(value){return value.toLocaleString("id-ID")}
                    },
                    time: {
                        unit: 'month',
                        displayFormats: {
                        	month: 'MMM YY'
                        },
                        format: timeFormat,
                        tooltipFormat: 'DD MMMM YYYY'
                    },
                    scaleLabel: {
                        display:     false,
                        labelString: 'Date'
                    }
                }],
                yAxes: [{
                    gridLines: {
                        enabled: true,
                        color: '#c0c0c0'
                    },
                    ticks: {
                        min: 0,
                        max: 50,
                        callback: function(value){return value+ "%"}
                    },
                    scaleLabel: {
                        display:     false,
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
        var ctx       = document.getElementById("chartjs-s3n-canvas").getContext("2d");
        window.myLine = new Chart(ctx, config);
    };
</script>
-->

---

## Sekadar info

1. Anies Baswedan--Muhaimin Iskandar

   **Koalisi Perubahan untuk Persatuan** ([*Change for Unity*](https://en.wikipedia.org/wiki/Coalition_of_Change_for_Unity))

   Anggota: Nasdem, PKB, PKS, Ummat (didukung oleh Masyumi, Pelita, PDA, SIRA, PAS Aceh)

   Total kursi DPR: 167 (29,04%)

2. Prabowo Subianto--Gibran Rakabuming Raka

   **Koalisi Indonesia Maju** ([*Advanced Indonesia*](https://en.wikipedia.org/wiki/Advanced_Indonesia_Coalition))

   Anggota: Gerindra, Golkar, Demokrat, PAN, PSI, PBB, Garuda, Gelora (didukung oleh PRIMA, PA)

   Total kursi DPR: 261 (45,39% )

3. Ganjar Pranowo--Mahfud MD

   **Kerja Sama Partai Politik Pengusung Ganjar Pranowo** ([*Alliance of Parties*](https://en.wikipedia.org/wiki/Alliance_of_Political_Parties_Supporting_Ganjar_Pranowo))

   Anggota: PDI-P, PPP, Perindo, Hanura

   Total kursi DPR: 147 (25,57%)

---

## Koreksi/tambahan

-

---

## Survei yang disertakan

Lihat [*Opinion polling for the 2024 Indonesian presidential election*](https://en.wikipedia.org/wiki/Opinion_polling_for_the_2024_Indonesian_presidential_election).

---

## Mungkin ditanya...

- ***Kenapa bikin pos ini?***

  Saya ingin melihat data dari berbagai survei capres 2024 dalam bentuk grafik.

- ***Apa ada sumber inspirasi dalam membuat pos ini?***

  Ada: [ElectionMapsUK](https://electionmaps.uk) dan grafik *polling* saat pilpres Brasil lalu.

- ***Kenapa Anies warna hijau? Kenapa Prabowo warna merah? Kenapa Ganjar warna putih?***

  Warna saya ambil dari warna resmi koalisi masing-masing paslon, kecuali untuk Koalisi Indonesia Maju (pengusung Prabowo--Gibran), saya menggunakan warna latar belakang slogan "Bersama Indonesia Maju" di logo resmi mereka. Ketiga warna tersebut dipilih untuk menghindari bentrokan antarwarna di grafik.

- ***Kenapa ada survei [masukkan nama survei di sini]? Mereka itu tidak akurat!***

  Semua survei itu tidak/kurang akurat. Kalau ada survei yang 100% akurat, ya buat apa ada pilpres.

- ***Ada kesalahan di pos ini!***

  Silakan [buat *issue*](https://github.com/kyunode/kyunode.github.io/issues) di repositori situs ini di GitHub atau [beritahu saya](https://social.vivaldi.net/@kyunode) di Mastodon.
