# Dr.MR v1

[English user manual](MANUAL_EN.md) · [한국어 사용 설명서](MANUAL_KO.md)

Dr.MR is an offline Windows x64 tool for inspecting Python programs against a JSON specification. The archive includes its Python runtime.

## Quick start

1. Extract the entire ZIP to a writable folder. Open `DrMR.exe` and keep `_internal` next to it.
2. Select **English** in the upper-right corner and choose **Load sample**. **Dr.MR preflight** checks the selected files without running the target. Its target verdict is `UNKNOWN`.
3. Select **Capsule Scanner** to compare observed runtime boundaries with the spec. Review the target and approve execution before running it. Use **TARGETPROBE** to observe points registered in a compatible spec.
4. Select **Open HTML report**. Switch between developer and student views in either language. In a failure report, differing numeric values such as `27` and `20` are highlighted in full. Matching values such as `KRW` keep the normal text color.

To try the intentional failure, use the Capsule Scanner sample and replace its target with `invoice_bug.py` while keeping `capture.json`. These example files are under `_internal/examples`.

## Support

> Donations are entirely voluntary.
> There is no difference in features or usage rights whether or not you donate.
> Thank you for supporting Dr.MR's development.

[Donate through AI World Portal on Ko-fi](https://ko-fi.com/aiportal). AI World Portal is the shared funding platform. Dr.MR is developed and branded by AI Companion Lab.

## License and notices

Run only programs you trust. Separate processes do not provide an OS sandbox. A verdict applies to the recorded scope. Free to run for individuals and businesses; not open source. See `LICENSE.md` and the third-party notices in `NOTICES/`, both included in the [latest release](https://github.com/MIJEONCHO/DrMR/releases/tag/v1.0.0-beta) ZIP.

Developed by AI Companion Lab. Copyright (c) 2026 Mijeon Cho.
