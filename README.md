# C6Samples
Manually annotated data sets from project C6 (SFB 1102)

## Data Sets

Corpus | Time period | #Tokens | Annotations
:------ | :-----------: | -------: | :------------
DTAmedical | 17th-20th century | 1,083,720 | Sentences (automatic), tokens (automatic), lemmas (automatic), STTS-POS (automatic/manually corrected), antecedents, citations, moving elements, orthographic correction (automatic), topological fields (sentence brackets only)
DTAtheological | 17th-20th century | 778,976 | Sentences (automatic), tokens (automatic), lemmas (automatic), STTS-POS (automatic/manually corrected), antecedents, citations, moving elements, orthographic correction (automatic), topological fields (sentence brackets only)


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

For more complex annotations, the BIO-tags can also be extended with more information. For details on the different annotations, cf. the sections below.

#### Antecedents

#### Chunks

#### Citations

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
