
# Scraping BM-EB

``` r

# --- Install required packages only if missing ---


# --- Load libraries ---
library(rvest)
library(xml2)
library(dplyr)

# --- Define the URL ---
url <- "https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=list&o=1"

# --- Read the HTML content ---
page <- read_html(url)

# --- Extract all <table> elements ---
tables <- page %>% html_nodes("table")

# --- Check how many tables are found ---
length(tables)
#> [1] 1

# --- Convert the first table to a data frame ---
ethno_table <- tables[[1]] %>% html_table(fill = TRUE)

# --- Preview the data ---
glimpse(ethno_table)
#> Rows: 145
#> Columns: 3
#> $ `Hawaiian Name`   <chr> "‘a‘ali‘i", "a‘e (Sapindus)", "a‘e (Zanthoxylem)", "…
#> $ `Scientific Name` <chr> "Dodonaea viscosa", "Sapindus saponaria", "Zanthoxyl…
#> $ `Vernacular Name` <chr> "none", "soapberry", "none", "none", "none", "sedge"…

# Optional: View first rows
head(ethno_table)
#> # A tibble: 6 × 3
#>   `Hawaiian Name`   `Scientific Name`       `Vernacular Name`
#>   <chr>             <chr>                   <chr>            
#> 1 ‘a‘ali‘i          Dodonaea viscosa        none             
#> 2 a‘e (Sapindus)    Sapindus saponaria      soapberry        
#> 3 a‘e (Zanthoxylem) Zanthoxylum (4 species) none             
#> 4 ‘ahakea           Bobea (4 species)       none             
#> 5 ‘āheahea          Chenopodium oahuense    none             
#> 6 ‘ahu‘awa          Cyperus javanicus       sedge

# --- Create 'data' directory if it doesn't exist ---
if (!dir.exists("data")) {
  dir.create("data")
}

# --- Save the table as CSV in the 'data' directory ---
write.csv(ethno_table, file = "data/ethno_table.csv", row.names = FALSE)
```

# Display BM EB Table

``` r

library(knitr)

bmeb <- read.csv("data/ethno_table.csv")

kable(bmeb, caption = "Ethnobotany plants in Bishop Museum")
```

