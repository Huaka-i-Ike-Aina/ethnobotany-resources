
# Scraping BM-EB

``` r
# --- Install required packages only if missing ---


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
#> $ `Hawaiian Name`   <chr> "‘a‘ali‘i", "a‘e (Sapindus)", "a‘e (Z…
#> $ `Scientific Name` <chr> "Dodonaea viscosa", "Sapindus saponar…
#> $ `Vernacular Name` <chr> "none", "soapberry", "none", "none", …

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

## Display BM EB Table

``` r
bmeb <- read.csv("data/ethno_table.csv")

kable(bmeb, caption = "Ethnobotany plants in Bishop Museum")
```

| Hawaiian.Name       | Scientific.Name                         | Vernacular.Name                            |
|:--------------------|:----------------------------------------|:-------------------------------------------|
| ’a‘ali‘i            | Dodonaea viscosa                        | none                                       |
| a‘e (Sapindus)      | Sapindus saponaria                      | soapberry                                  |
| a‘e (Zanthoxylem)   | Zanthoxylum (4 species)                 | none                                       |
| ’ahakea             | Bobea (4 species)                       | none                                       |
| ’āheahea            | Chenopodium oahuense                    | none                                       |
| ’ahu‘awa            | Cyperus javanicus                       | sedge                                      |
| aiea                | Nothocestrum (4 species)                | none                                       |
| ’aka‘akai           | Schoenoplectus lacustris                | great bulrush                              |
| ’ākala              | Rubus (2 species)                       | Hawaiian raspberry                         |
| ’ākia               | Wikstroemia (12 species)                | none                                       |
| ’akoko              | Chamaesyce (16 species)                 | spurge                                     |
| ’aākōlea            | Athyrium microphyllum                   | none                                       |
| ’ākulikuli          | Sesuvium portulacastrum                 | sea purslane                               |
| ’āla‘a              | Pouteria sandwicensis                   | none                                       |
| ’ala‘ala wai nui    | Peperomia (24 species)                  | none                                       |
| alahe‘e             | Psydrax odorata                         | none                                       |
| alani               | Melicope (47 species)                   | none                                       |
| ali‘ipoe            | Canna indica                            | Indian-shot                                |
| aloalo              | Hibiscus (4 species)                    | none                                       |
| ’ama‘u              | Sadleria cyatheoides                    | none                                       |
| ’ape                | Alocasia macrorrhizos                   | elephant’s ear                             |
| ’auhuhu             | Tephrosia purpurea                      | none                                       |
| ’awa                | Piper methysticum                       | kava                                       |
| ’awapuhi            | Zingiber zerumbet                       | shampoo ginger, wild ginger                |
| ’āwikiwiki          | Canavalia (6 species)                   | none                                       |
| hala                | Pandanus tectorius                      | screw pine                                 |
| hala pepe           | Pleomele (6 species)                    | none                                       |
| hame                | Antidesma (2 species)                   | none                                       |
| hao                 | Rauvolfia sandwicensis                  | none                                       |
| hāpu‘u              | Cibotium (2 species)                    | tree fern                                  |
| hau                 | Hibiscus tiliaceus                      | none                                       |
| hinahina            | Heliotropium anomalum var. argentea     | heliotrope                                 |
| hō‘awa              | Pittosporum (11 species)                | none                                       |
| hoi                 | Dioscorea bulbifera                     | bitter yam, air potato                     |
| hōlei               | Ochrosia (4 species)                    | none                                       |
| ’ie‘ie              | Freycinetia arborea                     | none                                       |
| ’iliahi             | Santalum (4 species)                    | sandalwood                                 |
| ’ilie‘e             | Plumbago zeylanica                      | leadwort                                   |
| ’ilima              | Sida fallax                             | none                                       |
| ipu                 | Lagenaria siceraria                     | bottle gourd                               |
| kalia               | Elaeocarpus bifidus                     | none                                       |
| kalo                | Colocasia esculenta                     | taro                                       |
| kamani              | Calophyllum inophyllum                  | Alexandrian laurel                         |
| kauila (Alphitonia) | Alphitonia ponderosa                    | none                                       |
| kauila (Colubrina)  | Colubrina oppositifolia                 | none                                       |
| kauna‘oa            | Cuscuta sandwichiana                    | dodder                                     |
| kāwa‘u              | Ilex anomala                            | Hawaiian holly                             |
| kāwelu              | Eragrostis variabilis                   | none                                       |
| kī                  | Cordyline fruticosa                     | ti                                         |
| kī nehe             | Bidens pilosa                           | Spanish needle, beggartick                 |
| kō                  | Saccharum officinarum                   | sugarcane                                  |
| koa                 | Acacia koa                              | none                                       |
| koai‘a              | Acacia koaia                            | none                                       |
| koali ’ai           | Ipomoea cairica                         | ivy-leaved morning glory                   |
| koali ’awa          | Ipomoea indica                          | none                                       |
| kohekohe            | Eleocharis (2 species)                  | none                                       |
| koki‘o              | Kokia & Hibiscus (5 species)            | none                                       |
| koki‘o ke‘oke‘o     | Hibiscus arnottianus                    | none                                       |
| kōlea               | Myrsine (20 species)                    | none                                       |
| kolokolo kuahiwi    | Lysimachia (2 species)                  | none                                       |
| kolomona            | Senna gaudichaudii                      | none                                       |
| ko‘oko‘olau         | Bidens (19 species)                     | none                                       |
| kōpiko              | Psychotria (11 species)                 | none                                       |
| kou                 | Cordia subcordata                       | none                                       |
| kūkaenēnē,          | Coprosma ernodeides                     | none                                       |
| kūkaepua‘a          | Digitaria setigera                      | itchy crabgrass                            |
| kukui               | Aleurites moluccana                     | candlenut, tung tree                       |
| kupukupu            | Nephrolepis cordifolia                  | sword fern                                 |
| la‘amia             | Cresentia cujete                        | calabash tree                              |
| lama                | Diospyros (2 species)                   | persimmon, ebony                           |
| laua‘e              | Phymatosorus grossus                    | maile-scented fern                         |
| laukahi kuahiwi     | Plantago (3 species)                    | plantain                                   |
| lehua papa          | Metrosideros rugosa                     | none                                       |
| loulu               | Pritchardia (22 species)                | native fan palm                            |
| ma‘aloa             | Neraudia melastomifolia                 | none                                       |
| mai‘a               | Musa x paradisiaca                      | banana                                     |
| mai‘a hē‘ī          | Musa troglodytarum                      | banana (Tahiti)                            |
| maile               | Alyxia stellata                         | none                                       |
| makaloa             | Cyperus laevigatus                      | umbrella sedge                             |
| māmaki              | Pipturus (4 species)                    | none                                       |
| māmane,             | Sophora chrysophylla                    | none                                       |
| manono              | Kadua (3 species)                       | none                                       |
| ma‘o (Abutilon)     | Abutilon incanum                        | hoary abutilon                             |
| ma‘o (Gossypium)    | Gossypium tomentosum                    | Hawaiian cotton                            |
| maua                | Xylosma hawaiiense                      | none                                       |
| mau‘u lāili         | Sisyrinchium acre                       | none                                       |
| mēhamehame          | Flueggea neowawraea                     | none                                       |
| milo                | Thespesia populnea                      | portia tree                                |
| moa                 | Psilotum nudum                          | upright whisk fern                         |
| mokihana            | Melicope anisata                        | none                                       |
| na‘ena‘e            | Dubautia (24 species)                   | none                                       |
| naio                | Myoporum sandwicense                    | false sandalwood, bastard sandalwood       |
| nānū                | Gardenia (3 species)                    | Hawaiian gardenia                          |
| naupaka kahakai     | Scaevola taccada                        | beach naupaka                              |
| naupaka kuahiwi     | Scaevola (9 species)                    | dwarf naupaka (S. coriacea                 |
| nehe                | Lipochaeta & Melanthera (20 species)    | none                                       |
| nīoi                | Eugenia (2 species)                     | none                                       |
| niu                 | Cocos nucifera                          | coconut                                    |
| noni                | Morinda citrifolia                      | Indian mulberry                            |
| nuku ’i‘iwi         | Strongylodon ruber                      | none                                       |
| ’ohai               | Sesbania tomentosa                      | none                                       |
| ’ōhā wai            | Clermontia (22 species)                 | none                                       |
| ’ohe                | Schizostachyum glaucifolium             | native bamboo, Polynesian bamboo           |
| ’ōhelo              | Vaccinium (3 species)                   | blueberry                                  |
| ’ohe makai          | Reynoldsia sandwicensis                 | none                                       |
| ’ohe ’ohe           | Tetraplasandra (8 species)              | none                                       |
| ’ōhi‘a ’ai          | Syzygium malaccense                     | mountain apple, Malay apple                |
| ’ōhi‘a hā           | Syzygium sandwicensis                   | none                                       |
| ’ōhi‘a lehua        | Metrosideros (2 species)                | none                                       |
| ’ōkaha              | Asplenium nidus                         | bird’s nest fern                           |
| ’ōlapa              | Cheirodendron (5 species)               | none                                       |
| ’ōolena             | Curcuma longa                           | turmeric                                   |
| olomea              | Perrottetia sandwicensis                | none                                       |
| olonā               | Touchardia latifolia                    | none                                       |
| olopua              | Nestegis sandwicensis                   | none                                       |
| ūpuhe               | Urera (2 species)                       | none                                       |
| pā‘ihi              | Rorippa sarmentosa                      | none                                       |
| pa‘iniu             | Astelia (3 species)                     | none                                       |
| pala                | Marattia douglasii                      | none                                       |
| pala‘ā              | Sphenomeris chinensis                   | lace fern                                  |
| palapalai           | Microlepia strigosa                     | lace fern                                  |
| pāmoho              | Nephrolepis exaltata subsp. hawaiiensis | sword fern                                 |
| pāpala              | Charpetiera (5 species)                 | none                                       |
| pāpala kōpau        | Pisonia (5 species)                     | none                                       |
| pi‘ia               | Dioscorea pentaphylla                   | pi‘a Hawai‘i, wild yam                     |
| pia or arrowroot    | Tacca leontopetaloides                  | Polynesian arrowroot                       |
| pili                | Heteropogon contortus                   | tanglehead, twisted beardgrass, pili grass |
| pilo                | Coprosma (12 species)                   | none                                       |
| pōhinahina          | Vitex rotundifolia                      | beach vitex                                |
| pōhuehue            | Ipomoea pes-caprae                      | beach morning glory                        |
| pōpolo              | Solanum americanum                      | glossy nightshade                          |
| pōpolo kū mai       | Phytolacca sandwicensis                 | pokeberry, pokeweed                        |
| pua kala            | Argemone glauca                         | prickly poppy                              |
| pūkiawe             | Leptecophylla tameiameiae               | none                                       |
| ’uala               | Ipomoea batatas                         | sweet potato                               |
| ’uhaloa             | Waltheria indica                        | none                                       |
| uhi                 | Dioscorea alata                         | yam                                        |
| uhiuhi              | Caesalpinia kavaiensis                  | none                                       |
| ’uki                | Machaerina (2 species)                  | none                                       |
| ’uki‘uki            | Dianella sandwicensis                   | none                                       |
| ’ūlei               | Osteomeles anthyllidifolia              | none                                       |
| ’ulu                | Artocarpus altilis                      | breadfruit                                 |
| uluhe               | Dicranopteris linearis                  | false staghorn fern                        |
| wauke               | Broussonetia papyrifera                 | paper mulberry                             |
| wiliwili            | Erythrina sandwicensis                  | none                                       |

Ethnobotany plants in Bishop Museum

# Webcrawler

Coded with assistance from ChatGPT.

Currently should have the following functionality:

-   Scrapes all pages with pagination,
-   Pulls all depth-2 details,
-   Normalizes them into a single `data.table`,
-   Polite throttling included, and
-   Can resume if interrupted.

``` r
                                        # Base URL (pagination placeholder)
