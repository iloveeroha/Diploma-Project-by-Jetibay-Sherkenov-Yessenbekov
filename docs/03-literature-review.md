# Literature review

## 1. Search protocol

| Item | Value |
|---|---|
| Databases | Crossref, publisher pages, ACL Anthology, AITU Scientific Journal, GitHub |
| Keywords | meeting summarisation, abstractive summarization, multilingual ASR, Kazakh speech recognition, action-item extraction, diarisation |
| Years | 2021–2026, with software repositories and foundational works allowed |
| Inclusion criteria | Traceable publication or maintained open-source repository; relevance to meeting summarisation, Kazakh/Russian ASR, diarisation or local deployment |
| Exclusion criteria | Untraceable metadata, unrelated summarisation tasks, or claims that cannot be checked against the source |

The review distinguishes scientific publications from software documentation. DOI metadata and access dates are listed in the References section.

## 2. Analysis table

| ID | Reference | Year | Type | Problem | Method / contribution | Data / languages | Relevance and limitation |
|---|---|---:|---|---|---|---|---|
| LIT-01 | Jiang, Zou, Xu & Zhang, “GATSum: Graph-Based Topic-Aware Abstract Text Summarization” | 2022 | Journal article | Long-document topic structure | Graph-based topic-aware abstractive summarisation | General text; language depends on corpus | Supports modelling topic transitions; not a meeting-specific or Kazakh evaluation |
| LIT-02 | Rennard, Shang, Hunter & Vazirgiannis, “Abstractive Meeting Summarization: A Survey” | 2023 | Survey | Fragmented meeting-summarisation research | Reviews datasets, evaluation and modelling approaches | Meeting data, primarily English | Frames the evaluation plan; does not solve local multilingual deployment |
| LIT-03 | Karabaliyev & Kolesnikova, “Kazakh Speech and Recognition Methods: Error Analysis and Improvement Prospects” | 2024 | Journal article | Recognition errors for Kazakh speech | Error analysis and improvement directions | Kazakh | Motivates language-specific error reporting; does not provide our product workflow |
| LIT-04 | Makhataeva, Atymtay, Meiramov et al., “Multilingual Automatic Speech Recognition Interface for Typing” | 2025 | Journal article | Usability and performance across languages | Multilingual ASR interface evaluation | Kazakh, Russian and English | Supports bilingual UX requirements; typing-interface results are not meeting diarisation results |
| LIT-05 | Aben, Kazbekova, Ismagulova & Ibrayeva, “Audio-to-Text Translation for the Hard of Hearing” | 2025 | Journal article | Accessible audio-to-text conversion | Whisper model-based study | Audio-to-text; language scope reported by source | Supports Whisper as a candidate; accuracy and meeting-domain transfer require local evaluation |
| LIT-06 | Zhabayev & Tukeyev, “Development of Technology for Summarization of Kazakh Text” | 2021 | Journal article | Kazakh text summarisation | Technology for abstractive/extractive Kazakh summarisation | Kazakh text | Establishes Kazakh summarisation context; meeting transcripts remain a harder domain |
| LIT-07 | OpenNMT, “CTranslate2” | — | Open-source software repository | Efficient local neural inference | CTranslate2 software engine for transformer models | Local deployment; model-dependent languages | Supports resource-efficient inference; repository documentation is not a peer-reviewed study |
| LIT-08 | Adams et al., “From Sparse to Dense: GPT-4 Summarization with Chain of Density Prompting” | 2023 | Workshop paper | Preserving salient entities while increasing summary density | Chain-of-Density prompting | English news summarisation setting | Provides a prompt-design idea; it must be tested rather than assumed to work for bilingual meetings |

## 3. Critical review by theme

### Meeting summarisation

Meeting summaries must preserve decisions, speakers and commitments rather than only compressing topical content. The survey in LIT-02 provides the broad evaluation context, while LIT-01 motivates explicit topic structure. The project therefore evaluates summaries together with action-item fields and supporting quotes, not only generic text overlap.

