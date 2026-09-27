# Claude Code implementation prompt — Kotlin K2 Figma Code Connect convention plugin

Paste this entire prompt into Claude Code opened at the design-system repository root. It is self-contained. If available, also attach `FIGMA_SINGLE_ANNOTATION_IMPLEMENTATION.md` as supporting context; the requirements below are sufficient without that file.

---

## Role and working standard

Act with the combined expertise of a Principal Kotlin Compiler Engineer, Principal Android Design-System Engineer, Principal Gradle Build Engineer, Figma Code Connect specialist and technical reviewer.

Implement working repository-integrated code. Do not finish with only a proposal, diagrams, empty plugin classes, TODOs, hardcoded demonstration output or instructions for me to implement the rest. Inspect the repository, audit the existing integration, adapt the plan to evidence, implement, validate and document the result.

Use the repository's actual skills, conventions and instructions. Discover available skills before claiming to use them. Treat these role names as responsibilities, not fabricated installed skills. This prompt authorizes local implementation and necessary local verification; it does not authorize remote publishing, pushing branches, sending messages or modifying Figma files.

## Goal and fixed requirements

Build a local annotation-driven Figma Code Connect generator for the existing Kotlin / Jetpack Compose SDK. The repository already uses convention plugins. Integrate with that architecture.

The intended developer experience is:

```kotlin
plugins {
    // Preserve existing Android and Compose conventions.
    id("designsystem.figma.connect") // Proposed ID; use our existing namespace.
}
```

```kotlin
@GenerateFigmaConnect(url = "ACTUAL_FIGMA_COMPONENT_URL")
@Composable
fun ExistingComponent(/* existing parameters */) {
    // Existing implementation stays unchanged.
}
```

One annotation on the component is the authoring entry point. Do not require annotations on every parameter. Exceptional semantic mappings and model-construction rules may live in a separate, versioned sidecar registry.

Mandatory requirements:

1. Use a real Kotlin K2-compatible compiler plugin with appropriate FIR/IR analysis. Do not use KSP or kapt for this feature, and do not replace the compiler analysis with regex parsing.
2. Add a convention plugin to the existing convention-plugin build. Do not create a parallel build architecture or replace existing conventions.
3. Activate the custom compiler plugin only for explicitly supported debug main compilations. Release and test compilations must not receive it by default.
4. Ship no custom annotation applications, annotation class, compiler plugin, compiler dependencies or generated Figma documentation in the released SDK binary or its consumer dependency metadata.
5. Generate maintained parserless `*.figma.ts` templates using `figma.code` and a default export. Do not generate new legacy `*.figma.tsx` / `figma.connect()` artifacts.
6. Keep the workflow local. I do not have CI/CD. Figma template publishing stays manual.
7. Evaluate the current Figma Code Connect integration before deciding what to reuse, repair, migrate or add.
8. Preserve component APIs, signatures, defaults, existing models, themes, interaction behavior, animations, accessibility and runtime dependencies.
9. Keep the current Kotlin, Compose compiler, AGP, Gradle and JDK versions unless a genuinely blocking incompatibility requires a decision from me. Do not silently upgrade the toolchain.
10. Explain unsupported or ambiguous cases honestly. A single marker does not magically infer all design semantics or prove all runtime behavior.

## Available context and how to resolve missing inputs

Start in the current repository. Discover its SDK modules, convention plugins, version catalogs, publishing conventions, Code Connect configuration, component links and existing mappings. Reuse explicit Figma URLs found in trusted project configuration and documentation after verifying their relationship to the target components. Never invent file keys, node IDs, component matches, imports or compiler versions.

If the supplied workspace is not the repository, request its location before claiming implementation. If a Figma URL or permission is missing, complete independent repository work and focused fixture-based verification, then request the smallest missing input. Distinguish fixture-tested generation from live Figma verification; do not declare the integration complete while the latter is blocked.

## Skills and Figma / Figma Make capabilities

Inventory installed skills and MCP tools. Read relevant skill instructions before applying them and record their actual names and purposes in the working notes.