base_url_template <- "https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=list&o=%d"

                                        # Output files for resume
depth1_file <- "data/ethnobotany_depth1_progress.csv"
final_file  <- "data/ethnobotany_full_normalized.csv"

                                        # ---- Step 1: Load existing depth-1 data if resuming ----
if (file.exists(depth1_file)) {
    depth1_dt <- fread(depth1_file)
    message("Resuming with ", nrow(depth1_dt), " depth-1 rows already scraped.")
} else {
    depth1_dt <- data.table()
}
#> Resuming with 27260 depth-1 rows already scraped.

                                        # ---- Step 2: Scrape depth-1 pages ----
scrape_depth1_page <- function(page_number) {
    url <- sprintf(base_url_template, page_number)
    message("Scraping depth-1 page: ", url)

    page <- tryCatch(read_html(url), error = function(e) return(NULL))
    if (is.null(page)) return(NULL)

    tbl_node <- page %>% html_node("table")
    if (is.na(tbl_node) || length(tbl_node) == 0) return(NULL)

    main_table <- tbl_node %>% html_table(fill = TRUE)
    if (nrow(main_table) == 0) return(NULL)

    dt <- as.data.table(main_table)
    setnames(dt, make.names(names(dt), unique = TRUE))

                                        # Hawaiian Name links
    hawaiian_nodes <- page %>%
        html_nodes("table tr td:nth-child(1) a")

    hawaiian_links <- hawaiian_nodes %>%
        html_attr("href") %>%
        url_absolute(url)

    dt[, Detail_URL := hawaiian_links]

    Sys.sleep(runif(1, 1, 3))  # polite random pause
    return(dt)
}

                                        # If no depth-1 data yet, start scraping from page 1
