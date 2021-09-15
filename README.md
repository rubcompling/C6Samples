# C6Samples
Manually annotated data sets from project C6 (SFB 1102)

## Data Sets

Corpus | Time period | #Tokens | Annotations
:------ | :-----------: | -------: | :------------
[DTAmedical](#dtamedical) | 17th-20th century | 1,083,720 | sentences (automatic), tokens (automatic), lemmas (automatic), STTS-POS (automatic/manually corrected), [antecedents](#antecedents), [citations](#citations), [moving elements](#moving-elements), orthographic correction (automatic), [topological fields](#topological-fields) (sentence brackets only)
[DTAtheological](#dtatheological) | 17th-20th century | 778,976 | sentences (automatic), tokens (automatic), lemmas (automatic), STTS-POS (automatic/manually corrected), [antecedents](#antecedents), [citations](#citations), [moving elements](#moving-elements), orthographic correction (automatic), [topological fields](#topological-fields) (sentence brackets only)

### DTAmedical

The sample contains sentences from 11 medical texts from the DTA [(German Text Archive; BBAW, 2019)](http://www.deutschestextarchiv.de/).

Sentence boundaries, tokens, lemmas, orthographic normalization, and POS tags are taken from the automatic annotations of the DTA.
To date, POS tags are manually corrected for the following texts:
- abel_leibmedicus_1699
- braeuner_pest_1714
- purmann_feldscher_1680
- unzer_gedanken_1746

### DTAtheological

The sample contains sentences from 13 theological texts from the DTA [(German Text Archive; BBAW, 2019)](http://www.deutschestextarchiv.de/).

Sentence boundaries, tokens, lemmas, orthographic normalization, and POS tags are taken from the automatic annotations of the DTA.
To date, POS tags are manually corrected for the following texts:
- bengel_abriss01_1751
- benner_meineid_1739
- dilger_arndes_1620_1
- hanssen_grundfragen_1731
- nividandts_schwerd_1708
- rotth_bedencken_1692
- spener_piadesideria_1676

## Data Format

The data sets are provided in the [CoNLL-U Plus format](https://universaldependencies.org/ext-format.html). The first line of each file (starting with `# global.columns = `) specifies the columns that are included.

### Annotation Format

Span annotations are encoded with a modified version of BIO-tags. The first letter of the tag specifies the position inside/outside of the span:

Letter | Meaning
 :---: | :-------------------------
 B | beginning of the span
 I | inside of the span
 O | outside of any span

`B` and `I` are supplemented with the span label, separated by a dash: `B-NP` or `I-NP`. Tokens outside of any span are only labeled as `O`. For sparse annotations that only concern few tokens (e.g., citations) the `O` can also be replaced by an underscore `_` to improve readability of the files for humans.

A span can also include one or more other spans. In this case, annotations are ordered hierarchically from the longest span to the left to the shortest, most deeply embedded span to the right. Multiple spans are seperated by a pipe `|`, e.g., `I-NF|B-LK`.

For more complex annotations, the BIO-tags can also be extended with more information, e.g., `B-RELC-extrap-1`. For details on the different annotations, cf. the sections below.

#### Antecedents

#### Chunks

#### Citations

Citations, e.g., from the Bible, are marked with `B-Citation` and `I-Citation`. Tokens that are not part of a citation are labeled with `_`.

#### Moving Elements

#### Phrases

#### Topological Fields

The following field labels are used:

Label | Field 
:---: | :----
KOORD | Koordinationsfeld (*coordination field*)
LV | Linksversetzung (*left dislocation*)
VF | Vorfeld (*pre-field*)
LK | Linke Satzklammer (*left sentence bracket*)
MF | Mittelfeld (*middle field*)
RK | Rechte Satzklammer (*right sentence bracket*)
NF | Nachfeld (*post-field*)

For data sets that only contain sentence brackets, the remaining tokens are labeled with `_` instead of `O`.

## References

BBAW. 2019. Deutsches Textarchiv. Grundlage für ein Referenzkorpus der neuhochdeutschen Sprache. Berlin-Brandenburgische Akademie der Wissenschaften; http://www.deutschestextarchiv.de/.

Anne Schiller, Simone Teufel, Christine Stöckert, and Christine Thielen. 1999. *Guidelines für das Tagging deutscher Textcorpora mit STTS (Kleines und großes Tagset)*. Retrieved from http://www.sfs.uni-tuebingen.de/resources/stts-1999.pdf.