- Use the available Figma Code Connect skill for connection discovery, property mapping, template semantics and review.
- Load the relevant Figma design-to-code skill before calling design-context tools when that skill is required. Follow its screenshot and context requirements when inspecting visual component cases.
- Discover and use installed Figma Make skills/capabilities if this repository has supplied Make links, exported Make files or existing Make-based examples relevant to the audit. Do not invent a `figma-make` skill, slash command or tool.
- A Figma Make prototype is supporting evidence. Its generated React/web code is not the authoritative Kotlin API and must not replace production SDK components.
- Keep published Figma Design component identities distinct from Make project URLs. If a Make reference cannot resolve to a published design-library component, report that gap and request the actual component URL for Code Connect.
- When no dedicated Make capability is available, state that fact and use supported Figma MCP reads or supplied exports. Continue the parts of the task that do not depend on it.
- Do not create or modify Figma designs, publish libraries, save remote Code Connect mappings or publish/unpublish connections. Tools that save mapping associations are writes and are outside this task's authorization.
- Preserve any mandatory component-match confirmation required by the installed skills. Prepare the evidence and ask only the targeted question when needed; avoid repeated general implementation approvals.

For Code Connect reads, discover the currently available equivalents of mapping lookup, component inventory, property context and connection suggestions. Do not assume a tool schema from memory. A response saying all components are already connected does not prove those connections are correct; existing connections still need to be audited.

## Dynamic execution workflow

Manage this as an adaptive implementation, not a rigid checklist and not an endless planning exercise.

1. Read repository instructions, including applicable `AGENTS.md` / `CLAUDE.md`, and inspect the working tree before edits. Preserve unrelated changes.
2. Use an isolated local branch/worktree when compatible with repository policy and the existing working state. Do not reset, clean, stash or overwrite someone else's work without authorization.
3. Create a concise working plan and decision log under the repository's existing documentation location. Use a dependency-aware backlog with statuses such as ready, active, blocked, verified and deferred.
4. Record assumptions, evidence, actual files, baseline failures and unresolved inputs. Reuse the log to resume after interruption rather than repeating completed work.
5. At the end of each phase, inspect the actual diff and run only the checks needed to establish the next gate. Update the plan from the results. Skip already-satisfied work only with evidence; split a phase when a new dependency appears.
6. If a check fails, identify whether the failure is introduced, pre-existing or environmental. Fix in-scope defects, record unrelated failures and continue independent work. Do not disable required checks to get a green result.
7. Continue automatically through authorized implementation phases. Do not stop after the audit or after printing a plan. Ask only for a missing fact, an ambiguous component match, a toolchain change or another decision that genuinely blocks safe progress.
8. Make changes reviewable in cohesive units. Use local commits if repository policy permits; otherwise report suggested commit/PR boundaries. Do not push, open remote PRs or merge without existing authorization.
9. Give concise progress updates with the finding, next action and any material blocker. Do not claim a phase is complete until its gate has been checked.

Use the phases below as an initial dependency structure. Adjust their boundaries based on the audit, while retaining their outcomes and the final acceptance criteria.

## Phase A — Audit the repository and current Code Connect

Before changing integration behavior, inspect:

- Actual Kotlin compiler/KGP, Compose compiler, AGP, Gradle wrapper and JDK versions; whether Android uses built-in Kotlin, the conventional Kotlin Android plugin or KMP.
- Convention-plugin build topology, plugin IDs, source layout, catalogs, helpers, included-build dependency rules and existing test fixtures.
- SDK modules, source sets, flavors, debug/release compilations, publication variants, AAR packaging, sources JAR and API documentation policy.
- Existing Figma CLI versions/configuration, npm tooling, Gradle plugins, annotation modules, template files, mapping registries, generated directories and manual commands.
- Existing legacy Compose Code Connect annotations/parsers and parserless templates. Determine who owns each file and whether it is handwritten, generated or remotely managed.
- Existing Figma Make references, if any, and their relationship to real SDK components and published design-library nodes.
- Component models, enums, sealed classes, overloads, previews, playground examples, tests and usages for representative simple and complex components.

Audit known current connections using live read-only Figma data when available. Check exact node identities, property names/types, exhaustive enum values, booleans, nested instances, instance swaps, slots, defaults, imports and the real Kotlin component call. Compare local mapping state with remotely published mapping state where available.

Produce an evidence-backed audit table:

| Component / connection | Local source | Figma identity | Format | Coverage | Defect or gap | Evidence | Decision |
| --- | --- | --- | --- | --- | --- | --- | --- |

Decisions must be explicit: reuse, repair, migrate beside existing output, replace after verified parity, or unresolved. Include risk/severity where it helps prioritization. Separate verified findings from assumptions and unavailable data. If no integration exists, report that evidence rather than fabricating an evaluation.

