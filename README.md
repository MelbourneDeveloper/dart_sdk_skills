# Dart SDK Skills for Claude Code

[Claude Code Agent Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) that help Claude navigate the Dart SDK development workflow — environment setup, builds, tests, and language changes.

## Skills

| Skill | What it does |
|-------|-------------|
| `setup-dart-sdk-dev` | Set up depot_tools, bootstrapping SDK, gclient sync |
| `build-dart-sdk` | Build the VM, compilers, and SDK targets |
| `run-dart-tests` | Run language, corelib, analyzer, and web test suites |
| `modify-dart-language` | Guide for adding AST nodes, parser rules, CFE changes, and experimental flags |

## Installing into the Dart SDK repo

Copy the skill directories into `.claude/skills/` inside your local `dart/sdk` checkout:

```bash
# From inside the dart/sdk checkout
mkdir -p .claude/skills

cp -r /path/to/dart_sdk_skills/setup-dart-sdk-dev  .claude/skills/
cp -r /path/to/dart_sdk_skills/build-dart-sdk       .claude/skills/
cp -r /path/to/dart_sdk_skills/run-dart-tests        .claude/skills/
cp -r /path/to/dart_sdk_skills/modify-dart-language  .claude/skills/
```

Or clone this repo and symlink:

```bash
git clone https://github.com/YOUR_USERNAME/dart_sdk_skills
ln -s $(pwd)/dart_sdk_skills/setup-dart-sdk-dev  dart/sdk/.claude/skills/setup-dart-sdk-dev
ln -s $(pwd)/dart_sdk_skills/build-dart-sdk       dart/sdk/.claude/skills/build-dart-sdk
ln -s $(pwd)/dart_sdk_skills/run-dart-tests        dart/sdk/.claude/skills/run-dart-tests
ln -s $(pwd)/dart_sdk_skills/modify-dart-language  dart/sdk/.claude/skills/modify-dart-language
```

Claude Code automatically discovers skills placed in `.claude/skills/`.

## Example workflow

Once installed, Claude can set up, build, and test entirely through these skills:

```
> Set up the dev environment and build the SDK runtime
> Run the language tests for record spreads
> Add a new experimental flag called my-feature
```

## Real-world example

[dart-lang/sdk#62630](https://github.com/dart-lang/sdk/pull/62630) was produced using these skills. **Note: the PR was rejected** — not because of code quality, but because it lacked a corresponding language specification change. Dart language features require both an implementation PR and a spec update to the [language repo](https://github.com/dart-lang/language). The skills help with the implementation side; the spec work is separate and required before a PR will be accepted.

## Contributing

Each skill lives in its own directory with a `SKILL.md` (the skill definition) and a `scripts/` folder (shell helpers). Patterns and reference docs are kept as separate markdown files linked from the skill.