### Kazakh and multilingual ASR

LIT-03 identifies language-specific recognition errors, and LIT-04 evaluates a Kazakh/Russian/English interface. LIT-05 provides evidence for a Whisper-based direction. These sources support recording language metadata and reporting separate Kazakh, Russian and mixed-language results. They do not justify assuming equal performance across languages.

### Kazakh summarisation and local inference

LIT-06 provides a Kazakh summarisation baseline. CTranslate2 provides an engineering route for local inference, while its repository status means it must not be cited as a scientific result. Prompting ideas from LIT-08 are treated as an experiment, with human verification required for names, deadlines and ownership.

## 4. Limitations the project takes into account

| Limitation | Source IDs | Project response |
|---|---|---|
| Topic structure and long context can be lost | LIT-01, LIT-02 | Use staged processing and verify summaries against transcript segments |
| Kazakh and mixed-language ASR errors are not uniform | LIT-03, LIT-04, LIT-05 | Report results by language and preserve editable transcript text |
| Kazakh meeting summarisation evidence is limited | LIT-06 | Treat the Kazakh summariser as an evaluated candidate, not a guaranteed baseline |
| Prompting does not replace factual verification | LIT-08 | Require action-item review and audio-quote seeking before export |
| Inference engines have different licensing and performance constraints | LIT-07 | Record model and engine versions and test local resource usage |

## References

1. M. Jiang, Y. Zou, J. Xu, and M. Zhang, “GATSum: Graph-Based Topic-Aware Abstract Text Summarization,” *Information Technology and Control*, vol. 51, no. 2, 2022. DOI: [10.5755/j01.itc.51.2.30796](https://doi.org/10.5755/j01.itc.51.2.30796). Accessed: October 2026.
2. V. Rennard, G. Shang, J. Hunter, and M. Vazirgiannis, “Abstractive Meeting Summarization: A Survey,” *Transactions of the Association for Computational Linguistics*, vol. 11, 2023. DOI: [10.1162/tacl_a_00578](https://doi.org/10.1162/tacl_a_00578). Accessed: October 2026.
3. Y. Karabaliyev and K. Kolesnikova, “Kazakh Speech and Recognition Methods: Error Analysis and Improvement Prospects,” *Scientific Journal of Astana IT University*, vol. 20, 2024. DOI: [10.37943/20DZGH8448](https://doi.org/10.37943/20DZGH8448). Accessed: October 2026.
4. Zh. Makhataeva, N. Atymtay, R. Meiramov et al., “Multilingual Automatic Speech Recognition Interface for Typing: Usability Study and Performance Evaluation for Kazakh, Russian, and English,” *Scientific Journal of Astana IT University*, vol. 24, 2025. DOI: [10.37943/24AHNP6638](https://doi.org/10.37943/24AHNP6638). Accessed: October 2026.
5. A. Aben, G. Kazbekova, Zh. Ismagulova, and G. Ibrayeva, “Audio-to-Text Translation for the Hard of Hearing: A Whisper Model-Based Study,” *Scientific Journal of Astana IT University*, vol. 22, 2025. DOI: [10.37943/22SNOK5872](https://doi.org/10.37943/22SNOK5872). Accessed: October 2026.
6. T. Zhabayev and U. Tukeyev, “Development of Technology for Summarization of Kazakh Text,” *International Journal of Advanced Computer Science and Applications*, vol. 12, no. 9, 2021. Accessed: October 2026.
7. OpenNMT, “CTranslate2,” open-source software repository, 2026. Available: [https://github.com/OpenNMT/CTranslate2](https://github.com/OpenNMT/CTranslate2). Accessed: October 2026.
8. G. Adams et al., “From Sparse to Dense: GPT-4 Summarization with Chain of Density Prompting,” *NewSum Workshop*, 2023. DOI: [10.18653/v1/2023.newsum-1.7](https://doi.org/10.18653/v1/2023.newsum-1.7). Accessed: October 2026.
