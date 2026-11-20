# BRIDE D19: the handoff recovered whole (2026-11-19)

The recovery note beside this one (RECOVERY-HANDOFF.md, committed 01:54 UTC) records a partial recovery: the digest incomplete, the payload absent. The complete handoff was given in thread to the Claude session the same evening (20:00 EST), because the ChatGPT environment could not download files. It is seated here as received (HANDOFF-mandala-guided-2026-11-19.md), with its code blocks extracted verbatim (views.py, consts.py, payload.py, recon.py), and in the alexanarch repository at rebuild/3i-atlas-signal-search/chatgpt/handoff-2026-11-19/.

What this settles of the recovery tasks:

1. **The payload is present and the digest is complete.** The D19 compact excerpt is embedded in the handoff as base64/zlib. It decodes to 3072 bytes with sha256 e16488f0b6d62f31402309f816e44328918d94c948cf55804888ad221a6e86ca. The six fixed-pair (7/15) correlations match the recorded values to about 10⁻⁸.
2. **The calibration values and the measurement code are present**, with the nomination rule and the audit rule kept separate, and the pooled-rule blind spots. The arithmetic recomputes from the stated scales.
3. **D19 is reproduced from public voltages for scans 13 and 14.** recon.py was run by bounded range reads on GB_ATLAS_raw, with each block hash-checked. The results were BRIDE 0.42468361 on groups 7 and 15, and 0.29514844 on groups 2 and 15. See VERIFY-claude-2026-11-19.md.
4. **Still open.** The ~2.55 MB packet itself has not been recovered. Scans 15–18, the additional-time window, the July branch and the controls have not been rerun. The fixed pair 7/15 does not repeat, as the handoff itself records.
