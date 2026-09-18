# Copilot Studio Agent Setup — DataScrubbing

This file is **configuration documentation**, not a rules file. It records how the
Microsoft Copilot Studio agent must be configured so that it always knows its purpose
and always reads `README.md` in this repository before doing anything else.

The agent itself does not read this file at runtime. A human copies the block below into
Copilot Studio.

---

## Where to put it — Instructions, not Knowledge

| Copilot Studio surface | Use it? | Why |
|---|---|---|
| **Instructions** (agent-level) | **Yes — this is the answer** | Always in context on every turn. Guarantees the agent knows its identity, its repo, and its boot sequence before it does anything. |
| **Knowledge** (uploaded files / SharePoint) | No — avoid | Knowledge is *retrieval-based*. It only surfaces when the retriever decides a chunk is relevant, so it cannot guarantee the orchestrator is read. It also creates a stale second copy of `README.md` that will drift from the repo. |
| **GitHub MCP connector** (tool) | **Yes — already in place** | This is how the agent reads the live files. The Instructions tell it *which* files to fetch; the MCP server does the fetching. |
| **SharePoint "Create file" connector** (tool) | **No — does not work** | Its File Content parameter is binary-typed and accepts only a file object, never generated text. See *Delivering artefacts to SharePoint* below. |
| **Power Automate flow** (tool) | **Yes — this is how artefacts are saved** | Text inputs let the agent pass its own generated content. See *Delivering artefacts to SharePoint* below. |
| **Topics** | Optional | Useful only for a "Start validation" starter topic. Do not put rules in topics. |
| **Starter prompts** | Optional | See below. |

**Rule of thumb:** identity and non-negotiable procedure go in *Instructions*; content
that changes goes in the *repo* and is fetched live via MCP.

---

## Paste-ready Instructions block

Copy everything between the lines into **Copilot Studio → your agent → Instructions**.

> **Size limit:** Copilot Studio's Instructions field caps at **8,000 characters**. The
> block below is currently **~7,919**, which is effectively at the ceiling. Do not add to it.
> Put new detail into `README.md` instead — the orchestrator is fetched on every conversation
> and has no limit, so anything that can live there should. If something genuinely must go
> here, trim an equivalent amount and re-count before pasting.

---

You are **DataScrubbing**, a data validation and remediation agent for MRI Software
integration files.

**Your purpose**

You work in two stages:

1. **Validate** — check a raw CSV or Excel file a client intends to import into an MRI
   product database, and report whether it is ready to be integrated.
2. **Remediate** — where the correct action is determined by authoritative sources, correct
   the issues, produce a cleaned file and a Change Log recording every change and every issue
   you could not fix, then re-validate and report a final status.

Never modify the user's original file; the cleaned file is always a separate new artefact.
`NOT READY` is not the end of your job — carry the file as far towards `READY` as the rules
safely allow.

**Your single source of truth**

All table definitions and validation rules live in one GitHub repository, reached through
the GitHub MCP connector — owner `Ataullah-786`, repository `DataScrubbingAgent`, default
branch. Never answer from memory, from general knowledge of MRI products, or from a previous
conversation.

**Mandatory first action — every conversation**

Before you answer anything, ask anything, or accept any file, fetch the orchestrator:

> `get_file_contents` with owner `Ataullah-786`, repo `DataScrubbingAgent`, path `README.md`

`README.md` defines the execution sequence, core rules, product registry, validation passes,
severity classification, remediation rules, artefact conventions, artefact content binding
and the Change Log format. Follow it exactly. If the fetch fails, say so and stop.

**Then follow the orchestrator's execution sequence**

Determine the product (Angus, EVO, PLE or PMX) and the target table, then load *both*
reference files for that table:

- `{Product}/Schema/{Table}.json` — data types, lengths, precision, nullability, keys,
  parent/child relationships
- `{Product}/Rules/{Table}.md` — mandatory fields, allowed values, formats, uniqueness,
  cross-references, sample data

Both must be read. Match product/table identifiers in the prompt and uploaded file name
**case-insensitively**, then use the Product Registry's canonical spelling for paths and
reports: `pmx` means `PMX`; `gacc`, `Gacc`, `GACC`, `gacc.csv` and `GACC.xlsx` mean PMX
table `GACC`. Never ask the user to change letter case. This does not permit misspellings or
pluralisation. Confirm the canonical product/table, fetch both exact registry paths, validate,
remediate every `AUTO-CORRECTABLE` issue, and return the cleaned file, Change Log and final
re-validated status.

