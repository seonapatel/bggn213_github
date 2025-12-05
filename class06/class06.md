# Class 6: R Functions
Seona Patel (PID: A69035519)

- [Our first (silly) function](#our-first-silly-function)
- [A second function](#a-second-function)
- [A protein generating function](#a-protein-generating-function)

All functions in R have at least 3 things:

- A **name**, we pick this and use it to call our function
- Input **arguments** (there can be multiple)
- The **body** lines of R code that do the work

## Our first (silly) function

Write a function to add some numbers

``` r
add <- function(x,y=1) {x+y}
```

Now we can call this function:

``` r
#add(10,10,100)
```

``` r
add(10,100)
```

    [1] 110

## A second function

Write a function to generate random nucleotide sequences of a user
specified length: The `sample()` function can be useful here.

``` r
sample(c('A','C','T','G'), size=30, replace=TRUE)
```

     [1] "A" "A" "C" "A" "G" "G" "A" "C" "A" "T" "G" "C" "T" "A" "T" "A" "C" "T" "T"
    [20] "A" "C" "A" "G" "T" "A" "T" "G" "C" "A" "G"

I want a 1 element long character vector that looks like “GACTA”

``` r
v <- sample(c('A','C','T','G'), size=30, replace=TRUE)
paste(v,collapse='')
```

    [1] "CAACGCAGGCATAAGCTCAACTCCGGCCCT"

``` r
generate_dna <- function(size=50) {
v <- sample(c('A','C','T','G'), size=size, replace=TRUE)
paste(v,collapse='')}
```

Test it:

``` r
generate_dna(60)
```

    [1] "GTTGTGCATTTATAGCTTTATGCTAGGTGAAGTGGTCTCCTACAAAAGTGAAGCATTACG"

``` r
fasta <- FALSE
if(fasta) {
  cat("HELLO You!")
} else {
    cat("No you dont")
  }
```

    No you dont

Add the ability to return a multi-elemnt vector or a single element
fasta like vector.

``` r
generate_fasta <- function(size=50, fasta=TRUE) {
v <- sample(c('A','C','T','G'), size=size, replace=TRUE)
s <- paste(v, collapse='')
if(fasta) {
return(s)
}
else{
return(v)}
}
```

``` r
generate_fasta(50, TRUE)
```

    [1] "CGATGTACTGTACCCGGAACGCATATTATAGACAACAGATGGAAAACTAT"

``` r
generate_fasta(50, FALSE)
```

     [1] "A" "C" "G" "C" "G" "T" "C" "A" "G" "G" "T" "T" "G" "C" "A" "C" "C" "G" "G"
    [20] "T" "T" "T" "T" "A" "A" "T" "T" "G" "A" "T" "C" "T" "G" "G" "C" "C" "T" "A"
    [39] "A" "A" "A" "C" "G" "G" "T" "A" "C" "T" "T" "G"

## A protein generating function

``` r
generate_protein <- function(size=50, fasta=TRUE) {
  aa <- c('A','R','N','D','C','Q','E','G','H','I','L','K','M','F','P','S','T','W','Y','V')
  v <- sample(aa, size=size, replace=TRUE)
  s <- paste(v, collapse='')
  if(fasta) {
    return(s)
  } else {
    return(v)
  }
}
```

``` r
generate_protein(6)
```

    [1] "FCIQTH"

Use new `generate_protein()` function to generate random protein
sequences of lengths between 6 and 12.

One way to do this is brute force.

A second way is usign a `for()` loop:

``` r
lengths <- 6:12
lengths
```

    [1]  6  7  8  9 10 11 12

``` r
for(i in lengths) {
  cat(">", i, "\n", sep="")
  aa <- generate_protein(i)
  cat(aa)
  cat("\n")
}
```

    >6
    VTMECN
    >7
    KIGEWCH
    >8
    VVSVYSWR
    >9
    SGLPHTYFI
    >10
    MHNCLCWCRF
    >11
    PPRRAQSVDGI
    >12
    RVSPQLHYSHNV

``` r
paste(c('barry', 'monika'), "R", sep=" loves ")
```

    [1] "barry loves R"  "monika loves R"

A third, and better, way to solve this is to use the `apply()` family of
functions, specifically the`sapply()` function in this case.

``` r
sapply(6:12, generate_protein)
```

    [1] "AARCTE"       "REFWTFR"      "KAYNHVID"     "ALDTCFQTI"    "SRERQLNDRW"  
    [6] "FYKLCCCCYNQ"  "KNWNFVYCYDGK"
