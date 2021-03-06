Progress Report-JOE
================
Joe Patrick
10/11/2021

-   [Initial Set-Up, 10-11-2021](#initial-set-up-10-11-2021)
-   [Belated First Progress Report,
    11/1/21](#belated-first-progress-report-11121)
-   [11-20-2021 Second Project
    Report](#11-20-2021-second-project-report)

## Initial Set-Up, 10-11-2021

Created the Github repo and uploaded the progress report and the plan
docs. Set gitignore to R, but Git made me choose a license before
letting me finish creating the repo, so I set it as MIT license.

## Belated First Progress Report, 11/1/21

I have been able to import each wikipedia article as it’s own object to
process. I would probably like to put those articles together in a
larger combined corpus, but I’m not there yet. I’m processing texts from
Croatian wiki, in Latin script, and Serbian wiki, in Cyrillic script.
There’s evidence in the literature that these two variants are the most
differentiated. To do so, I’m looking at a collection of 16 features
based on previous work by Ljubesic, Milicevic-Petrovic, and Samardzic
(2018) to locate features on Twitter and their geotags because these
features are canonically used as markers of dialect between the
varieties of Serbo-Croatian. The paper suggests ways of collecting data
for some of the features, but I still need to figure out how to get the
other features. These are 16 two-categorical level variables.

The features (sr= Serbian, hr= Croatian; generally):  
1. ‘jat’ reflexes: systematic occurrence of historical /j/ in some
lexical items  
\* mleko (sr) vs. mlijeko (hr) ‘milk’  
\* Use pre-made word lists to compare and identify? Small corpus- by
hand?  
2. r vs. r-drop in some words  
\* takodjer (hr) vs. takodje (sr) ‘also’  
\* Use pre-made word lists to compare and identify? This list can be
smaller.  
3. k vs. h in certain word beginnings with Greek roots  
\* kemija (hr) vs. hemija (sr) ‘chemistry’  
\* Use pre-made word lists to compare and identify?  
4. h (hr) vs. no h (Sr- both forms)  
\* gluh vs. gluv ‘deaf’; hrvanje vs. rvanje ‘wrestling’  
\* not sure- word list? Might exclude  
5. use of sto (sr) vs. sta (hr) as question word ‘what’  
\* can use regexs to find these uses in Latin and Cyrillic  
\* \#kosovosr %&gt;% str\_detect(“sto”) %&gt;% sum()  
\* \#kosovosr %&gt;% str\_detect(“што”) %&gt;% sum()  
\* \#kosovosr %&gt;% str\_detect(" \[sta\|шта\|sto\|што\] ") %&gt;%
sum()  
6. use of dali(sr) vs. jeli (hr) for yes/no questions and
complementizers  
\* sometimes a space; also these particles have other meanings/uses  
\* paper cited uses regexs, but not sure I’ll find examples in formal
text  
\* ‘li and ‘li  
7. use of s (hr) vs sa (sr) as a preposition (often instrumental)  
\* paper cited uses a ’two-form manual lexicon file’  
8. use of mnogo (sr) vs puno (hr) as most common word for ‘a lot,
many’  
9. use of question word ko (sr) vs tko (hr) as word for ‘who’  
\* this is a challenging variable- some inflected forms look like
other  
common words.  
10. long (sr) vs. short (hr) forms of infinitive verbs  
\* provozati vs. provozat ‘to go for a ride’  
\* paper used lexicon files derived from hrLex and srLex  
11. use of da (sr) vs. inf (hr)  
\* da posluzi vs. posluziti ‘to serve’  
12. synthentic (sr) vs. nonsynthetic (hr) use of the future tense  
\* otvoricemo vs. otvorit cemo ‘we will open…’  
\* back to hrLex and srLex…  
13. long (hr) vs short (sr) forms of adjectives  
\* prosloga vs. proslog ‘last, past’  
14. ira (hr) vs isa/ova (sr) in adjectives  
\* organizirana vs. organizovan ‘organized’  
15. trebam.conjugated vs. treba da + verb.conj ‘to need something’  
\* this feature might be in more free variation, or less hr vs sr.  
\* ‘(m\|s\|mo\|te\|ju)(?! da)’, for present tense forms of the verb  
(without the adjacent da), and ‘da, for impersonal form of the verb
(sr)  
16. suffix form of ica (hr) vs. ka (sr) for feminine titles  
\* profesorica vs. profesorka ’female professor’  
\* extracted fem nouns using lexs and checked by hand

There is a lot here- the authors of the study I’m basing this on largely
used R for their processing. The authors found patterns where Croatia
aligned with Bosnia vs. Serbia and Montenegro in some features and
Croatia vs. everyone and Serbia vs. everyone in other features. Everyone
is: Croatia, Serbia, Montenegro, and Bosnia.

The patterns found on Twitter data are below:

A. HR vs. rest== ira:isaova ko:tko k:h rdrop  
B. HR, BA vs.ME, RS== da:inf mnogo:puno treba h:noh synth:nonsynth
s:sa  
C. RS vs. rest== e:je ica:ka  
D. no pattern== dali:jeli long:shortinf sto:sta adjg

So it might be the case that I focus on A, B, C and leave D alone here.

My corpus: articles from the Serbian and Croatian wikipedia- matched on
topic. Starting with potentially politically-divisive articles- small,
focused corpus for this project. E.g. Hr and Sr article topics on
Kosovo, WW2, Yugoslav wars.

Sharing plan: because this is wiki data and protected under a creative
commons license, I can share all of it. Especially if I’m building this
project on the back of Ljubesic, Milicevic-Petrovic, and Samardzic
(2018)

What do I need: First, to determine scope of variables (this is a DS
project but also a comps, but I don’t need all 16 variables to apply
method to Wiki data). Next, to figure out a way to find features0- regex
and manual search might be useful, but is there a better way?

I attached an rmd with my exploring of the sto/sta variable (\#5)

## 11-20-2021 Second Project Report

Figured out how to import the data I need in a processable format.
Cleaned the data by trimming front/back white space and making
everything lower case. Made a function to do the importing and cleaning,
using a URL as input. Started processing my data. I have about 5
features testable via functions already. I set the license to MIT in the
first progress report because it was suggested as a pretty generic, open
license and since I’m working with open-source data to begin with, I
should be as open as possible. It is all shareable widely and freely
because it’s Wikipedia data.

Two problems:

1.  I still have to run each feature-function on every URL
    independently, so that if I have 12 Wiki-texts, I have to run each
    function 12 times. This is what I was envisioning would be corrected
    by a corpus-type object that I could pass through a function once.

2.  I am trying to nest all my feature-functions into one master
    function that will do all the processing for me. I can’t make it
    work yet- is this genius or madness? \#\# Second Project Report,
    11-20-2021- NEW CONTINUING Figured out how to import the data I need
    in a processable format. Cleaned the data by trimming front/back
    white space and making everything lower case. Made a function to do
    the importing and cleaning, using a URL as input. Started processing
    my data. I have about 5 features testable via functions already. I
    set the license to MIT in the first progress report because it was
    suggested as a pretty generic, open license and since I’m working
    with open-source data to begin with, I should be as open as
    possible. It is all shareable widely and freely because it’s
    Wikipedia data.

Two problems:

1.  I still have to run each feature-function on every URL
    independently, so that if I have 12 Wiki-texts, I have to run each
    function 12 times. This is what I was envisioning would be corrected
    by a corpus-type object that I could pass through a function once.

2.  I am trying to nest all my feature-functions into one master
    function that will do all the processing for me. I can’t make it
    work yet- is this genius or madness?

In case anyone has any ideas, this is how I’m inputting and cleaning the
data:

``` r
 input_data <- function(x) {
   x <- read_html(x) %>% 
     html_elements("#collapsibleTable1 tr:nth-child(2) td , .tright+ ul li , .infobox small , #mw-content-text p") %>% 
     html_text() %>% 
     str_remove_all("\\[\\d+?\\]") %>%
     str_trim() %>% 
     tolower()
 }
```

This is how I’m trying to nest my functions (the other functions are
already made in my full script):

``` r
BCS_Dialect <- function(x) { 
  x <- input_data(x)
  x <- mnogopuno(x) %>%
  x <- isa_iraova(x) %>%
  x <- ko_tko(x) %>%
  x <- da_inf(x) %>%
  x <- sorsa(x)
}
```

And that is everything I have right now.
