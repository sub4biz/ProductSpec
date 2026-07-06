# Validate Your First Product Spec

This is the fastest local path for trying the ProductSpec validator.

```bash
git clone https://github.com/gokulrajaram/ProductSpec.git
cd ProductSpec
npm install
npm run validate -- examples/minimal.product-spec.md
```

You should see:

```text
examples/minimal.product-spec.md: valid
```

## Install The Local CLI

For local development, run the package CLI through npm:

```bash
npm run cli -- validate examples/minimal.product-spec.md
```

This uses the `productspec` binary from `parsers/ts` without requiring a global install.

You can also link it:

```bash
npm run link:cli
```

After linking, `productspec validate examples/minimal.product-spec.md` works if your npm
global binary directory is on `PATH`. Until the package is published, `npm run cli -- ...`
is the most reliable local command.

## What Validation Checks

The v0.2 validator checks:

- required frontmatter exists
- `spec_format_version` is supported
- required frontmatter fields are present
- `artifact_type` is supported
- all mandatory sections are present
- duplicate sections are rejected
- required sections appear in the correct relative order
- custom section IDs use `custom-<kebab-name>`
- empty required sections produce warnings
- very short required sections produce warnings

Warnings do not fail validation. Errors do.
