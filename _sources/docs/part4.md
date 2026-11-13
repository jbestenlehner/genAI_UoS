# Prompt Engineering & Token Efficiency

**Objective:** Learn prompt architecture, token budget optimisation, context reduction and using GenAU to automatically read academic research papers and organise them into a structured comparison table or matrix.

## Sample Open-Access Reference Library

This tutorial references the following peer-reviewed, open-access publications for hands-on prompting exercises:

1. **GelMA Hydrogels:** Yue et al., *"Synthesis, properties, and biomedical applications of gelatin methacryloyl (GelMA) hydrogels."* *Biomaterials* (2015). [DOI: 10.1016/j.biomaterials.2015.06.026](https://doi.org/10.1016/j.biomaterials.2015.06.026)

2. **Electrospun Nanofibers:** Li et al., *"Electrospun nanofibrous structure: A novel scaffold for tissue engineering."* *Journal of Biomedical Materials Research* (2002). [PubMed: 11932882](https://pubmed.ncbi.nlm.nih.gov/11932882/)

3. **Vascular Grafts:** Dahl et al., *"Readily Available Tissue-Engineered Vascular Grafts."* *Science Translational Medicine* (2011). [PubMed: 21307353](https://pubmed.ncbi.nlm.nih.gov/21307353/)

4. **Cancer Nanocarriers:** Peer et al., *"Nanocarriers as an emerging platform for cancer therapy."* *Nature Nanotechnology* (2007). [Nature: nnano.2007.387](https://www.nature.com/articles/nnano.2007.387)

5. **Titanium Nanotubes:** Roy et al., *"*$TiO_2$ *nanotubes: synthesis and applications."* *Angewandte Chemie* (2011). [PubMed: 21394857](https://pubmed.ncbi.nlm.nih.gov/21394857/)

_Note: Be careful with content under copyright and other none open-access materials._


## 1. Token Economics

### Key Concepts

* **Token Math in Scientific Manuscripts:** In Google Gemini, $1\text{ token} \approx 4\text{ characters}$ or $\approx 0.75\text{ words}$. A 10-page article from *Biomaterials* or *IEEE Transactions on Biomedical Engineering* averages $8,000$ to $14,000\text{ tokens}$ when including chemical formulas, gene markers, and experimental tables.

* **The Cost of Context Bloat:** Uploading five 30-page PDF papers simultaneously ($>60,000\text{ tokens}$) consumes extensive processing time and can reduce retrieval accuracy for specific quantitative metrics (such as Young's modulus or cell seeding density).

* **Targeted Section Slicing:** Extracting only the *Methods* and *Results* sections reduces token usage by $60\text{--}80\%$ while improving extraction accuracy.

## 2. Prompt Architecture for Literature Analysis

Vague prompts consume unnecessary tokens by forcing the model to generate generic background information. Use the **RTCE Framework** (Role, Task, Context, Execution) to eliminate generic conversational filler and direct Gemini straight to actionable research insights:

- **Role:** Set the domain expertise (e.g., Biomaterials Engineer specializing in electrospun scaffolds).
- **Task:** State the precise analytical objective.
- **Context:** Provide the relevant subfield, material class, or physiological application.
- **Execution/Constraints:** Define output structure (e.g., Markdown table, JSON schema, specific units like $\mathrm{MPa}$ or $\mathrm{g/cm^3}$).

If unsure what Markdown table or JSON schema is, just ask Gemini.

### Structural Template

```
[ROLE / DOMAIN SPECIALISATION]
Act as a Senior Biomaterials Scientist specialising in hydrogels and
tissue scaffolds.

[CONTEXT]
Evaluating photopolymerised hydrogels for cartilage tissue repair based
on Yue et al., 2015 (https://doi.org/10.1016/j.biomaterials.2015.06.026).

[TASK]
Analyse the structural and mechanical properties of GelMA hydrogels
described in the provided text snippet.

[EXECUTION & CONSTRAINTS]
- Output format: Bulleted list categorised by (1) Synthesis Conditions,
(2) Mechanical Strength, and (3) In-Vitro Biocompatibility.
- Include explicit quantitative metrics (e.g., stiffness in kPa,
swelling ratio, cell viability %).
- Omit general introductory prose or conclusions.

```

### Refactoring Exercise

* ❌ **Unoptimised Prompt (Heavy token cost, unconstrained prose):**

  > "Tell me everything about GelMA hydrogels from the Yue et al. paper, what are they made of, how strong are they, and are they good for cells?"

* ✅ **Optimiesd RTCE Prompt (Lean input, structured output):**

  > "Act as a Biomaterials Engineer. Extract the hydrogel synthesis parameters and mechanical performance metrics from the abstract below ([Yue et al., 2015](https://doi.org/10.1016/j.biomaterials.2015.06.026)).
  > Format as a 3-row table: `Parameter` | `Value / Metric` | `Testing Condition`.
  >
  > `<abstract>` \[Insert Abstract Text\] `</abstract>`"

## 3. Quantitative Property & Parameter Extraction

When mining physical and biological properties across experimental papers, prompt Gemini to standardise units and strictly flag missing values rather than inferring them.

### Hands-on Exercise: Electrospun Scaffold Characterisation

Pasting text from [Li et al., 2002 (PubMed: 11932882)](https://pubmed.ncbi.nlm.nih.gov/11932882/) or similar scaffold literature, run the following extraction prompt:

```
Role: Tissue Engineering Data Specialist.

Task: Extract quantitative scaffold characterisation metrics from the
paper excerpt wrapped in <paper_text>.

Execution Rules:
1. Format output as a Markdown table with columns:
   | Polymer Material | Fiber Diameter Range ($\mu\text{m}$) | Porosity (%) | Compressive/Tensile Modulus ($\text{MPa}$) | Cell Type Cultured |
2. Standardise all spatial metrics to micrometers ($\mu\text{m}$) and pressure metrics to Megapascals ($\text{MPa}$).
3. If an empirical metric is not explicitly stated in the text, write "NR" (Not Reported). Do NOT calculate or guess missing values.

<paper_text>
[Insert Methods/Results excerpt from electrospinning publication]
</paper_text>

```

## 4. Multi-Paper Synthesis & Literature Matrix Construction

Synthesise multiple research papers into a single structured comparative matrix without exceeding context or output generation limits.

### Multi-Study Comparative Prompt

```
Task: Synthesise the 3 publication abstracts provided below regarding cardiovascular and targeted drug delivery systems.

Sources:
- Paper 1: Dahl et al., 2011 (Vascular Grafts, https://pubmed.ncbi.nlm.nih.gov/21307353/)
- Paper 2: Peer et al., 2007 (Cancer Nanocarriers, https://www.nature.com/articles/nnano.2007.387)
- Paper 3: Roy et al., 2011 (Titanium Nanotubes, https://pubmed.ncbi.nlm.nih.gov/21394857/)

Abstract 1: [Paste Text]
Abstract 2: [Paste Text]
Abstract 3: [Paste Text]

Generate a Comparative Literature Matrix:
| Primary Author & Year | Bio-Platform Class | Target Application | Key Quantitative Outcome | Primary Material Limitation |
| :--- | :--- | :--- | :--- | :--- |

Follow the table immediately with a concise summary (max 150 words) identifying common biomaterial translation hurdles across all three platforms.

```

## 5. Grounding, Verification & Researcher Checklist

Always verify extracted numbers, chemical formulas and citations against the primary source publications.


- [ ] CONSTRAIN: Did I enforce explicit SI units (e.g., $\text{kPa}$, $\text{MPa}$, $\mu\text{m}$, $\text{wt}\%$) and table/JSON format?
- [ ] TRIM: Did I strip references, grant funding text, and institutional headers before pasting text into Gemini?
- [ ] GROUND: Did I instruct Gemini to write "NR" for missing experimental variables to prevent hallucinated numbers?
- [ ] CITE: Are all paper inputs grounded with real DOI/PubMed URLs (e.g., PubMed ID or DOI links)?
- [ ] VERIFY: Did I cross-reference critical quantitative metrics against original figures and tables in the source paper?