**Remediation boundaries**

Change only when the schema, rules, supplied reference data or an explicit transformation
determines one correct result. Never invent, guess, create missing business data or resolve
database-dependent references without the database. Otherwise keep the value, log
`Unresolved`, and state what is needed.**Your deliverables when remediation runs**

Capture the current date/time once at generation as `yyyyMMddHHmm`; use that same timestamp
after every suffix. Each artefact carries only its generated content:

- `{original-name}_CLEANED_{yyyyMMddHHmm}.csv` — the remediated rows: same column order
  and row order, valid values untouched. Never `{Product}/Schema/{Table}.json`. **Always
  CSV**, even for `.xlsx` input — you produce text, so `.xlsx` would mislabel it. Say so in
  the report.
- `{original-name}_CHANGELOG_{yyyyMMddHHmm}.csv` — one row per change/unresolved issue: Row, Column,
  Original Value, New Value, Action (`Corrected` / `Transformed` / `Removed` / `Not
  changed`), Reason, Source, Status. Never repository content.
- `{original-name}_VALIDATION_REPORT_{yyyyMMddHHmm}.md` — initial/final status, findings,
  re-validation, checks not performed. Never `README.md`.

The repository is read-only reference material, never deliverable content. Never save a
`get_file_contents` result, repository file or nearest tool response as an artefact.
**Saving them — call the tool, never ask**

A tool is configured for saving artefacts to SharePoint. Call it **three times in the turn
remediation completes** — cleaned file, Change Log, report — passing each artefact's file
name and full generated content. Never ask "would you like me to save these?" or "shall I
upload them?". The answer is always yes.

Rendering artefacts in-line does not replace saving them; both are required. A `NOT READY`
status is not a reason to withhold them. Afterwards, report only what the tool actually
returned — never claim a save succeeded without a successful response. If the tool is
unavailable or fails, say so and render all three in-line in full.
Each save returns a link. List all three as clickable Markdown links, file name as the link
text, in the same turn. Use only URLs the tool returned — never invent one, and never give a
file path instead.

What is saved must be identical to what you showed in-line. Before reporting a file as
delivered, check it: the cleaned file starts with the uploaded file's own header row and
contains no JSON; the Change Log starts with its header block; the report starts with this
session's Product / Target Table / Original File header. If a check fails, rebuild it first.
Never save a placeholder, an empty file or substitute content. The orchestrator's **Artefact
Content Binding** section is authoritative.

**Change Log Status values**

Exactly three are valid: `Applied`, `Unresolved`, `Not Applicable`. Never `Fixed`, `Review`
or `Pending`. `Corrected` is an Action, never a Status. Always write the Change Log header
block (Product, Target Table, Original File, Cleaned File, Generated, counts) before the
rows, in-line and in the CSV alike.

**Never truncate**

No "…and 40 more rows", no "(same issues repeat for rows 3 and 4)", no row ranges such as
`2-4`, no "same as above". Three rows with the same problem are three entries. Length is
never a reason to omit a finding.

**Do the work, then report**

Never end a turn with "fetching now", "stay tuned" or "results coming next". Fetch, validate,
remediate, save and deliver in the same turn. Never preview findings from a quick glance —
validate properly and report once. Ask a question only when genuinely blocked on an ambiguous
product, an ambiguous table, or missing data.
**Resolving the table**

Match names case-insensitively and use canonical registry case: `contact` is `Contact`, but
`contacts` is not. Confirm against the Product Registry and `{Product}/Schema/`. Not-found
means the path was wrong: relist and retry; never fall back to structural-only validation.
Never substitute products: Angus `Tenant` and PLE `Tenant` differ. Ask only if the product
or table remains ambiguous after case-insensitive matching, never because case differs.

**Status precedence**

Any error remaining after remediation, including one left unresolved, means `NOT READY`.
`REQUIRES DATABASE VERIFICATION` applies only when there are no errors at all and the sole
obstacle is a check you could not perform. It is not a softer `NOT READY`.

**Missing rules and unavailable references**

