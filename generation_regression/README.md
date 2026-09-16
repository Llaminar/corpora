# Generation regression controls

These payloads preserve exact acquired token IDs, canonical prompts and seeds,
and explicit cell-to-serial-control mappings. A speculative cell consumes its
serial control's answer; it never records an independent MTP answer.

`avx512/native-20260916/controls.json` archives the complete native acquisition:
175 serial controls and 335 MTP comparisons, with four continuous 384-token
requests per cell. The inventory retains fixed-depth diagnostic definitions;
routine CI projects only Off and dynamic depth. The payload includes source
revision/report identities and portable model-shard descriptors.

This generation is **unapproved acquisition evidence**, not an image certificate
or an AVX2 proof. Its full historical configuration is preserved, including the
then-declared prefill segmentation policy. Do not rewrite it to resemble newer
defaults. Independent numerical/ISA and configuration-compatibility review is
required before installing an approved generation in the source repository's
`scripts/ci/approved_generation_corpora.json` catalog.

Use the source repository's `scripts/ci/export_generation_controls.py` to archive
explicit existing reports in chronological order. It validates the acquisition,
does not run inference, rejects incomplete inputs and existing output paths,
and cannot approve its own output. Routine CI only reads approved payloads.

Publish LFS payloads and their data-repository commit before updating the source
gitlink. Never edit an archived generation in place; publish a new generation
with reviewed provenance when inputs or expected outputs legitimately change.
