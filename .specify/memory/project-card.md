# egovframe-development: project context

## Role and maintenance boundary

Eclipse plug-ins for eGovFrame implementation, code generation, project templates, testing, batch, and mobile tooling. Preserve Eclipse extension and bundle contracts, wizard output, existing template layouts, and target-platform compatibility.
This card reflects source inspection at adoption; it does not certify runtime behavior.

## Public entry points and evidence

- `README.md`: JDK 21, platform-specific Eclipse RCP/JEE setup, target-platform configuration, and Run Configurations / Validate Plug-ins.
- `.github/workflows/maven.yml`: JDK 21 and a Maven package of only `egovframework.dev.imp.templates/pom.xml`, explicitly skipping tests.
- `egovframework.dev.imp.core/META-INF/MANIFEST.MF`: JavaSE-21 and Eclipse bundle dependencies.
- `egovframework.dev.imp.codegen.model/META-INF/MANIFEST.MF`: still declares JavaSE-1.8; do not assume every bundle has the same execution environment.
- `egovframework.dev.imp.templates/pom.xml`: a standalone templates module with Velocity and JUnit 4.13.2.

## Build and verification entry points

The exact CI packaging command is `mvn -B package --file
egovframework.dev.imp.templates/pom.xml -Dmaven.test.skip=true` (one shell line). It does not
run tests or build all PDE plug-ins. A future focused template test can use
`mvn -f egovframework.dev.imp.templates/pom.xml test`, subject to its declared dependencies.
For plug-ins follow README: import projects, configure the Eclipse target, reload the target,
and validate plug-ins in an Eclipse Application run configuration. There is no root Maven reactor.

## Environment and evidence limits

README setup differs by operating system and Eclipse release; a badge alone is not the
source of the runtime contract. PDE/UI verification needs the documented Eclipse environment.
Public fork issues #1 and #3 identify execution-environment and test-runner questions; their
existence is not evidence that a fix is agreed or tests have run.
No application build, test suite, formatter, device test, or external service was run for this
workflow-only adoption. A Spec Kit CLI/status and isolated scaffold smoke validate the tooling
only. No CodeGraph index was present in the adoption workspace; targeted file listing and
exact text inspection supplied the evidence, without installing an indexer.

## Upstream and submission baseline

Upstream: [eGovFramework/egovframe-development](https://github.com/eGovFramework/egovframe-development). Fetch the actual upstream default branch
and record its exact SHA before preparing `upstream-submit`; do not infer the baseline from
fork work. Preserve an existing submission branch or open PR. Adoption changes are pushed
only to fork `work`; an absent `upstream-submit` is created from the fetched upstream SHA
without adoption commits, as a separate submission baseline.
The [constitution](constitution.md) is the policy source for domain cards, verification, and
work-only artifact isolation. Native OMP commands are in `.omp/commands/`; the bundled bug
workflow provides assess, fix, and test stages. No application fix or PR is part of
this adoption.