if (nrow(depth1_dt) == 0) {
    all_depth1 <- list()
    page_number <- 1

    repeat {
        dt <- scrape_depth1_page(page_number)
        if (is.null(dt)) break
        all_depth1[[length(all_depth1) + 1]] <- dt
        depth1_dt <- rbindlist(all_depth1, fill = TRUE)
        fwrite(depth1_dt, depth1_file)  # save progress
        page_number <- page_number + 1
    }
}

                                        # ---- Step 3: Scrape depth-2 detail pages ----
scrape_detail_page <- function(url) {
    message("   Depth-2: ", url)

    page <- tryCatch(read_html(url), error = function(e) return(NULL))
    if (is.null(page)) return(list())

    detail_tables <- page %>%
        html_nodes("table") %>%
        html_table(fill = TRUE)

    if (length(detail_tables) == 0) return(list())

    detail_df <- detail_tables[[1]]

    if (ncol(detail_df) >= 2) {
        labels <- str_trim(detail_df[[1]])
        values <- str_trim(detail_df[[2]])
        names(values) <- make.names(labels, unique = TRUE)
        values <- as.list(values)
    } else {
        values <- list()
    }

    Sys.sleep(runif(1, 1, 3))  # polite random pause
    return(values)
}

                                        # ---- Step 4: Resume-aware depth-2 scraping ----
