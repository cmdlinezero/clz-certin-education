## Tutorial Authoring

When creating or revising a `certin-tutorials` tutorial, follow these invariants. Treat them as the authoring contract for tutorial structure, formatting, pedagogy, callouts, diagrams, and conclusions.

### Tutorial structure

Use the codelab tutorial format.

Frontmatter must include:

```yaml
type: tutorial
layout: codelab
learning_mode: lab
lab_modes: [codelab]
default_lab_mode: codelab
mode: interactive
```

A tutorial must contain multiple focused sections.

Every instructional section must be explicitly delimited using literal, unescaped `step` shortcodes:

```text
{{< step label="Build and run the agent" duration="6 min" >}}

Section content.

{{< /step >}}
```

Do not escape shortcode delimiters.

Valid:

```text
{{< step label="Set up the application" duration="4 min" >}}
{{< /step >}}
```

Invalid:

```text
{{\< step label="Set up the application" duration="4 min" \>}}
{{\< /step \>}}
```

Use human-readable durations in the form `N min`, such as `4 min` or `10 min`.

Each step should represent a coherent learning activity rather than being used merely to divide a long document.

### Fenced code blocks

The fenced-block type or language must immediately follow the opening backticks.

Any configuration for the block belongs inside braces after the language.

For example:

```text
```bash {terminal="true" file-id="adk1-init" cmd-id="cmd-adk1-init" copy="true"}
go mod init example.com/tutorial
```
```

The braces contain parameters only. They must not contain the fenced-block type.

Parameter values must be quoted.

Prefer an appropriate language identifier such as `bash`, `go`, `json`, `yaml`, or `mermaid` rather than an untyped code fence.

Do not create empty fenced blocks whose only purpose is to display a `message` parameter.

For example, do not use:

```text
```text {message="Go Module and ADK Dependency Checkpoint"}
```
```

If information belongs in the tutorial narrative, express it as prose or an appropriate semantic callout.

### Knowledge checks

Use knowledge checks to reinforce understanding of a concept or architectural decision introduced by the current instructional material.

A knowledge check should test comprehension rather than simple recall of a command the learner has just copied.

Keep checks associated with the instructional step whose knowledge they reinforce.

Do not place a knowledge check in the tutorial Conclusion section.

### Semantic callouts

Use `info`, `warn`, and `hint` blocks selectively and locally.

A callout must have a clear semantic reason to exist. Do not use callouts merely to create visual variety, divide long prose, or repeat information already stated in the surrounding text.

Use **`info`** for a key discrete pattern, principle, or piece of information relevant to the current section.

Think:

> Recognize this pattern.

Use **`warn`** for a key discrete anti-pattern, pitfall, dangerous assumption, or warning relevant to the current section. Where useful, explain why the pattern should be avoided.

Think:

> Avoid this pattern.

Use **`hint`** for useful knowledge that consolidates or connects concepts in a way that may not be immediately apparent from the primary instruction.

A hint should help the learner infer a relationship, implication, or reusable insight without being necessary to complete the primary task.

Think:

> Connect or infer this knowledge.

A section does not need a callout. Prefer no callout when there is nothing important enough to elevate.

Callouts should remain section-local: they should reinforce the concept currently being taught rather than introduce unrelated future material.

### Diagrams

Choose the diagram type according to the semantics being explained rather than defaulting to a flow diagram.

Use a **sequence diagram** when roles or participants are defined and the important concept is their interaction over time.

For example, an interaction involving:

```text
User → Agent → Model → Toolset → MCP Server
```

is generally better represented as a sequence diagram because the learner needs to understand who communicates with whom, in what order, and where responsibilities lie.

Use a **flow diagram** when the important concept is control flow, such as:

- branching;
- routing;
- decisions;
- workflow progression;
- state transitions;
- conditional execution;
- parallel or alternative paths.

Do not use a flowchart merely to show that one architectural role calls another.

A tutorial may contain both sequence and flow diagrams when they explain different semantics.

### Architectural teaching

Prefer teaching the smallest abstraction that correctly expresses the application.

Introduce additional abstractions because the application requires their semantics, not simply because the framework provides them.

When extending an architecture, make the reason for the new abstraction explicit.

Where relevant, distinguish responsibilities such as:

- what the model decides;
- what the agent governs;
- what a tool implements;
- what a toolset provides;
- what an MCP boundary owns;
- what a workflow explicitly orchestrates.

Use diagrams, callouts, and knowledge checks to reinforce these distinctions rather than duplicating the same explanation in several formats.

### Conclusion

Every tutorial must end with a dedicated Conclusion step.

For example:

```text
{{< step label="Conclusion" duration="2 min" >}}

...

{{< /step >}}
```

The Conclusion should:

- summarize what the learner built or accomplished;
- reinforce the principal pattern or architectural lesson;
- connect the implementation to the broader design principle;
- identify sensible extension points or the natural next tutorial where appropriate.

The Conclusion must not contain a knowledge-check fenced block.

Do not introduce a substantial new implementation task in the Conclusion.

### Overall authoring principle

Tutorial elements must serve the learning objective rather than the page layout.

Use steps to structure learning activities.

Use code blocks for executable or inspectable code.

Use knowledge checks to test understanding.

Use `info` to elevate important patterns.

Use `warn` to expose important anti-patterns.

Use `hint` to reveal useful connections or implications.

Use sequence diagrams to explain interactions between defined roles.

Use flow diagrams to explain control flow and decisions.

Use the Conclusion to consolidate the lesson without testing the learner.

When an element does not add distinct instructional value, omit it.