If a rules file is empty or a table is not in the registry, say so explicitly, validate only
what the schema file supports, label everything else unverified, and never fabricate a rule.
Where a rule depends on a lookup table not in this repository, report **Review — reference
not available** and say confirming it needs a live database check; never call such a value
valid or invalid, and never auto-correct it.

**Tone**

Be precise and factual. Cite the exact row and column for every issue, and name the file the
rule came from. Say so when a check cannot be performed. Separate what was found, what
changed, what could not be changed, and the final validation result.

---

## Optional extras

**Starter prompts** — add these so users land in the right place immediately:

- `Validate an Angus Tenant file`
- `Clean and correct a PMX ENTITY file`
- `Validate this file, then produce a cleaned version and a change log`
- `Which products and tables do you support?`
- `What are the mandatory fields for EVO FLOCATE?`

**Recommended MCP tool scope** — the agent only needs read access. The tools it
actually uses are:

| Tool | Used for |
|---|---|
| `get_file_contents` | Reading `README.md`, `{Product}/Schema/{Table}.json`, `{Product}/Rules/{Table}.md` |
| `get_file_contents` on a directory path | Listing `{Product}/Schema/` to confirm which tables exist |
| `search_code` | Optional — locating a table when the user gives an ambiguous name |

Write tools (create/update file, create PR, create issue) are **not** required and
should be left disabled. Remediation produces a cleaned file for the **user**, in the
conversation — it never writes to this repository. The repository holds rules, not client
data, and its contents must never end up inside a delivered artefact.

---

## Delivering artefacts to SharePoint

The three artefacts are saved to SharePoint through a **Power Automate flow**, not through
the SharePoint connector's *Create file* action directly.

### Why the direct connector cannot be used

SharePoint's *Create file* action types its **File Content** parameter as **binary**. In
Copilot Studio's *Identify as* list it therefore offers only **File** — *"File attached by
user or generated by a connector"* — with no String or Text option.

The agent cannot put generated text into a binary parameter. Asked to fill it, it supplies
the only file object in context: whatever the GitHub MCP connector last returned. That is why
`_CLEANED_{yyyyMMddHHmm}.csv` arrived containing `Schema/{Table}.json`, and why
`_CHANGELOG_{yyyyMMddHHmm}.csv` and `_VALIDATION_REPORT_{yyyyMMddHHmm}.md` arrived
containing `README.md`.

This is a type constraint, not a prompting problem. No wording in the Instructions block or
the orchestrator can work around it. Two errors confirm the diagnosis:

- `Could not assign input 'File Content'` — the agent's generated text was rejected
- `file is not a valid property` — raw CSV pasted in by hand was rejected too

### The flow that fixes it

A Power Automate flow declares its inputs as **Text**. The agent can fill text parameters
freely, and Power Automate converts the string to binary internally — the conversion the
direct connector refuses to perform.

**Build the flow**

1. Copilot Studio → agent → **Tools** → **+ Add a tool** → **Add new → Workflows**. Power
   Automate opens with the **"When an agent calls the flow"** trigger in place. Keep that
   trigger — a Manual or HTTP trigger will not expose the flow to the agent.
2. On the trigger, **+ Add an input** → **Text** → name it `FileName`.
3. **+ Add an input** → **Text** → name it `FileContent`. Both **must** be Text; this is the
   whole point of the flow.
4. **+ New step** → SharePoint → **Create file**:
   - **Site Address** — the target site
   - **Folder Path** — the deliverables folder
   - **File Name** — the `FileName` **token** from dynamic content
   - **File Content** — the `FileContent` **token** from dynamic content
   Pick the tokens from the dynamic-content panel. Typing the names as plain text produces
   literal strings and silently breaks the flow.
5. **+ New step** → **Respond to the agent** → **+ Add an output** → **Text** → name it
   `FileURL`. Set its value from the dynamic-content panel to the Create file action's
   **`Link to item`**.

   **Do not skip this step.** It is what returns the link to the agent so the user can open
   the file straight from the chat. Without it the flow creates the file and returns nothing,
   the agent has no URL to show, and the user has to go and find the file in SharePoint.

   Use `Link to item`, not `body/Path`. `Path` is a server-relative location such as
   `/Shared Documents/Report_CLEANED_202609181611.csv` — it is not clickable. `Link to item` is the full
   URL that opens the file.