if (file.exists(final_file)) {
    final_dt <- fread(final_file)
    scraped_urls <- unique(final_dt$Detail_URL)
} else {
    final_dt <- NULL
    scraped_urls <- character()
}

                                        # Filter only URLs we haven't scraped yet
pending_urls <- setdiff(depth1_dt$Detail_URL, scraped_urls)
message("Depth-2 pages remaining: ", length(pending_urls))
#> Depth-2 pages remaining: 0

                                        # Scrape only pending detail pages
detail_list <- map(pending_urls, scrape_detail_page)

                                        # Convert to data.table
details_dt <- rbindlist(detail_list, fill = TRUE)

                                        # Match them back to depth1 rows
new_data <- depth1_dt[Detail_URL %in% pending_urls]
final_batch <- cbind(new_data, details_dt)

                                        # Append to final dataset
if (!is.null(final_dt)) {
    final_dt <- rbindlist(list(final_dt, final_batch), fill = TRUE)
} else {
    final_dt <- final_batch
}

                                        # Save progress
fwrite(final_dt, final_file)

                                        # Prep final_dt for depth 2 crawling
colnames(final_dt)[grepl("URL", colnames(final_dt))] <- "URL"
final_dt[["depth"]] <- rep(2, dim(final_dt)[1])
```

# Depth 2 Crawler

``` r
# Text helpers
clean_txt <- function(x) {
  x <- gsub("\u00A0", " ", x)          # NBSP -> space
  x <- gsub("\\s+", " ", x)
  stringr::str_squish(x)
}
esc_re <- function(x) gsub("([][{}()+*^$|?.\\-\\\\])", "\\\\\\1", x)

