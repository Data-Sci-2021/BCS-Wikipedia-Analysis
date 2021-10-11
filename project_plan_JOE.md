Linguistic Differences among BCS Wikis
================
Joe Patrick
10/7/21

-   [Background](#background)
    -   [Questions](#questions)
    -   [Goal](#goal)
-   [Data](#data)
-   [Analysis](#analysis)
-   [Issues](#issues)

# Background

-   Bosnian, Croatian, and Serbian languages used to be considered the
    same language and called ‘Serbo-Croatian.’ They are largely mutually
    intelligible in many cases– at least regarding the written standard–
    and the name differences reflects differences in
    political/national/ethnic identity. Oftentimes the group of
    languages is now referred to as **BCS**

-   Wikipedia offers user-editable Wikis in many (approved) languages in
    which users can write, edit, and disseminate content. There are four
    separate Wikis relevant to the languages of interest: **Bosnian**,
    **Croatian**, **Serbian**, and a catch-all, **Serbo-Croatian**.
    There is a small internet movement to make a Montenegrin wiki, but
    it has not been approved yet.

-   Because wiki content is user-generated, text material differs across
    wikis, such that content has been thought to reflect nationalistic
    tendencies (see, for example, popular news media on historical
    revisionism on the Croatian Wiki).

    -   9/27/2018: Croatian-language Wikipedia: when the extreme right
        rewrites history-
        <https://www.balcanicaucaso.org/eng/Areas/Croatia/Croatian-language-Wikipedia-when-the-extreme-right-rewrites-history-190081>
    -   8/18/2021: Non-English Wikipedia has a misinformation problem-
        <https://www.fastcompany.com/90666412/non-english-wikipedia-misinformation>

## Questions

-   I am interested in determining if there are systematic linguistic
    differences between wikis that reflect common dialectological
    borders. If so, is presence/absence of features related to topic?  
-   I will focus on comparing the Croatian and Serbian Wikis. I may use
    the WikiDumps files, but they may be too large. If so, I will look
    at a handmade corpus made of articles on topics of WW2, Kosovo, and
    the Yugoslav Wars of the 1990s because they are likely to provoke
    disagreement and perhaps stoke more regionalisms and
    linguistically-discernable bias. I will ask the following questions:
    1.  What are the grammatical and circumstantial contexts of use when
        ethnonyms are referenced (e.g., the Serbian wiki referencing
        Croatians and vice versa)
    2.  How are linguistic/‘dialectal’ differences reflected on
        Wikipedia?
    3.  If I keeep this project tied to bias,what is linguistic bias?
        Working definition:
        -   Systematic asymmetry in word choice (?) that reflects the
            social category cognitions that are applied to the described
            group or individuals (Beukeboom & Burgers, 2017, 3)
        -   word/grammatical patterns?
        -   biases in labeling, what we communicate about, and how we
            formulate info about categorized individuals
    4.  Will this just be a modern dialectology of Wikipedia and reserve
        the bias component for later?

## Goal

This project will hopefully serve as my second comprehensives project
(which I need to find advisors for and start/finish soon), so please
offer any feedback/criticism/cynical judgments you so desire!

# Data

The data will be text data that I need to figure out how to extract from
Wikipedia. I will choose a small set of seed articles and I think I can
set web-crawlers to dig for text from one or two links deep. Then I will
turn those data into two corpora (one for Croatian and one for Serbian)

I will need to be able to split the corpora into concordances for
ethnonym contexts. Because I am intentionally dealing with a written,
more-formal genre, I’m not too concerned about removing punctuation- I
think it will be helpful. But I’ll need to split lines, make sure the
input looks appropriate, deal with headers, and work with two scripts
(Serbian wiki uses Cyrillic) and special graphemes with diacritics.

I have used packages like wikipediaR and Rvest to scrape some data, but
it’s not perfect yet. I need to figure out how to access the bodies of
text in the Wikis:

-   <https://github.com/michael-hainke/Wikipedia_API>  
-   <http://www.hainke.ca/index.php/2018/12/14/retrieving-wikipedia-data-for-natural-language-processing/>

Example: I tried to import text from
<https://hr.wikipedia.org/wiki/Kosovo>

Some of the data comes back in different order–e.g., data from the
bottom of the rightmost column of the article is presented first.

``` r
KosovoWiki <- readLines("~/Desktop/KosovoWikidata.rmd")
head(KosovoWiki, n=12)
```

    ##  [1] "---"                                                                                                                                                   
    ##  [2] "title: \"KosovoWikiData\""                                                                                                                             
    ##  [3] "author: \"Joe Patrick\""                                                                                                                               
    ##  [4] "date: \"10/3/2021\""                                                                                                                                   
    ##  [5] "output: html_document"                                                                                                                                 
    ##  [6] "---"                                                                                                                                                   
    ##  [7] "3  do 1"                                                                                                                                               
    ##  [8] "  siječnja 2015"                                                                                                                                       
    ##  [9] "  na kosovu je korišten pozivni broj za srbiju  381 za fiksne linije"                                                                                  
    ## [10] "  operateri mobilne telefonije na kosovu služili su se predbrojem  377  monako  ili  386  slovenija "                                                  
    ## [11] "  kosovo  albanski  kosova  kosovë  republika e kosovës  srpski  република косово  turski  kosova  je djelomično priznata država u jugoistočnoj europi"
    ## [12] "  u veljači 2008"

# Analysis

Domains of potentially controversial topics and articles to use as seed
topics:

1.  **WW2**- General: ustashe, chetnik, ускоке, drugi svetskog rat,
    kraljevine yugoslavije, fascism, concentration camps (Jasenovac),
    Garavice, Kruscica, kosta pecanic, ante pavelic

2.  **Kosovo**- eulex, albanians in serbia, Kosovars, pristina, vjosa
    osmani, nato, Kosovo liberation army, resolution 1244, Illyria,
    Metohija/kosmet/kim/Autonomous Province of Kosovo and Metohija,
    Ibrahim Rugova

3.  **Yugoslav Wars 1990s**- War criminals: Slobodan Praljak, Ratko
    Mladic, Slobodan Milosevic, Radovan Karadzic; Bosniaks, Srebrenica
    genocide, nationalism, republika Srpska, Tribunal, Dayton Agreement

4.  **Something neutral**- squirrels, fiji islands, galactic disks

For **RQ1**, I think I can make concordances once the corpora are made,
which would help with determining contexts of use for ethnonyms (Serb,
Croat, Hrvat, Albanian, Kosovar, Turk, bosniak, bosnian and all in
Cyrillic).  
\* How often are ‘self’ and ‘others’ referenced and in which context? \*
Morphosyntax- Since all nouns/adjectives are marked for case and
gender/number agreement.

For **RQ2**, I am coming up with a list of measurably important
dialectal features that might be more likely to show up in a ‘heavily
Croatian or Serbian’ text. A 2018 paper looks at Twitter distribution of
BC(M)S linguistic features and compares it with geotags, which seems
like a good metric to compare my features of interest:

-   Ljubešić, N., Miličević Petrović, M., & Samardžić, T. (2018).
    Borders and boundaries in Bosnian, Croatian, Montenegrin and
    Serbian: Twitter data to the rescue. Journal of Linguistic
    Geography, 6(2), 100–124. <https://doi.org/10.1017/jlg.2018.9>  
-   Most meaningful linguistic features generally:
    -   **HR vs. Rest**: ira:isa:ova, ko:tko, k:h, rdrop
    -   **HR,BA vs. ME, RS**: da:inf, mnogo:puno, treba, h:no h,
        synth:nonsynth, s:sa
    -   **RS vs. Rest**: e:je, ica:ka
-   Four most frequent variables with 81% variable occurrences
    -   **RS vs. Rest**: e:je
        -   devojka vs. djevojka
    -   **HR, BA vs ME, RS**: da:inf, s:sa
        -   posluziti vs. da posluzi (to serve)
        -   s nobelovcima vs. sa nekim
    -   **RS vs. Rest**: long:shortinf
        -   variti vs. provozat (take, go for a ride)

# Issues

-   Making the corpus itself
    -   scraping the text off the wiki pages
        -   what to include or not include?
        -   structure of each article worth saving? e.g. order of
            sections/columns
    -   Using WikiDumps? Or is that too ‘big data’?
    -   Well-balanced and representative corpus?
-   Intellectually sound?
    -   Dialect features to check for presence of regionalism or writer
        style in article
    -   Use of ethnonyms meaningful in any way? Quantity? Grammatical?
        Word form inflections?
