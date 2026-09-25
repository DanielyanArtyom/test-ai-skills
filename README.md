# test-ai-skills

A sandbox repository for evaluating security scanners for agent skills
([SkillPlus](https://skillplus.xyz), [Snyk agent-scan](https://github.com/snyk/agent-scan)).

## Layout

```
plugins/<plugin>/skills/<skill>/SKILL.md
```

| Skill | Purpose |
|---|---|
| `plugins/sample-plugin/skills/conventional-commits` | Clean, working skill — baseline for false positives |

Skills added here are test fixtures. Do not install them into a real agent.
