
<br/>

<img align="right" height="32px" src="https://www.kela.fi/image/layout_set_logo?img_id=2174196&t=1585229282595">

# Reseptilääkkeiden ostot ATC-luokituksen mukaisesti

## Aineiston kuvaus

Sairausvakuutus maksaa korvausta niiden reseptilääkkeiden
kustannuksista, joille on vahvistettu korvattavuus ja kohtuullinen
tukkuhinta. Lisäksi korvataan lääkkeitä vastaavien valmisteiden
kustannuksia. Lääkkeitä vastaavia valmisteita ovat eräiden vaikeiden
sairauksien hoidossa käytettävät kliiniset ravintovalmisteet ja
pitkäaikaisen ihotaudin hoitoon käytettävät perusvoiteet.

Aineistosta on poistettu ne lääkeaineet, joita on yhtenä tai useampana
viikkona ostanut alle 10 henkilöä.

Aineistossa on mukana tarkastelujakson aikana ostettujen, apteekkien
välityksellä korvattujen lääkkeiden ja vastaavien valmisteiden tiedot
atc-luokan ja sairaanhoitopiirin mukaan viikkotasolla sisältäen
seuraavat muuttujat:

| CODE             | CLASS     | NAME                         | DESCRIPTION                                                                                                                                                                                                                                               |
|:-----------------|:----------|:-----------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ALUEKOODI        | numeric   | Alueen koodi                 | Koko Suomen koodi on 99. SHP-koodit Tilastokeskuksen koodiston mukaiset SHP-tieto perustuu lääkkeen ostajan asuinkuntaan, joka vuoden 2019 osalta perustuu vuoden lopun tietoon ja vuoden 2020 osalta uusimpaan saatavilla olevaan tietoon.               |
| ALUENIMI\_EN     | character | Region name in English       | Region name in English                                                                                                                                                                                                                                    |
| ALUENIMI\_FI     | character | Alueen nimi suomeksi         | Koko Suomi tai sairaanhoitopiirin nimi. SHP-nimet Tilastokeskuksen koodiston mukaiset SHP-tieto perustuu lääkkeen ostajan asuinkuntaan, joka vuoden 2019 osalta perustuu vuoden lopun tietoon ja vuoden 2020 osalta uusimpaan saatavilla olevaan tietoon. |
| ALUENIMI\_SV     | character | Region name in Swedish       | Region name in Swedish                                                                                                                                                                                                                                    |
| ATC\_KOODI       | character | ATC-luokan koodi             | ATC-luokan koodi                                                                                                                                                                                                                                          |
| ATC\_SELITE\_EN  | character | ATC-luokan selite in English | ATC-luokan selite in English                                                                                                                                                                                                                              |
| ATC\_SELITE\_FI  | character | ATC-luokan selite            | ATC-luokan selite suomeksi                                                                                                                                                                                                                                |
| ATC\_SELITE\_SV  | character | ATC-luokan selite på Svenska | ATC-luokan selite på Svenska                                                                                                                                                                                                                              |
| ATC\_TASO        | numeric   | ATC-luokan taso              | ATC-luokan taso. Taso 0 tarkoittaa kaikkia reseptitietoja.                                                                                                                                                                                                |
| UPDATED          | character | Data päivitetty              | Data päivitetty                                                                                                                                                                                                                                           |
| VAR\_KUSTANNUS   | numeric   | Kustannus (€)                | Apteekkien välityksellä korvattujen, tarkastelujakson aikana ostettujen lääkkeiden kustannukset. Kustannuksella tarkoitetaan lääkkeen hinnasta ja apteekin toimitusmaksusta koostuvaa summaa, josta ei ole vielä vähennetty sairausvakuutuskorvausta      |
| VAR\_N\_HENKILOT | integer   | Henkilöiden lukumäärä        | Niiden henkilöiden lukumäärät, jotka ovat tarkastelujakson aikana ostaneet lääkkeitä. Nämä lääkeostot on joko korvattu apteekeissa tai niiden kustannukset ovat jääneet alle 50 euron omavastuun, jolloin ostot ovat vain kerryttäneet omavastuut         |
| VAR\_N\_OSTOT    | integer   | Ostojen lukumäärä            | Ostolla tarkoitetaan yhdellä kertaa apteekista toimitettua tietyn lääkevalmisteen erää. Vuodeksi määrätty lääkevalmiste kirjautuu tilastoon yleensä useana ostona, koska potilas noutaa lääkkeensä tavallisesti kolmen kuukauden välein                   |
| VIIKKO           | numeric   | Viikko                       | Vuoden viikko                                                                                                                                                                                                                                             |
| VUOSI            | numeric   | Vuosi                        | Vuosi                                                                                                                                                                                                                                                     |