| Hawaiian.Name | Scientific.Name | Vernacular.Name |
|:---|:---|:---|
| ‘a‘ali‘i | Dodonaea viscosa | none |
| a‘e (Sapindus) | Sapindus saponaria | soapberry |
| a‘e (Zanthoxylem) | Zanthoxylum (4 species) | none |
| ‘ahakea | Bobea (4 species) | none |
| ‘āheahea | Chenopodium oahuense | none |
| ‘ahu‘awa | Cyperus javanicus | sedge |
| aiea | Nothocestrum (4 species) | none |
| ‘aka‘akai | Schoenoplectus lacustris | great bulrush |
| ‘ākala | Rubus (2 species) | Hawaiian raspberry |
| ‘ākia | Wikstroemia (12 species) | none |
| ‘akoko | Chamaesyce (16 species) | spurge |
| ‘aākōlea | Athyrium microphyllum | none |
| ‘ākulikuli | Sesuvium portulacastrum | sea purslane |
| ‘āla‘a | Pouteria sandwicensis | none |
| ‘ala‘ala wai nui | Peperomia (24 species) | none |
| alahe‘e | Psydrax odorata | none |
| alani | Melicope (47 species) | none |
| ali‘ipoe | Canna indica | Indian-shot |
| aloalo | Hibiscus (4 species) | none |
| ‘ama‘u | Sadleria cyatheoides | none |
| ‘ape | Alocasia macrorrhizos | elephant’s ear |
| ‘auhuhu | Tephrosia purpurea | none |
| ‘awa | Piper methysticum | kava |
| ‘awapuhi | Zingiber zerumbet | shampoo ginger, wild ginger |
| ‘āwikiwiki | Canavalia (6 species) | none |
| hala | Pandanus tectorius | screw pine |
| hala pepe | Pleomele (6 species) | none |
| hame | Antidesma (2 species) | none |
| hao | Rauvolfia sandwicensis | none |
| hāpu‘u | Cibotium (2 species) | tree fern |
| hau | Hibiscus tiliaceus | none |
| hinahina | Heliotropium anomalum var. argentea | heliotrope |
| hō‘awa | Pittosporum (11 species) | none |
| hoi | Dioscorea bulbifera | bitter yam, air potato |
| hōlei | Ochrosia (4 species) | none |
| ‘ie‘ie | Freycinetia arborea | none |
| ‘iliahi | Santalum (4 species) | sandalwood |
| ‘ilie‘e | Plumbago zeylanica | leadwort |
| ‘ilima | Sida fallax | none |
| ipu | Lagenaria siceraria | bottle gourd |
| kalia | Elaeocarpus bifidus | none |
| kalo | Colocasia esculenta | taro |
| kamani | Calophyllum inophyllum | Alexandrian laurel |
| kauila (Alphitonia) | Alphitonia ponderosa | none |
| kauila (Colubrina) | Colubrina oppositifolia | none |
| kauna‘oa | Cuscuta sandwichiana | dodder |
| kāwa‘u | Ilex anomala | Hawaiian holly |
| kāwelu | Eragrostis variabilis | none |
| kī | Cordyline fruticosa | ti |
| kī nehe | Bidens pilosa | Spanish needle, beggartick |
| kō | Saccharum officinarum | sugarcane |
| koa | Acacia koa | none |
| koai‘a | Acacia koaia | none |
| koali ‘ai | Ipomoea cairica | ivy-leaved morning glory |
| koali ‘awa | Ipomoea indica | none |
| kohekohe | Eleocharis (2 species) | none |
| koki‘o | Kokia & Hibiscus (5 species) | none |
| koki‘o ke‘oke‘o | Hibiscus arnottianus | none |
| kōlea | Myrsine (20 species) | none |
| kolokolo kuahiwi | Lysimachia (2 species) | none |
| kolomona | Senna gaudichaudii | none |
| ko‘oko‘olau | Bidens (19 species) | none |
| kōpiko | Psychotria (11 species) | none |
| kou | Cordia subcordata | none |
| kūkaenēnē, | Coprosma ernodeides | none |
| kūkaepua‘a | Digitaria setigera | itchy crabgrass |
| kukui | Aleurites moluccana | candlenut, tung tree |
| kupukupu | Nephrolepis cordifolia | sword fern |
| la‘amia | Cresentia cujete | calabash tree |
| lama | Diospyros (2 species) | persimmon, ebony |
| laua‘e | Phymatosorus grossus | maile-scented fern |
| laukahi kuahiwi | Plantago (3 species) | plantain |
| lehua papa | Metrosideros rugosa | none |
| loulu | Pritchardia (22 species) | native fan palm |
| ma‘aloa | Neraudia melastomifolia | none |
| mai‘a | Musa x paradisiaca | banana |
| mai‘a hē‘ī | Musa troglodytarum | banana (Tahiti) |
| maile | Alyxia stellata | none |
| makaloa | Cyperus laevigatus | umbrella sedge |
| māmaki | Pipturus (4 species) | none |
| māmane, | Sophora chrysophylla | none |
| manono | Kadua (3 species) | none |
| ma‘o (Abutilon) | Abutilon incanum | hoary abutilon |
| ma‘o (Gossypium) | Gossypium tomentosum | Hawaiian cotton |
| maua | Xylosma hawaiiense | none |
| mau‘u lāili | Sisyrinchium acre | none |
| mēhamehame | Flueggea neowawraea | none |
| milo | Thespesia populnea | portia tree |
| moa | Psilotum nudum | upright whisk fern |
| mokihana | Melicope anisata | none |
| na‘ena‘e | Dubautia (24 species) | none |
| naio | Myoporum sandwicense | false sandalwood, bastard sandalwood |
| nānū | Gardenia (3 species) | Hawaiian gardenia |
| naupaka kahakai | Scaevola taccada | beach naupaka |
| naupaka kuahiwi | Scaevola (9 species) | dwarf naupaka (S. coriacea |
| nehe | Lipochaeta & Melanthera (20 species) | none |
| nīoi | Eugenia (2 species) | none |
| niu | Cocos nucifera | coconut |
| noni | Morinda citrifolia | Indian mulberry |
| nuku ‘i‘iwi | Strongylodon ruber | none |
| ‘ohai | Sesbania tomentosa | none |
| ‘ōhā wai | Clermontia (22 species) | none |
| ‘ohe | Schizostachyum glaucifolium | native bamboo, Polynesian bamboo |
| ‘ōhelo | Vaccinium (3 species) | blueberry |
| ‘ohe makai | Reynoldsia sandwicensis | none |
| ‘ohe ‘ohe | Tetraplasandra (8 species) | none |
| ‘ōhi‘a ‘ai | Syzygium malaccense | mountain apple, Malay apple |
| ‘ōhi‘a hā | Syzygium sandwicensis | none |
| ‘ōhi‘a lehua | Metrosideros (2 species) | none |
| ‘ōkaha | Asplenium nidus | bird’s nest fern |
| ‘ōlapa | Cheirodendron (5 species) | none |
| ‘ōolena | Curcuma longa | turmeric |
| olomea | Perrottetia sandwicensis | none |
| olonā | Touchardia latifolia | none |
| olopua | Nestegis sandwicensis | none |
| ūpuhe | Urera (2 species) | none |
| pā‘ihi | Rorippa sarmentosa | none |
| pa‘iniu | Astelia (3 species) | none |
| pala | Marattia douglasii | none |
| pala‘ā | Sphenomeris chinensis | lace fern |
| palapalai | Microlepia strigosa | lace fern |
| pāmoho | Nephrolepis exaltata subsp. hawaiiensis | sword fern |
| pāpala | Charpetiera (5 species) | none |
| pāpala kōpau | Pisonia (5 species) | none |
| pi‘ia | Dioscorea pentaphylla | pi‘a Hawai‘i, wild yam |
| pia or arrowroot | Tacca leontopetaloides | Polynesian arrowroot |
| pili | Heteropogon contortus | tanglehead, twisted beardgrass, pili grass |
| pilo | Coprosma (12 species) | none |
| pōhinahina | Vitex rotundifolia | beach vitex |
| pōhuehue | Ipomoea pes-caprae | beach morning glory |
| pōpolo | Solanum americanum | glossy nightshade |
| pōpolo kū mai | Phytolacca sandwicensis | pokeberry, pokeweed |
| pua kala | Argemone glauca | prickly poppy |
| pūkiawe | Leptecophylla tameiameiae | none |
| ‘uala | Ipomoea batatas | sweet potato |
| ‘uhaloa | Waltheria indica | none |
| uhi | Dioscorea alata | yam |
| uhiuhi | Caesalpinia kavaiensis | none |
| ‘uki | Machaerina (2 species) | none |
| ‘uki‘uki | Dianella sandwicensis | none |
| ‘ūlei | Osteomeles anthyllidifolia | none |
| ‘ulu | Artocarpus altilis | breadfruit |
| uluhe | Dicranopteris linearis | false staghorn fern |
| wauke | Broussonetia papyrifera | paper mulberry |
| wiliwili | Erythrina sandwicensis | none |

Ethnobotany plants in Bishop Museum
