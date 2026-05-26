# IntelligenceMesh pack fixtures

This repo mirrors the **test-fixture** pack JSONs from the main IntelligenceMesh repo's `companion-app/packs-source/v1.0.0/` directory. It exists because the main repo is private and the IntelligenceMesh app's download path can't inject auth headers — anonymous `raw.githubusercontent.com` requests need a public source.

## What this is NOT

- **Not real content.** Every pack carries a `[TEST FIXTURE]` prefix on its `name`. Every guide opens with a `[TEST FIXTURE]` disclaimer. This is LLM-generated placeholder content for exercising the install pipeline end-to-end on real devices.
- **Not production delivery infrastructure.** That decision is tracked as OFF-1380 in the main repo's Linear. This sister-repo pattern works for dev testing; production may use HuggingFace / Cloudflare R2 / etc.

## Real authoring

Replaces this content via OFF-1373..1378 in the main repo, with citations from CC-BY-compatible sources (CDC, FEMA, NIH, USGS, NOAA, USDA, etc.). The TEST FIXTURE markers in this repo are guardrails so a copy-paste accident can't silently promote placeholders to production.

## Usage

In the main repo's `companion-app/.env.local`:

```
EXPO_PUBLIC_PACKS_BASE_URL=https://raw.githubusercontent.com/Offline-Protocol/intelligencemesh-pack-fixtures/main
```

The app's `packDownloadUrl()` then resolves to `…/main/v1.0.0/<packId>.en.json` for each catalog entry.

## Keeping in sync

When the main repo's `packs-source/v1.0.0/` changes, mirror with:

```bash
cd /tmp && git clone https://github.com/Offline-Protocol/intelligencemesh-pack-fixtures.git
cp -r /path/to/companion-app/packs-source/v1.0.0 /tmp/intelligencemesh-pack-fixtures/
cd /tmp/intelligencemesh-pack-fixtures && git add . && git commit -m "Sync fixtures" && git push
```