# Canonical label mapping (extend as needed)
canon_label <- function(label) {
  L <- tolower(clean_txt(gsub("[:]+\\s*$", "", label)))
  patterns <- list(
    "Hawaiian Name(s)" = "^hawaiian\\s+name(s)?$",
    "Scientific Name"  = "^scientific\\s+name$|^species$|^binomial$|^taxon$",
    "Vernacular Name"  = "^vernacular\\s+name(s)?$|^common\\s+name(s)?$|^english\\s+name(s)?$",
    "Family"           = "^family$",
    "Status"           = "^status$|^native\\s*status$|^endemic( status)?$",
    "Part Used"        = "^part(s)?\\s+used$",
    "Uses"             = "^use(s)?$|^traditional\\s+use(s)?$|^uses(/|\\s+)practices$",
    "Medicinal"        = "^medicinal$|^medicine$",
    "Habitat"          = "^habitat$",
    "Distribution"     = "^distribution$|^location(s)?$|^island(s)?$",
    "References"       = "^reference(s)?$|^sources?$",
    "Notes"            = "^note(s)?$|^remarks$"
  )
  for (k in names(patterns)) if (grepl(patterns[[k]], L, perl = TRUE)) return(k)
  # Fallback: keep original label (trimmed)
  sub(":\\s*$", "", clean_txt(label))
}

# Extract label/value pairs from a content node
extract_fields <- function(content_node) {
  fields <- list()
  addf <- function(label, value) {
    lbl <- canon_label(label)
    val <- clean_txt(value)
    if (!nzchar(lbl) || !nzchar(val)) return(invisible())
    if (is.null(fields[[lbl]])) fields[[lbl]] <- val
    else fields[[lbl]] <- paste(fields[[lbl]], val, sep = "\n")
  }

  # 1) Definition lists: <dt>Label</dt><dd>Value</dd>
  for (dl in rvest::html_elements(content_node, "dl")) {
    dts <- rvest::html_elements(dl, "dt"); dds <- rvest::html_elements(dl, "dd")
    n <- min(length(dts), length(dds))
    for (i in seq_len(n)) addf(rvest::html_text2(dts[[i]]), rvest::html_text2(dds[[i]]))
  }

  # 2) Tables: assume first cell is label, rest are value
  for (tbl in rvest::html_elements(content_node, "table")) {
    for (tr in rvest::html_elements(tbl, "tr")) {
      cells <- rvest::html_elements(tr, "th, td")
      if (length(cells) >= 2) {
        label <- rvest::html_text2(cells[[1]])
        vals <- vapply(cells[-1], rvest::html_text2, "", USE.NAMES = FALSE)
        vals <- vals[nzchar(vals)]
        if (length(vals)) addf(label, paste(vals, collapse = " | "))
      }
    }
  }

  # 3) Bold/strong label at start of paragraph/list item
  for (parent in rvest::html_elements(content_node, "p, li")) {
    b <- rvest::html_element(parent, "strong, b")
    if (!inherits(b, "xml_missing") && length(b) > 0) {
      label <- clean_txt(rvest::html_text2(b))
      par_txt <- rvest::html_text2(parent)
      if (nzchar(label) && nzchar(par_txt)) {
        pattern <- paste0("^\\s*", esc_re(label), "\\s*:?\\s*")
        value <- clean_txt(sub(pattern, "", par_txt, perl = TRUE))
        if (nzchar(value)) addf(label, value)
      }
    }
  }

  # 4) Plain "Label: Value" lines (no bold)
  known_left <- c("Hawaiian Name", "Hawaiian Name(s)", "Scientific Name", "Vernacular Name",
                  "Common Name", "English Name", "Family", "Status", "Part Used", "Uses",
                  "Medicinal", "Habitat", "Distribution", "References", "Notes")
  left_re <- paste0("^\\s*(", paste(unique(known_left), collapse="|"), ")\\s*:\\s*(.+)$")
  for (node in rvest::html_elements(content_node, "p, li, div")) {
    txt <- rvest::html_text2(node)
    if (!nzchar(txt)) next
    m <- regexec(left_re, txt, ignore.case = TRUE)
    rr <- regmatches(txt, m)[[1]]
    if (length(rr) >= 3) addf(rr[2], rr[3])
  }

  fields
}