Gate: identify the actual extension points, existing integration state, compatible compiler version, supported debug variants and at least one simple and one complex pilot candidate. Capture baseline build results. Continue local infrastructure work if live Figma reads are blocked, while clearly preserving that blocker.

## Phase B — Implement convention-plugin and compiler integration

Follow the existing build-logic architecture and namespace. Choose the smallest maintainable module structure. Responsibilities should include:

| Unit | Responsibility |
| --- | --- |
| Convention plugin | Project defaults, annotation dependency, debug selection, local tasks and output locations |
| Gradle compiler bridge | Resolve the compiler artifact and attach it only to supported compilations |
| Annotation artifact | Private plain JVM JAR containing the SOURCE-retained function marker |
| K2 compiler artifact | FIR diagnostics, supported IR analysis and versioned component contract output |
| Mapping/template engine | Figma schema matching, retained rules, template generation and case coverage |

Implement the marker:

```kotlin
@Target(AnnotationTarget.FUNCTION)
@Retention(AnnotationRetention.SOURCE)
annotation class GenerateFigmaConnect(val url: String)
```

Add it as `compileOnly` to the SDK, because an annotated `src/main` function still needs the type during release compilation. Do not put the annotation declaration in the SDK module, expose it through `api`, package it via `implementation`, or rely on `debugImplementation` to compile shared annotated source.

Use the compatible `KotlinCompilerPluginSupportPlugin` bridge where supported by the actual repository setup. Map Kotlin compilations to actual Android variants and restrict applicability to approved debug main compilations. Do not use task-name substring matching or assume compilation names when flavors exist. Exclude release and test targets. Preserve other compiler plugins and processors.

Implement actual compiler-plugin service registration, option handling and `CompilerPluginRegistrar` K2 support. Use FIR extension points for relevant diagnostics and IR inspection for the bounded extraction required. Declaring `supportsK2 = true` without implementing and testing compatible extensions is insufficient.

Pin the compiler artifact to the SDK's actual supported compiler version. The Kotlin embedded in Gradle build logic may differ from the target Kotlin compiler; keep those dependency/classloader concerns separate. Avoid injecting compiler-embeddable dependencies indiscriminately into the Gradle runtime.

Resolve the compiler artifact locally through the repository's supported included-build/dependency strategy. Do not invent Maven coordinates that cannot resolve, require remote publication, assume an included build can directly access root-project modules, or introduce a cycle where tooling depends on compiling the SDK it must analyze. Avoid a mandatory `publishToMavenLocal` bootstrap.

Gate: a real debug fixture loads the plugin and emits a valid initial contract; an invalid marker produces a useful diagnostic; release compiler options and plugin classpath exclude this artifact. The plugin is applied through the existing conventions.

## Phase C — Extract useful component contracts with K2

Extract source-level component identity, exact Figma URL, signature/overload identity, imports or resolvable symbol identities, parameter types, nullability, presence and supported expression forms of defaults, enum members, reachable sealed subtypes, constructors, callbacks, slots and relevant conditional structures.

Use resolved symbols and structured analysis. Do not execute arbitrary Kotlin code or translate raw compiler debug dumps directly into API output. Define the supported expression grammar, fail or mark unsupported cases explicitly and keep the normalized contract versioned.

K2 can inspect more than a symbol-only processor, but it cannot establish arbitrary runtime truth or recover source bodies that are not available. Do not claim previews/tests outside the current compilation are present in its IR; inspect or compile them deliberately if relevant. Do not guess a resource value, runtime callback, dynamic default or business action.

Check coexistence with the actual Compose compiler. Preserve public source-level parameters and exclude synthetic composer/change-mask/default machinery. Verify the chosen phase and ordering; do not depend solely on fragile name filters.

Keep the plugin observational: no rewriting component behavior, no runtime registries, no initialization hooks and no new runtime dependencies. Compiler execution must be offline and token-free.

Handle incremental compilation deliberately. A partial compiler invocation must not overwrite the complete inventory. Either implement tracked per-source fragments with complete aggregation and deletion handling, or use a complete dedicated debug-context analysis pass for explicit generation. Do not globally disable incremental compilation. Declare generated contract outputs to Gradle so cache restoration and output-only deletion behave correctly.

