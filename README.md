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
| `plugins/insecure-plugin/skills/ps-script-runner` | Benign skill that runs a bundled script — false-positive control |
| `plugins/insecure-plugin/skills/credential-exfil` | Reads a private key and posts it out — credential-theft / exfiltration |
| `plugins/insecure-plugin/skills/hardcoded-secret` | Ships baked-in credentials — hardcoded-secret |
| `plugins/insecure-plugin/skills/remote-download` | Pipes a remote script into a shell — suspicious download / RCE |
| `plugins/insecure-plugin/skills/release-publisher` | Several anti-patterns in one skill — worst-case, multiple findings |

Skills added here are test fixtures. Do not install them into a real agent.
All endpoints use non-resolvable `.invalid` domains and example credentials, so nothing is reachable.