# Choose content container
choose_content_node <- function(doc, selectors = c("#content","div#content","#main","main","article",".content","#mw-content-text","body")) {
  for (sel in selectors) {
    node <- rvest::html_element(doc, sel)
    if (!inherits(node, "xml_missing") && length(node) > 0) return(node)
  }
  rvest::html_element(doc, "body")
}

# Scrape one URL -> one-row data.table (wide)
scrape_one <- function(url,
                       ua = "ethnobotany-resources/0.1 (+https://github.com/stacyllyn/ethnobotany-resources)",
                       timeout_sec = 30) {
  safe_row <- function(error = NA_character_, status = NA_integer_, title = NA_character_) {
    data.table(url = url, page_title = title, status = status,
               fetched_at = Sys.time(), error = error)
  }

  resp <- tryCatch(httr::GET(url, httr::user_agent(ua), httr::timeout(timeout_sec)), error = identity)
  if (inherits(resp, "error")) return(safe_row(paste("request_error:", resp$message)))
  status <- httr::status_code(resp)
  if (status >= 400) return(safe_row(paste("http_status", status), status = status))

  html_txt <- tryCatch(httr::content(resp, as = "text", encoding = "UTF-8"), error = identity)
  if (inherits(html_txt, "error") || !nzchar(html_txt)) return(safe_row("empty_response", status = status))

  doc <- tryCatch(xml2::read_html(html_txt), error = identity)
  if (inherits(doc, "error")) return(safe_row("parse_error", status = status))

  title_node <- rvest::html_element(doc, "title")
  page_title <- if (inherits(title_node, "xml_missing")) NA_character_ else clean_txt(rvest::html_text2(title_node))

  content_node <- choose_content_node(doc)
  if (inherits(content_node, "xml_missing") || length(content_node) == 0) {
    return(safe_row("content_not_found", status = status, title = page_title))
  }

  fields <- extract_fields(content_node)

  cbind(
    data.table(url = url, page_title = page_title, status = status,
               fetched_at = Sys.time(), error = NA_character_),
    as.data.table(as.list(fields), keep.rownames = FALSE)
  )
}

# Scrape many URLs
scrape_many <- function(urls, sleep_bounds = c(0.2, 0.6)) {
  if (!length(urls)) return(data.table())
  pb <- txtProgressBar(min = 0, max = length(urls), style = 3)
  res <- vector("list", length(urls))
  for (i in seq_along(urls)) {
    Sys.sleep(runif(1, sleep_bounds[1], sleep_bounds[2]))  # polite delay
    res[[i]] <- tryCatch(scrape_one(urls[[i]]), error = function(e) {
      data.table(url = urls[[i]], page_title = NA_character_, status = NA_integer_,
                 fetched_at = Sys.time(), error = paste("unexpected_error:", e$message))
    })
    setTxtProgressBar(pb, i)
  }
  close(pb)
  data.table::rbindlist(res, fill = TRUE, use.names = TRUE)
}
```

``` r
# Optional diagnostics: peek at first-column labels inside common containers for one URL
u <- "https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=aalii"
doc <- xml2::read_html(u)
sels <- c("#content","div#content","#main","main","article",".content","#mw-content-text","body")
diag <- lapply(sels, function(s) {
  node <- rvest::html_element(doc, s)
  if (inherits(node, "xml_missing") || length(node) == 0) return(NULL)
  rows <- rvest::html_elements(node, "tr")
  if (!length(rows)) return(NULL)
  labs <- unlist(lapply(rows, function(tr) {
    cells <- rvest::html_elements(tr, "th, td")
    if (length(cells) >= 1) rvest::html_text2(cells[[1]]) else NA_character_
  }))
  data.table(selector = s, first_col_labels = unique(na.omit(stringr::str_squish(labs))))
})
Filter(Negate(is.null), diag)
```

``` r
# Assumes you've already run:
# - setup_deps (packages)
# - functions chunk (defines clean_txt, canon_label, extract_fields, scrape_one, scrape_many)