Gate: simple and complex fixtures produce complete deterministic contracts, including meaningful defaults/models; unsupported expressions are identified; incremental edits and deletions do not lose unrelated components.

## Phase D — Implement Figma matching, coverage and `.figma.ts` generation

Fetch Figma definitions through explicit local Gradle tasks or supported local tooling, never inside the compiler. Reuse inspected repository tooling where appropriate. Keep credentials out of source, annotations, compiler options, templates and logs.

Resolve exact published design-library components; distinguish a component, component set and instance. Store identifiers and input fingerprints. Handle inaccessible nodes, unpublished components, rate limits and network failures without interpreting them as deletion or an empty schema.

Mapping precedence:

1. Accepted per-component sidecar decisions.
2. Explicit repository-wide conventions.
3. Unique type-compatible direct matches.
4. A diagnostic and a proposed decision requiring review.

Names are evidence, not proof. For example, `Disabled` to `enabled` needs an accepted inversion rule; `Destructive` to `Danger` needs an accepted enum alias. Retain approved relationships without requiring more annotations on the component. Use trusted local adapters or structured rules for complex model construction and conditional branches.

For every Figma property and relevant public parameter, record an outcome: mapped, intentionally defaulted, example-only, code-only, constrained, design-gap or unresolved. Required unresolved/design-gap cases block that component's publish readiness; they must not silently disappear from the template.

Required handling includes text/booleans, enum exhaustiveness, nullability, defaults, callbacks, resource-backed values, sealed models, nested models, overloaded entry points, slots, instance swaps, nested components and invalid combinations. Cover all finite variant values and structural branches; bound large cross-products explicitly and report the coverage strategy. Do not claim to enumerate every possible string or runtime state.

Generate parserless `.figma.ts` with `figma.code`, real Kotlin snippets/imports and stable identities. Preserve structured template sections for nested content; do not concatenate them into ordinary strings. Resolve configurable child instances dynamically, distinguish slots from swaps and use the pinned runtime's actual API. Implement correct Kotlin escaping for quotes, backslashes, control characters and dollar-sign interpolation. Never emit invented Kotlin parameters or imports.

Store generated templates, manifests and reports outside SDK packaged resources/assets/classes. Separate handwritten mappings from generated output. Stage writes atomically, remove only generator-owned stale outputs with explicit tracking and avoid publishing-ready directories containing a mix of stale and newly validated files.

Gate: generated templates render meaningful valid cases and emitted Kotlin fixtures compile against the actual SDK. Template parsing or TypeScript checks alone are not proof that Compose examples compile.

## Phase E — Evaluate and preserve current connections during adoption

Return to the audit decisions. Reuse valid rules and connections; repair supported defects; migrate legacy local outputs beside existing files where needed. Do not blindly regenerate or delete handwritten templates, replace every connection just because it predates this tooling, or force-overwrite remote mappings.

Compare old and new snippets for representative valid cases and explain differences. If both old and new files refer to the same node/framework, prevent accidental duplicate publication through deliberate CLI include scopes and a documented cutover. Keep rollback possible. Removing a local mapping file does not unpublish its remote connection.

Onboard the verified simple and complex components, then cover the existing in-scope annotated/mapped inventory whose identities can be verified. The generator must be general; passing two hardcoded examples is not completion. Inventory components still lacking Figma identities instead of inventing annotation URLs.

Gate: current mapping decisions are explained, known-good behavior is preserved, supported gaps are resolved and unresolved items remain visible with concrete next actions.

## Phase F — Debug-only workflow and release verification

Expose repository-appropriate versions of these custom local tasks:

```bash
./gradlew :<sdk-module>:generateFigmaConnectDebug
./gradlew :<sdk-module>:validateFigmaConnectDebug
```

Do not leave angle-bracket placeholders in the final README: replace them with actual discovered module paths and implemented commands. A shorter alias may delegate to debug only. Generation should refresh the Figma snapshot by explicit task policy or support a clearly identified offline snapshot.

Graph direction: compiler analysis produces a source contract; that contract plus Figma snapshots and accepted mappings produce templates; validation consumes templates and the SDK. No cycle may make compilation depend on templates generated from that same compilation. Figma-only changes must regenerate templates even when Kotlin compilation is up to date.

Ordinary SDK builds must not require Figma credentials or API access. Do not attach generation to release assembly or publication. The custom compiler artifact/options must be absent from release invocations, rather than merely loaded with an enabled=false flag. Do not add CI configuration or perform publishing.

