# Dr.MR v1 User Manual

[한국어 사용 설명서](MANUAL_KO.md)

## Get started

Extract the entire Windows x64 ZIP to a writable folder and open `DrMR.exe`. Keep the `_internal` folder next to the executable. Select **English** or **한국어** in the upper-right corner to change the interface language.

Use **Load sample** to fill in the example paths. To inspect a specific program, set the workspace to a folder containing both your target program and its JSON spec. Select a writable output folder.

| Tool | What it checks | Included example |
|---|---|---|
| Dr.MR preflight | Checks the target and spec before execution. The target verdict stays `UNKNOWN`. | `invoice_candidate.py` with `capture.json` |
| Capsule Scanner | Runs an approved target and compares recorded boundaries against the spec. | `invoice_candidate.py` with `capture.json`; select `invoice_bug.py` for the intentional failure |
| TARGETPROBE | Runs an approved target and observes points registered in a compatible spec. | `synthetic_target.py` with `probe_spec_multipoint.json`; keep the companion data and rules in the example folder |

## Run a diagnosis

1. Select **Dr.MR preflight** and check the target and spec paths. You can run preflight without approving target execution.
2. To check runtime behavior, select **Capsule Scanner**. Switching tools loads that tool’s sample paths. Reselect your target and a compatible spec if you want to continue inspecting your own program. Check the approval box and confirm the local execution prompt.
3. For closer observation of specific registered points, select **TARGETPROBE**, choose its compatible spec, and approve execution.
4. Select **Open HTML report**. Use the report’s top links to switch between **Developer** and **Student**, or between English and Korean. Each run saves all four views. Links to engine reports and raw evidence show the original material in its recorded language.

Changing the workspace, target program, JSON spec, output folder, or tool clears the current approval and report shortcut. Previous reports remain in their output folders.

## Read the report

Execution status, observation completeness, and target verdict are separate. A run can show `COMPLETED` and `COMPLETE` while the target verdict is `FAIL`.

| Target verdict | Meaning |
|---|---|
| `PASS` | No contract mismatch was detected within the specified and observed scope. |
| `FAIL` | Recorded evidence shows an expected/observed mismatch. |
| `UNKNOWN` | The target was not run or the evidence was insufficient to determine a verdict. |

### Try the intentional invoice failure

Select `invoice_bug.py` and `capture.json` in Capsule Scanner, then approve and run the target.

| Event | Example result |
|---|---|
| #1 Input | Quantity `3` and unit price `10` match the spec. |
| #2 Calculation | Expected `27` and observed `20`. Both complete numeric values appear in red. This is the first recorded mismatch, at the `calculate()` boundary. |
| #3 Final output | The nested JSON field `amount` differs. The matching field `currency` and value `KRW` keep the normal text color. This later mismatch does not establish propagation. |

The **Developer** view links to the recorded events, functions, and source locations when available. The **Student** view adds hints for comparing inputs and outputs. Select **Expand value** to open a long value. A recorded mismatch does not by itself establish the root cause.

## Troubleshooting

| Code | What to do |
|---|---|
| `PROGRAM_OUTSIDE_APPROVED_WORKSPACE` | Select a workspace that contains the target and its spec. |
| `SPEC_OUTSIDE_WORKSPACE` | Select a spec inside the workspace. |
| `INVALID_EXECUTION_SPEC` | Select a compatible JSON spec or reload the selected tool’s sample. |
| `FILE_NOT_FOUND` or `TARGET_NOT_FOUND` | Use **Browse** to select the correct workspace, target, or spec. |
| `INVALID_OUTPUT` | Choose a writable output folder. |
| `TIMEOUT` | Inspect the program for long waits or loops and retry with a small synthetic input. |
| `ENGINE_ERROR` | Check the execution log and the selected paths. |

## Scope and notices

Run only programs you trust. A separate process is not an OS sandbox. Dr.MR v1 checks registered observation points and does not discover unregistered boundaries, automatically switch tools, or establish causality on its own.

The ZIP includes the Windows runtime. See `NOTICES`, `_internal/runtime/LICENSE.txt`, and `_internal/engine/LICENSE_EVALUATION_KO.md` for third-party notices and first-party evaluation terms.