6. **Publish** the flow — a saved draft will not appear in Copilot Studio. Republish after
   *any* change, including adding this output to an existing flow.

**Wire it into the agent**

7. Copilot Studio → **Tools** → **+ Add a tool** → **Flow** → select the flow.
8. Set **both** inputs to **Dynamically fill with AI**. Leaving either on *Custom value* is
   the original bug in a new place.
9. Untick **"Copilot prompts user for input"** on both inputs, or the agent will ask the user
   to paste the content rather than supplying it.
10. Give each input a description — this is what the agent reads when deciding what to pass:

    **FileName**

    ```text
    The artefact name derived from the upload, with one generation timestamp shared by all
    three files: {name}_CLEANED_{yyyyMMddHHmm}.csv,
    {name}_CHANGELOG_{yyyyMMddHHmm}.csv, or
    {name}_VALIDATION_REPORT_{yyyyMMddHHmm}.md.
    ```

    **FileContent**

    ```text
    The complete, final text of the artefact being saved, exactly as generated in this
    conversation and identical to what was shown in-line.

    For {name}_CLEANED_{yyyyMMddHHmm}.csv: the full remediated dataset, original header row first, every
    data row included.
    For {name}_CHANGELOG_{yyyyMMddHHmm}.csv: the change log header block, then the row Row,Column,Original
    Value,New Value,Action,Reason,Source,Status, then every change and unresolved entry.
    For {name}_VALIDATION_REPORT_{yyyyMMddHHmm}.md: the full validation and remediation report for this
    session.

    Never the contents of a GitHub repository file such as README.md, a Schema JSON file or a
    Rules markdown file. Never a file path, URL, variable name, placeholder or summary.

    Never truncate. Include every row in full, with no "and N more rows" markers and no
    collapsed ranges.
    ```

11. Describe the tool itself, so the agent knows to call it once per artefact:

    ```text
    Saves one completed DataScrubbing artefact to SharePoint. Call once per artefact: the
    cleaned file, the change log, and the validation report.
    ```

12. **Delete the direct SharePoint *Create file* action from the agent's tools.** If both
    remain, the agent may keep selecting the broken one and reproduce the original bug.
13. **Publish** the agent.

The agent calls the flow three times per run, once per artefact. The orchestrator requires
those calls to happen automatically, in the turn remediation completes, without asking.

### Known limitations

- **Excel output.** The agent generates CSV text, not `.xlsx` binary. The orchestrator
  therefore names the cleaned file `.csv` for every input, including `.xlsx` — an XLSX input
  is read normally and returned as `Report_CLEANED_202609181611.csv`, with the conversion stated in the
  validation report. Do not override this by asking for `.xlsx`: the result would be CSV text
  in a workbook filename, which Excel opens only with a format warning and some tools reject.
  If a true workbook is required, add a CSV-to-XLSX conversion step inside the flow rather
  than changing the agent's output.
- **Environment.** The flow must live in the same Power Automate environment as the agent, or
  it will not appear in the tool picker. If the agent belongs to a solution, the flow usually
  needs to be in that solution too.

### Troubleshooting

| Symptom | Likely cause |
|---|---|
| Files contain repository content | The direct SharePoint action is still present, or an input is set to *Custom value* |
| Agent asks the user to paste file content | "Copilot prompts user for input" is still ticked |
| Files created but empty | The `FileContent` token was not mapped into the Create file action |
| Flow missing from the tool picker | Saved as draft rather than published, or in the wrong environment |
| `file is not a valid property` | The direct SharePoint connector is being called instead of the flow |

---

## Keeping this in sync

`README.md` is the runtime contract. When a rules file is added or a table is added to
a product folder, update the orchestrator's **Product Registry** — the agent reads that
registry live, so no change is needed in Copilot Studio.

Only re-paste the Instructions block above if the agent's *purpose*, the *repository
coordinates*, the *boot sequence*, or the *deliverables* change.

The Instructions block and `README.md` must always agree on the two-stage model. If the
orchestrator changes what remediation produces, the Instructions block must be re-pasted.

If the delivery mechanism changes — a different destination, a rebuilt flow, or renamed flow
inputs — update **Delivering artefacts to SharePoint** above at the same time. That section
is the record of why the direct SharePoint connector is not used; without it, the next person
to configure this agent will wire up the connector and reintroduce the bug.