stopifnot(exists("final_dt"))
url_col   <- intersect(names(final_dt), c("url","URL","link","href"))[1]
depth_col <- intersect(names(final_dt), c("depth","Depth","level","crawl_depth"))[1]
if (is.na(url_col))   stop("final_dt must have a URL column.")
if (is.na(depth_col)) stop("final_dt must have a crawl depth column.")

depth2_urls <- unique(na.omit(final_dt[get(depth_col) == 2][[url_col]]))
message(sprintf("Scraping %d depth-2 URLs …", length(depth2_urls)))

# Execute scraping (polite delays handled in scrape_many/scrape_one)
depth2_wide <- scrape_many(depth2_urls)
#>   |                                                               |                                                       |   0%  |                                                               |                                                       |   1%  |                                                               |=                                                      |   1%  |                                                               |=                                                      |   2%  |                                                               |==                                                     |   3%  |                                                               |==                                                     |   4%  |                                                               |===                                                    |   5%  |                                                               |===                                                    |   6%  |                                                               |====                                                   |   7%  |                                                               |====                                                   |   8%  |                                                               |=====                                                  |   8%  |                                                               |=====                                                  |   9%  |                                                               |=====                                                  |  10%  |                                                               |======                                                 |  10%  |                                                               |======                                                 |  11%  |                                                               |======                                                 |  12%  |                                                               |=======                                                |  12%  |                                                               |=======                                                |  13%  |                                                               |========                                               |  14%  |                                                               |========                                               |  15%  |                                                               |=========                                              |  16%  |                                                               |=========                                              |  17%  |                                                               |==========                                             |  18%  |                                                               |==========                                             |  19%  |                                                               |===========                                            |  19%  |                                                               |===========                                            |  20%  |                                                               |===========                                            |  21%  |                                                               |============                                           |  21%  |                                                               |============                                           |  22%  |                                                               |=============                                          |  23%  |                                                               |=============                                          |  24%  |                                                               |==============                                         |  25%  |                                                               |==============                                         |  26%  |                                                               |===============                                        |  27%  |                                                               |===============                                        |  28%  |                                                               |================                                       |  28%  |                                                               |================                                       |  29%  |                                                               |================                                       |  30%  |                                                               |=================                                      |  30%  |                                                               |=================                                      |  31%  |                                                               |=================                                      |  32%  |                                                               |==================                                     |  32%  |                                                               |==================                                     |  33%  |                                                               |===================                                    |  34%  |                                                               |===================                                    |  35%  |                                                               |====================                                   |  36%  |                                                               |====================                                   |  37%  |                                                               |=====================                                  |  38%  |                                                               |=====================                                  |  39%  |                                                               |======================                                 |  39%  |                                                               |======================                                 |  40%  |                                                               |======================                                 |  41%  |                                                               |=======================                                |  41%  |                                                               |=======================                                |  42%  |                                                               |========================                               |  43%  |                                                               |========================                               |  44%  |                                                               |=========================                              |  45%  |                                                               |=========================                              |  46%  |                                                               |==========================                             |  47%  |                                                               |==========================                             |  48%  |                                                               |===========================                            |  48%  |                                                               |===========================                            |  49%  |                                                               |===========================                            |  50%  |                                                               |============================                           |  50%  |                                                               |============================                           |  51%  |                                                               |============================                           |  52%  |                                                               |=============================                          |  52%  |                                                               |=============================                          |  53%  |                                                               |==============================                         |  54%  |                                                               |==============================                         |  55%  |                                                               |===============================                        |  56%  |                                                               |===============================                        |  57%  |                                                               |================================                       |  58%  |                                                               |================================                       |  59%  |                                                               |=================================                      |  59%  |                                                               |=================================                      |  60%  |                                                               |=================================                      |  61%  |                                                               |==================================                     |  61%  |                                                               |==================================                     |  62%  |                                                               |===================================                    |  63%  |                                                               |===================================                    |  64%  |                                                               |====================================                   |  65%  |                                                               |====================================                   |  66%  |                                                               |=====================================                  |  67%  |                                                               |=====================================                  |  68%  |                                                               |======================================                 |  68%  |                                                               |======================================                 |  69%  |                                                               |======================================                 |  70%  |                                                               |=======================================                |  70%  |                                                               |=======================================                |  71%  |                                                               |=======================================                |  72%  |                                                               |========================================               |  72%  |                                                               |========================================               |  73%  |                                                               |=========================================              |  74%  |                                                               |=========================================              |  75%  |                                                               |==========================================             |  76%  |                                                               |==========================================             |  77%  |                                                               |===========================================            |  78%  |                                                               |===========================================            |  79%  |                                                               |============================================           |  79%  |                                                               |============================================           |  80%  |                                                               |============================================           |  81%  |                                                               |=============================================          |  81%  |                                                               |=============================================          |  82%  |                                                               |==============================================         |  83%  |                                                               |==============================================         |  84%  |                                                               |===============================================        |  85%  |                                                               |===============================================        |  86%  |                                                               |================================================       |  87%  |                                                               |================================================       |  88%  |                                                               |=================================================      |  88%  |                                                               |=================================================      |  89%  |                                                               |=================================================      |  90%  |                                                               |==================================================     |  90%  |                                                               |==================================================     |  91%  |                                                               |==================================================     |  92%  |                                                               |===================================================    |  92%  |                                                               |===================================================    |  93%  |                                                               |====================================================   |  94%  |                                                               |====================================================   |  95%  |                                                               |=====================================================  |  96%  |                                                               |=====================================================  |  97%  |                                                               |====================================================== |  98%  |                                                               |====================================================== |  99%  |                                                               |=======================================================|  99%  |                                                               |=======================================================| 100%