## Aineiston käyttäminen

Sovelluksen käyttämä aineisto on vapaasti käytettävissä [Nimeä 4.0
Kansainvälinen (CC BY
4.0)](https://creativecommons.org/licenses/by/4.0/deed.fi)-lisenssin
ehdoilla.

Klikkaa linkistä hiiren oikealla näppäimellä ja valitse “tallenna linkki
nimellä” ja anna tiedostopäätteeksi `csv`.

Itse data on pilkottu vuosittaisiin tiedostoihin

-   Lataa
    <a href="https://github.com/kelaresearchandanalytics/korona_atc_data/raw/master/data_viikko_2019.csv" download="data_viikko_2019.csv">data\_viikko\_2019.csv</a>
-   Lataa
    <a href="https://github.com/kelaresearchandanalytics/korona_atc_data/raw/master/data_viikko_2020.csv" download="data_viikko_2020.csv">data\_viikko\_2020.csv</a>
-   Lataa
    <a href="https://github.com/kelaresearchandanalytics/korona_atc_data/raw/master/data_viikko_2021.csv" download="data_viikko_2021.csv">data\_viikko\_2021.csv</a>
-   Lataa
    <a href="https://github.com/kelaresearchandanalytics/korona_atc_data/raw/master/metadata_viikko.csv" download="metadata_viikko.csv">metadata\_viikko.csv</a>

Aineisto päivittyy kerran viikossa keskiviikkoaamuisin.

## Käyttöesimerkki R-kielellä

**Datojen lataaminen**

``` r
df <- bind_rows(
  readr::read_csv2('https://github.com/kelaresearchandanalytics/korona_atc_data/raw/master/data_viikko_2019.csv'),
  readr::read_csv2('https://github.com/kelaresearchandanalytics/korona_atc_data/raw/master/data_viikko_2020.csv'),
  readr::read_csv2('https://github.com/kelaresearchandanalytics/korona_atc_data/raw/master/data_viikko_2021.csv')
)
head(df)
#> # A tibble: 6 x 15
#>   VUOSI VIIKKO VAR_KUSTANNUS VAR_N_OSTOT VAR_N_HENKILOT ATC_KOODI ATC_SELITE_FI
#>   <dbl>  <dbl>         <dbl>       <dbl>          <dbl> <chr>     <chr>        
#> 1  2019      2     36375566.      956694         528534 <NA>      (NA) NA      
#> 2  2019      3     36919671.      959393         526708 <NA>      (NA) NA      
#> 3  2019      4     37345883.      945287         519017 <NA>      (NA) NA      
#> 4  2019      5     39602251.      991698         540596 <NA>      (NA) NA      
#> 5  2019      6     38800197.     1008379         550861 <NA>      (NA) NA      
#> 6  2019      7     38803541.     1003305         551353 <NA>      (NA) NA      
#> # … with 8 more variables: ATC_SELITE_SV <chr>, ATC_SELITE_EN <chr>,
#> #   ALUEKOODI <dbl>, ATC_TASO <dbl>, ALUENIMI_FI <chr>, ALUENIMI_SV <chr>,
#> #   ALUENIMI_EN <chr>, UPDATED <dttm>
```

``` r
meta <- readr::read_csv2('https://github.com/kelaresearchandanalytics/korona_atc_data/raw/master/metadata_viikko.csv')
head(meta)
#> # A tibble: 6 x 6
#>   CODE    VALUES    CLASS  NAME     DESCRIPTION              UPDATED            
#>   <chr>   <chr>     <chr>  <chr>    <chr>                    <dttm>             
#> 1 ALUENI… Koko Suo… chara… Alueen … Koko Suomi tai sairaanh… 2021-04-01 09:35:41
#> 2 ALUENI… Varsinai… chara… Alueen … Koko Suomi tai sairaanh… 2021-04-01 09:35:41
#> 3 ALUENI… Satakunn… chara… Alueen … Koko Suomi tai sairaanh… 2021-04-01 09:35:41
#> 4 ALUENI… Kanta-Hä… chara… Alueen … Koko Suomi tai sairaanh… 2021-04-01 09:35:41
#> 5 ALUENI… Pirkanma… chara… Alueen … Koko Suomi tai sairaanh… 2021-04-01 09:35:41
#> 6 ALUENI… Päijät-H… chara… Alueen … Koko Suomi tai sairaanh… 2021-04-01 09:35:41
```

**Viivakuvio ATC-luokasta `R`**

``` r
library(ggplot2)
library(dplyr)
options(scipen = 999)
dat <- df %>% 
  filter(ALUEKOODI == 99,
         ATC_KOODI == "R") %>% 
  tidyr::pivot_longer(names_to = "muuttuja", 
                      values_to = "arvo", 
                      cols = starts_with("VAR_")) %>% 
  left_join(meta, by = c("muuttuja" = "CODE")) %>% 
  setNames(tolower(names(.)))

ggplot(dat, aes(x = viikko, y = arvo, color = factor(vuosi))) +
  geom_line() +
  geom_point(size = 2, alpha = .7) +
  facet_wrap(~name , scales = "free", ncol = 1) +
  scale_x_continuous(breaks = 1:max(dat$viikko)) +
        labs(fill = NULL, 
             color = NULL, 
             y = NULL,
             title = unique(dat$atc_selite_fi),
             x = "Viikko") +
        scale_fill_manual(values = c('#e41a1c','#377eb8','#4daf4a')) +
        scale_color_manual(values = c('#e41a1c','#377eb8','#4daf4a')) +
        theme_light(base_family = "PT Sans") +
        theme(legend.position = "top", 
              panel.grid.minor = element_blank()) +
        scale_y_continuous(labels = function(x) format(x, big.mark = " ",
                                                       scientific = FALSE),
                           limits = c(0,NA))
```

![](README-unnamed-chunk-5-1.png)<!-- -->

**Kartta sairaanhoitopiireittäisistä ostomääristä viikolla 12
ATC-luokassa `R`**

``` r
library(geofi)
dat <- df %>% 
  filter(ALUEKOODI != 99,
         VIIKKO == 12,
         ATC_KOODI == "R") %>% 
  select(-VAR_N_OSTOT,-VAR_N_HENKILOT,-UPDATED) %>% 
  left_join(meta, by = c("ATC_KOODI" = "CODE")) %>% 
  setNames(tolower(names(.))) 

# Haetaan kuntadata ja aggregoidaan se sairaanhoitopiiritasolle
muni <- get_municipalities()
shp <- muni %>% 
  group_by(sairaanhoitop_code) %>% 
  summarise()

mapd <- left_join(shp,dat, by = c("sairaanhoitop_code" = "aluekoodi"))

ggplot(mapd, aes(fill = var_kustannus, label = paste0(aluenimi_fi,"\n", var_kustannus ))) +
  geom_sf(color = alpha("white", 1/3)) +
  scale_fill_viridis_b() +
  theme_minimal(base_family = "PT Sans") +
  geom_sf_label(size = 3, color = "white", alpha = .7, family = "PT Sans") +
  facet_wrap(~vuosi) +
  theme(axis.text = element_blank(),
           axis.title = element_blank(),
           panel.grid = element_blank()) +
  labs(title = "ATC-luokan R (Hengityselinten sairauksien lääkkeet) kustannusten \nprosentuaalinen ero 2019 vs. 2020 viikolla 12",
       fill = "%")
```

![](README-unnamed-chunk-6-1.png)<!-- -->
