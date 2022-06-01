# C6Samples
Manually annotated data sets from project C6 (SFB 1102)

## Content

1. [Data sets](#data-sets)  
   1.1 [DTAmedical and DTAtheological](#dtamedical-and-dtatheological)  
2. [Data format](#data-format)  
3. [Span annotations](#span-annotations)  
   3.1 [Antecedents](#antecedents)  
   3.2 [Chunks](#chunks)  
   3.3 [Citations](#citations)  
   3.4 [Moving elements](#moving-elements)  
   3.5 [Phrases](#phrases)  
   3.6 [Topological fields](#topological-fields) 
4. [License](#license) 
5. [References](#references)  

- - - - - - - - - - - - - - - - 

## Data Sets

Corpus | Time period | #Tokens | Annotations  | License 
:------ | :-----------: | -------: | :------------ | :------
[DTAmedical](#dtamedical-and-dtatheological) | 17th-20th century | 1,083,720 | sentences (automatic), tokens (automatic), lemmas (automatic), STTS-POS (automatic/manually corrected), [antecedents](#antecedents), [citations](#citations), [moving elements](#moving-elements), orthographic correction (automatic), [topological fields](#topological-fields) (sentence brackets only) | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de)
[DTAtheological](#dtamedical-and-dtatheological) | 17th-20th century | 778,976 | sentences (automatic), tokens (automatic), lemmas (automatic), STTS-POS (automatic/manually corrected), [antecedents](#antecedents), [citations](#citations), [moving elements](#moving-elements), orthographic correction (automatic), [topological fields](#topological-fields) (sentence brackets only) | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de)

- - - - - - - - - - - - - - - - 

### DTAmedical and DTAtheological

The sample contains sentences from 11 medical texts and 13 theological texts from the [DTA](http://www.deutschestextarchiv.de/ "Deutsches Textarchiv (German Text Archive)").

Sentence boundaries, tokens, lemmas, orthographic normalization, and POS tags are taken from the automatic annotations of the [DTA](http://www.deutschestextarchiv.de/ "Deutsches Textarchiv (German Text Archive)").
To date, POS tags are manually corrected for the following texts:

*Medical*
- abel_leibmedicus_1699
- blumenbach_anatomie_1824
- braeuner_pest_1714
- carus_gynaekologie02_1820_1
- gall_untersuchungen_1791_1
- ludwig_physiologie02_1856
- purmann_feldscher_1680
- reil_curmethode_1803
- unzer_gedanken_1746

*Theological*
- bengel_abriss01_1751
- benner_meineid_1739
- dilger_arndes_1620_1
- hanssen_grundfragen_1731
- loehe_evangelium_1847
- nividandts_schwerd_1708
- pahl_simpertus_1799
- rotth_bedencken_1692
- spener_piadesideria_1676
- strauss_jesus01_1835_1

In addition, the sentences are manually annotated with the following linguistic information:

1. [*Moving elements*](#moving-elements)

Label | Element | Annotation
:---: | :------ | :---------
NP  | noun phrase | Every extraposed `NP` + one comparable in-situ `NP` with the same length
PP  | prepositional phrase | Every extraposed `PP` + one comparable in-situ `PP` with the same length and preposition
AP  | adjective phrase | Every extraposed `AP` + one comparable in-situ `AP` with the same length
ADVP | adverb phrase | Every extraposed `ADVP` + one comparable in-situ `ADVP` with the same length
CMPP | comparative element | All comparative elements with adjectival antecedent (in comparative or superlative)
RELC | relative clause | All attributive relative clauses with (pro)nominal antecedent
ADVC | adverbial clause | All causal clauses

2. [*Antecedents*](#antecedents)

Antecedents are annotated for all relative clauses and comparative elements. The other moving elements can also have antecedents (probably except for `ADVPs`). This is rarely the case, though.

3. [*Sentence brackets*](#topological-fields)

4. [*Citations*](#citations)

- - - - - - - - - - - - - - - - 

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

- - - - - - - - - - - - - - - - 

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

1. [Antecedents](#antecedents)
2. [Chunks](#chunks)
3. [Citations](#citations)
4. [Moving elements](#moving-elements)
5. [Phrases](#phrases)
6. [Topological fields](#topological-fields)

- - - - - - - - - - - - - - - - 

### Antecedents

Antecedents are annotated in the `Antec` column. Antecedents can be nested, i.e., contain other antecedents. They usually have one (or possibly more) head token(s) and they are always linked to a [moving element](#moving-elements) via an ID. The label thus consists of up to 4 parts, separated by dashes. Empty parts are ommited.

BIO letter | Antecedent | ID | Head |
:--------: | :---------- | :------ | :----- |
 B         |  Antec | 1, 2, ... | Head 
 I         |  Antec | -- | Head |
 
The beginning of an antecedent could thus be: `B-Antec-1` or `B-Antec-2-Head`  
A token inside of an antecedent could be annotated with: `I-Antec` or `I-Antec-Head`.

Additional remarks:
- `Head` is only annotated for the head token(s) of the antecedent.
- `IDs` are unique within a given sentence, starting at index 1. They always refer unambiguously to a [moving element](#moving-elements) in the same sentence.
- If the same token span serves as antecedent for multiple moving elements, this is annotated as if there were two distinct antecedents, e.g. `B-Antec-1|B-Antec-2`.
- Tokens that are not part of an antecedent are labeled with `_`.

- - - - - - - - - - - - - - - - 

### Chunks

Chunks are non-recursive, non-overlapping constituents from a sentence's parse tree. Chunk annotations are included in the `CHUNK` column. The following chunk labels are used:

Label | Chunk 
:---: | :----
NC | Noun chunk
PC | Prepositional chunk
AC | Adjective chunk
ADVC | Adverb chunk
sNC | Stranded noun chunk
sPC | Stranded prepositional chunk

Stranded chunks occur when the beginning of a chunk is separated from the rest of the chunk by pre-modifying elements. For more information, cf. [Ortmann (2021)](https://aclanthology.org/2021.nodalida-main.19/).

- - - - - - - - - - - - - - - - 

### Citations

Citations, e.g., from the Bible, are marked with `B-Citation` and `I-Citation` in the `Cite` column. Tokens that are not part of a citation are labeled with `_`.

- - - - - - - - - - - - - - - - 

### Moving Elements

Moving elements are phrases/clauses that are or can be extraposed, i.e., moved to the post-field of the sentence. They are annotated in the `MovElem` column. The following types are considered in this project:

Label | Element | 
:---: | :------ |
NP  | noun phrase |
PP  | prepositional phrase | 
AP  | adjective phrase | 
ADVP | adverb phrase | 
CMPP | comparative element (with adjectival antecedent in comparative or superlative) |
RELC | relative clause | 
ADVC | adverbial (causal) clause |

Moving elements can contain other moving elements, e.g., a relative clause with embedded noun phrases.

The label of a moving elements can consist of up to 5 parts, separated by dashes. Empty parts are ommited.

1. The first part specifies, whether the token is at the beginning `B` or inside `I` of the moving element.
2. The second part gives the type of moving element, e.g., `NP` or `RELC`.
3. The third part is only present for the beginning of moving elements:
    * For `ADVCs`, the third part specifies the position of the verb as verb-second `V2` or verb-last `VL` order.
    * For other moving elements, the third part specifies the position `extrap`, `insitu`, or `ambig`.
4. The fourth part marks the `Head` token.
5. The fifth part specifies the ID, if the element has an [antecedent](#antecedents). It is only annotated for the first token of a moving element.

BIO letter | Element type | Position | Head | ID |
:--------: | :---------- | :------ | :----- | :--- |
 B         |  NP, PP, AP, ADVP, CMPP, RELC | extrap, insitu, ambig | -- | 1, 2, ...
 B         |  ADVC        | V2, VL   | Head | 1, 2, ...
 I         |  NP, PP, AP, ADVP, CMPP, RELC | -- | -- | --
 I         |  ADVC        |   --     | Head | --

Exemplary labels for the beginning of a moving element could be: `B-NP-insitu`, `B-RELC-ambig-1`, `B-ADVC-VL`, `B-ADVC-V2-Head-3`  
Labels inside of moving elements could be: `I-AP`, `I-ADVC`, `I-ADVC-Head`

Additional remarks:
- `Head` is only annotated for the head token of `ADVCs`, usually the finite verb.
- `IDs` are unique within a given sentence, starting at index 1. Only elements with an [antecedent](#antecedents) get an `ID`.
- Tokens outside of moving elements are labeled with `_`.

- - - - - - - - - - - - - - - - 

### Phrases

In the context of this project, phrases are understood as non-overlapping constituents from a sentence's parse tree. They are annotated in the `PHRASE` column. Only the highest non-terminal nodes of the following types are included:

Label | Phrase 
:---: | :----
NP | Noun phrase
PP | Prepositional phrase
AP | Adjective phrase
ADVP | Adverb phrase

Phrases are expected to not cross topological field boundaries. This means that they can be located within a field or contain one or more fields, but the may not be part of two neighbouring fields and the fields they contain may not stretch across the boundaries of the phrase. For more information, cf. [Ortmann (2021b)](https://konvens2021.phil.hhu.de/wp-content/uploads/2021/09/2021.KONVENS-1.11.pdf).

- - - - - - - - - - - - - - - - 

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

The annotations are derived from the annotation scheme of the TüBa-D/Z corpus (Telljohann et al., 2017). For more information, cf. [Ortmann (2020)](https://aclanthology.org/2020.latechclfl-1.2.pdf)

For data sets that only contain sentence bracket annotations, the remaining tokens are labeled with `_` instead of `O`.

- - - - - - - - - - - - - - - - 

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

- - - - - - - - - - - - - - - - 

## References
BBAW. 2019. Deutsches Textarchiv. Grundlage für ein Referenzkorpus der neuhochdeutschen Sprache. Berlin-Brandenburgische Akademie der Wissenschaften; http://www.deutschestextarchiv.de/.

Katrin Ortmann. 2020. Automatic Topological Field Identification in (Historical) German Texts. In *Proceedings of the The 4th Joint SIGHUM Workshop on Computational Linguistics for Cultural Heritage, Social Sciences, Humanities and Literature (LaTeCH-CLfL)*, Barcelona, Spain (online), pp. 10-18. [[PDF]](https://aclanthology.org/2020.latechclfl-1.2.pdf) [[Github]](https://github.com/rubcompling/latech2020)

Katrin Ortmann. 2021. Chunking Historical German. In *Proceedings of the 23rd Nordic Conference on Computational Linguistics (NoDaLiDa)*, Reykjavik, Iceland (online), pp. 190-199. [[PDF]](https://aclanthology.org/2021.nodalida-main.19/) [[Github]](https://github.com/rubcompling/nodalida2021)

Katrin Ortmann. 2021b. Automatic Phrase Recognition in Historical German. In *Proceedings of the Conference on Natural Language Processing (KONVENS)*, Düsseldorf, Germany. [[PDF]](https://konvens2021.phil.hhu.de/wp-content/uploads/2021/09/2021.KONVENS-1.11.pdf) [[Github]](https://github.com/rubcompling/konvens2021)

Anne Schiller, Simone Teufel, Christine Stöckert, and Christine Thielen. 1999. *Guidelines für das Tagging deutscher Textcorpora mit STTS (Kleines und großes Tagset)*. Retrieved from http://www.sfs.uni-tuebingen.de/resources/stts-1999.pdf.

Heike Telljohann, Erhard W. Hinrichs, Sandra Kübler, Heike Zinsmeister, and Kathrin Beck. 2017. *Stylebook for the Tübingen Treebank of Written German (TüBa-D/Z)*. Seminar fur Sprachwissenschaft, Universität Tübingen, Germany.