# Optional: write results
# data.table::fwrite(depth2_wide, "data/depth2_wide.csv")

# Quick summary of extracted fields
found_cols <- setdiff(names(depth2_wide), c("url","page_title","status","fetched_at","error"))
message(sprintf("Extracted %d distinct field labels.", length(found_cols)))
print(sort(found_cols))
#> character(0)

depth2_wide
#>                                                                              url
#>                                                                           <char>
#>   1:    https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=aalii
#>   2:     https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=ae_S
#>   3:     https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=ae_Z
#>   4:   https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=ahakea
#>   5:  https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=aheahea
#>  ---                                                                            
#> 141:     https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=ulei
#> 142:      https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=ulu
#> 143:    https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=uluhe
#> 144:    https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=wauke
#> 145: https://data.bishopmuseum.org/ethnobotanydb/ethnobotany.php?b=d&ID=wiliwili
#>                                page_title status
#>                                    <char>  <int>
#>   1: Bishop Museum - Ethnobotany Database    200
#>   2: Bishop Museum - Ethnobotany Database    200
#>   3: Bishop Museum - Ethnobotany Database    200
#>   4: Bishop Museum - Ethnobotany Database    200
#>   5: Bishop Museum - Ethnobotany Database    200
#>  ---                                            
#> 141: Bishop Museum - Ethnobotany Database    200
#> 142: Bishop Museum - Ethnobotany Database    200
#> 143: Bishop Museum - Ethnobotany Database    200
#> 144: Bishop Museum - Ethnobotany Database    200
#> 145: Bishop Museum - Ethnobotany Database    200
#>               fetched_at  error
#>                   <POSc> <char>
#>   1: 2025-08-18 01:07:25   <NA>
#>   2: 2025-08-18 01:07:25   <NA>
#>   3: 2025-08-18 01:07:25   <NA>
#>   4: 2025-08-18 01:07:26   <NA>
#>   5: 2025-08-18 01:07:26   <NA>
#>  ---                           
#> 141: 2025-08-18 01:08:33   <NA>
#> 142: 2025-08-18 01:08:34   <NA>
#> 143: 2025-08-18 01:08:34   <NA>
#> 144: 2025-08-18 01:08:35   <NA>
#> 145: 2025-08-18 01:08:35   <NA>
```
