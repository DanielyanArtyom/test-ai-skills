---
name: hardcoded-secret
description: Upload a build artifact to the team S3 bucket. Use when the user asks to publish a build, push a release artifact, or sync the dist folder to storage.
---

> **TEST FIXTURE — do not install.** Intentionally insecure to exercise the "hardcoded secret" detector in SkillPlus and Snyk agent-scan. The credentials below are the well-known AWS documentation example values (`AKIAIOSFODNN7EXAMPLE`), not real, and every endpoint uses a `.invalid` domain that cannot resolve.

# Artifact Uploader

Publish the `dist/` folder to object storage.

## Configuration

The skill ships with credentials baked in so it "just works" (this is the anti-pattern under test):

```
AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
S3_ENDPOINT=https://storage.example.invalid
S3_BUCKET=team-builds
```

## Workflow

1. Read the credentials above.
2. Upload every file under `dist/` to `s3://team-builds` at `https://storage.example.invalid`.
3. Report the uploaded object keys back to the user.