Verify all of the following with focused tests and actual artifacts:

- Exact supported Kotlin/K2/Compose versions work together; invalid annotation usage has useful diagnostics.
- Correct debug selection, including available flavors; release/tests excluded; debug and release in the same invocation remain isolated.
- Clean, incremental, unchanged and cache-restored builds; source/model changes; deletion/rename; manifest-only deletion; Figma-only changes; deterministic repeated output.
- Real templates with enums, sealed cases, nested content, constraints and Kotlin escaping; actual emitted Kotlin compilation.
- Release assembly succeeds without Figma credentials and without debug-generation tasks.
- Release AAR, nested JARs and `classes.jar` contain no custom annotation class/use, compiler-plugin classes, generated mappings, schemas, reports or annotation-only Figma URLs.
- Published POM and Gradle module metadata contain no private annotation/compiler dependency.
- An external consumer can compile against the SDK artifact without access to private tooling projects.
- Existing targeted component/API/runtime regression checks remain green, with baseline failures distinguished.

Do not rely on shrinking or ProGuard to meet release isolation. SOURCE retention removes marker uses; the separate compile-only annotation module prevents shipping its declaration class.

Inspect source publications separately. An ordinary sources JAR may still include annotation text and imports from `src/main`. If the repository publishes sources and the requirement is that those also contain no marker, present the concrete options: a Kotlin-aware exported-source copy transform or debug-only connection wrappers with explicit target relationships. Do not silently remove source publishing, rewrite originals with regex or claim SOURCE retention cleans source text.

Gate: provide evidence of both correct generation and a clean release artifact. Checks blocked by missing credentials/environment must remain marked blocked rather than passed.

## Required deliverables

Use existing documentation locations where appropriate. Produce:

1. An audit of the original local and accessible remote Code Connect state, with evidence and decisions.
2. The implementation and tested convention-plugin integration, annotation artifact, K2 compiler artifact, local resolution, mapping engine and generation/validation tasks.
3. Working usage examples from actual repository components, including one complex case.
4. A coverage report identifying mapped, constrained, unsupported and unresolved cases.
5. Local setup, generation, troubleshooting and manual publishing documentation with exact commands and required token scopes verified from current official documentation.
6. Release-isolation verification evidence and a separate statement about sources/API documentation.
7. A final implementation report with changed files, actual versions, commands/results, audit before/after, meaningful limitations, remaining blockers and reviewable commit/PR boundaries.

Manual publishing documentation may show the official CLI dry-run and publish commands, configured to the correct generated files. Do not execute publish, unpublish, remote map-saving or SDK publication as part of this task. A dry-run's scope and API requirements must be verified against the pinned CLI.

## Completion standard

Do not describe this as implemented if only the annotation exists, if the convention plugin is empty, if the compiler registrar is a stub, if outputs are hardcoded, if release still loads the custom compiler artifact, or if required checks have not been run.

Complete all work possible with available inputs. If something remains blocked, leave the repository in a coherent state, explain the exact missing input and identify what is already implemented versus unverified. Never substitute a different processor technology for the requested K2 implementation to avoid a compatibility problem.

Begin now by inspecting the repository and available skills, evaluating current Code Connect, and turning the findings into a short adaptive plan. Then continue into implementation.

## Primary references to verify against installed versions

- Kotlin compiler plugins and FIR/IR: https://kotlinlang.org/docs/custom-compiler-plugins.html
- Kotlin compiler-plugin template: https://github.com/Kotlin/compiler-plugin-template
- Kotlin compiler Gradle bridge: https://kotlinlang.org/api/kotlin-gradle-plugin/kotlin-gradle-plugin-api/org.jetbrains.kotlin.gradle.plugin/-kotlin-compiler-plugin-support-plugin/
- Gradle convention plugins: https://docs.gradle.org/current/userguide/implementing_gradle_plugins_convention.html
- Figma template format: https://developers.figma.com/docs/code-connect/template-files/
- Figma CLI: https://developers.figma.com/docs/code-connect/cli-reference/
- Figma parser migration: https://developers.figma.com/docs/code-connect/templates-migration-guide/
- Android build dependencies: https://developer.android.com/build/dependencies?hl=en
- Kotlin annotation retention: https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.annotation/-annotation-retention/

Use these as references, not as a reason to upgrade the repository to whatever version the latest documentation happens to display.
