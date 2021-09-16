# C6Samples
Manually annotated data sets from project C6 (SFB 1102)

## Data Sets

Corpus | Time period | #Tokens | Annotations
:------ | :-----------: | -------: | :------------
[DTAmedical](#dtamedical-and-dtatheological) | 17th-20th century | 1,083,720 | sentences (automatic), tokens (automatic), lemmas (automatic), STTS-POS (automatic/manually corrected), [antecedents](#antecedents), [citations](#citations), [moving elements](#moving-elements), orthographic correction (automatic), [topological fields](#topological-fields) (sentence brackets only)
[DTAtheological](#dtamedical-and-dtatheological) | 17th-20th century | 778,976 | sentences (automatic), tokens (automatic), lemmas (automatic), STTS-POS (automatic/manually corrected), [antecedents](#antecedents), [citations](#citations), [moving elements](#moving-elements), orthographic correction (automatic), [topological fields](#topological-fields) (sentence brackets only)

### DTAmedical and DTAtheological

The sample contains sentences from 11 medical texts and 13 theological texts from the DTA [(German Text Archive; BBAW, 2019)](http://www.deutschestextarchiv.de/).

Sentence boundaries, tokens, lemmas, orthographic normalization, and POS tags are taken from the automatic annotations of the DTA.
To date, POS tags are manually corrected for the following texts:

*Medical*
- abel_leibmedicus_1699
- braeuner_pest_1714
- purmann_feldscher_1680
- unzer_gedanken_1746

*Theological*
- bengel_abriss01_1751
- benner_meineid_1739
- dilger_arndes_1620_1
- hanssen_grundfragen_1731
- nividandts_schwerd_1708
- rotth_bedencken_1692
- spener_piadesideria_1676

In addition, the sentences are manually annotated with the following linguistic information:

1. [*Moving elements*](#moving-elements)

Label | Element | Annotation
:---: | :------ | :---------
`NP`  | noun phrase | Every extraposed `NP` + one comparable in-situ `NP` with the same length
`PP`  | prepositional phrase | Every extraposed `PP` + one comparable in-situ `PP` with the same pronoun and length
`AP`  | adjective phrase | Every extraposed `AP` + one comparable in-situ `AP` with the same length
`ADVP` | adverb phrase | Every extraposed `ADVP` + one comparable in-situ `ADVP` with the same length
`CMPP` | comparative element | All comparative elements with adjectival antecedent (in comparative or superlative)
`RELC` | relative clause | All attributive relative clauses with (pro)nominal antecedent
`ADVC` | adverbial clause | All causal clauses

2. [*Antecedents*](#antecedents)

Antecedents are annotated for all relative clauses and comparative elements. The other moving elements can also have antecedents (probably except for `ADVPs`). This is rarely the case, though.

3. [*Sentence brackets*](#topological-fields)

4. [*Citations*](#citations)


## Data Format

The data sets are provided in the [CoNLL-U Plus format](https://universaldependencies.org/ext-format.html). The first line of each file (starting with `# global.columns = `) specifies the columns that are included.

Columns are separated by tabs and sentences by empty lines. For each sentence, meta information can be given at the beginning of a sentence, e.g., the sentence ID and the concatenated tokens. Meta lines are preceded by the hash sign `#`.

Tokens are indexed starting with index 1. Empty annotations are indicated by an underscore `_`.

The following example shows the head of the file abel_leibmedicus_1699 from the DTAmedical sample.

> \# global.columns = ID FORM LEMMA UPOS XPOS FEATS HEAD DEPREL DEPS MISC Antec MovElem OrthCorr OrthCorrOp OrthCorrReason TOPF  
> \# sent_id = 1  
> \# sent_id(TSV) = 1  
> \# text = D. Henrici Caſparis Abelii , ...  
> 1	D.	D.	_	NE	_	_	_	_	_	B-Antec-1-Head	_	_	_	_	_  
> 2	Henrici	Henrici	_	NE	_	_	_	_	_	I-Antec	_	_	_	_	_  
> 3	Caſparis	Casparis	_	NE	_	_	_	_	_	I-Antec	_	Casparis	replace	*	_  
> 4	Abelii	Abelii	_	NE	_	_	_	_	_	I-Antec	_	_	_	_	_  
> 5	,	,	_	$,	_	_	_	_	_	I-Antec	_	_	_	_	_  

## Span Annotations

Span annotations are encoded with a modified version of BIO-tags. The first letter of the tag specifies the position inside/outside of the span:

Letter | Meaning
 :---: | :-------------------------
 B | beginning of the span
 I | inside of the span
 O | outside of any span

`B` and `I` are supplemented with the span label, separated by a dash: `B-NP` or `I-NP`. Tokens outside of any span are only labeled as `O`. For sparse annotations that only concern few tokens (e.g., citations) the `O` can also be replaced by an underscore `_` to improve the readability of the file for a human user.

A span can also include one or more other spans. In this case, annotations are ordered hierarchically from the longest span to the left to the shortest, most deeply embedded span to the right. Multiple spans are seperated by a pipe `|`, e.g., `I-NF|B-LK`.

For more complex annotations, the BIO-tags can also be extended with more information, e.g., `B-RELC-extrap-1`. For details on the different annotations, cf. the sections below.

### Antecedents

### Chunks

Chunks are non-recursive, non-overlapping constituents from a sentence's parse tree. The following chunk labels are used:

Label | Chunk 
:---: | :----
NC | Noun chunk
PC | Prepositional chunk
AC | Adjective chunk
ADVC | Adverb chunk
sNC | Stranded noun chunk
sPC | Stranded prepositional chunk

Stranded chunks occur when the beginning of a chunk is separated from the rest of the chunk by pre-modifying elements. For more information, cf. [Ortmann (2021)](https://aclanthology.org/2021.nodalida-main.19/).

### Citations

Citations, e.g., from the Bible, are marked with `B-Citation` and `I-Citation`. Tokens that are not part of a citation are labeled with `_`.

### Moving Elements

### Phrases

In the context of this project, phrases are understood as non-overlapping constituents from a sentence's parse tree. Only the highest non-terminal nodes of the following types are included:

Label | Phrase 
:---: | :----
NP | Noun phrase
PP | Prepositional phrase
AP | Adjective phrase
ADVP | Adverb phrase

Phrases are expected to not cross topological field boundaries. This means that they can be located within a field or contain one or more fields, but the may not be part of two neighbouring fields and the fields they contain may not stretch across the boundaries of the phrase.

### Topological Fields

The topological field annotation is included in the `TOPF` column. Fields can - and often are - nested, i.e., one filed can encompass one or more (possibly complex) other fields. The following field labels are used:

Label | Field 
:---: | :----
KOORD | Koordinationsfeld (*coordination field*)
LV | Linksversetzung (*left dislocation*)
VF | Vorfeld (*pre-field*)
LK | Linke Satzklammer (*left sentence bracket*)
MF | Mittelfeld (*middle field*)
RK | Rechte Satzklammer (*right sentence bracket*)
NF | Nachfeld (*post-field*)

For data sets that only contain sentence bracket annotations, the remaining tokens are labeled with `_` instead of `O`.

## References

BBAW. 2019. Deutsches Textarchiv. Grundlage für ein Referenzkorpus der neuhochdeutschen Sprache. Berlin-Brandenburgische Akademie der Wissenschaften; http://www.deutschestextarchiv.de/.

Katrin Ortmann. 2021. Chunking Historical German. In: Proceedings of the 23rd Nordic Conference on Computational Linguistics (NoDaLiDa), Reykjavik, Iceland (online), pp. 190-199. [PDF](https://aclanthology.org/2021.nodalida-main.19/) [Github](https://github.com/rubcompling/nodalida2021)

Anne Schiller, Simone Teufel, Christine Stöckert, and Christine Thielen. 1999. *Guidelines für das Tagging deutscher Textcorpora mit STTS (Kleines und großes Tagset)*. Retrieved from http://www.sfs.uni-tuebingen.de/resources/stts-1999.pdf.
