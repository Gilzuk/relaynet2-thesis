# Deep Learning Architectures for Two-Hop Relay Communication

M.Sc. thesis, Tel Aviv University, Gil Zukerman, 2026.

This project is generated from [`thesis/` in Gilzuk/relaynet2](https://github.com/Gilzuk/relaynet2/tree/main/thesis).
Edit that source repository and regenerate this mirror. Compile `main.tex` with
**XeLaTeX**; [thesis.pdf](thesis.pdf) is the accompanying built artifact.
The simulation code and experiment evidence live in the source repository,
not in this Overleaf package.

## Scope and main observations

The canonical experiment is uncoded QPSK on a two-hop SISO i.i.d. Rayleigh link.
No learned advantage over DF is resolved in the reported canonical paired tests. The feedforward
relays' low-SNR advantage is over the implemented block-normalized AF; against
a conventional variable-gain AF the MLP's 0 dB margin is 0.007. Separate studies
examine selected ISI/composite channels, finite-pilot and blind receivers, and
finite-length coded forwarding.

On the coded link, the original comparisons used decoder metrics that ignore
symbol-dependent reliability. With reliability-weighted (matched) metrics at the
relay and the destination, block decode-and-forward has lower BER than both
MLP read-outs at every tested SNR (30 of 30 paired trials), so their published
high-SNR advantage concerns the unweighted decoding pipeline. Matched Mamba
was not evaluated. These numerical summaries describe the historical runs;
additional training realizations are assessed separately below.

The fixed three-tap BPSK MLP has BER 0.0065 at 8 dB versus matched genie MLSE
0.001354, and 1.20e-7 at 16 dB versus below 3.0e-8 for the same detector at a
predeclared 1e8 bits. Matched MLSE therefore leads at every point where both
are resolved, and the required-SNR penalty grows with the target (0.26–2.53 dB
at the stated targets) rather than holding at a fixed offset. The 16-dB MLP
confirmation records 36 errors in 300M bits; the 18–20-dB MLP tail is not
validated.

The QPSK BCJR study measures relay-output BER only; it is not an end-to-end
BCJR-versus-MLP comparison. Zero observed errors are insufficient data for a
positive BER estimate, not proof of zero true BER. Nominal rule-of-three
bounds require an independent-bit assumption for their stated coverage.

The learned relays are trained on the impairment families tested. Their results
do not establish new-family generalization, a universal advantage over
classical receiver design, or hardware latency and energy savings. The separate
coded-QPSK cost study uses a 220-parameter, 208-MAC relay, not the 170-parameter
real BPSK model; with real taps the QPSK trellis factorizes exactly into two
binary trellises (2^(L+1) multiplications per symbol), so its arithmetic
crossover with the network moves to about 6.7 taps.

The SNR-penalty tables use comparable reference-defined targets; a failure to
reach a target remains an explicit bound, not an omitted observation. Smallest
model sizes refer to the tested grid and budgets. The Mamba implementations are
simplified: causal centre readouts do not give the same context as full-window
MLP/Transformer processing, and block normalization still requires the whole block.

## Reproduction and evidence

Start with the source repository's
[researcher protocol](https://github.com/Gilzuk/relaynet2/blob/main/docs/round2_reproduction_protocol.md)
and [README](https://github.com/Gilzuk/relaynet2/blob/main/README.md).
Record the source commit before running a script. This mirror does not contain
runnable experiment dependencies or checkpoints.

- **Historical configurations:** §4.3.3/Table 4.2 and
  [canonical provenance](https://github.com/Gilzuk/relaynet2/blob/main/results/canonical_run_provenance.json)
  specify architecture, scaling, sample/epoch counts, optimization, checkpoint
  selection and evaluation budgets. Historical canonical learned weights, Torch
  RNG states, software versions and epoch losses remain unavailable.
- **Additional hosted evidence:** all four workers completed; learned outputs
  differ from historical results and classical controls match. See the
  [assessment JSON](https://github.com/Gilzuk/relaynet2/blob/main/results/round2_rerun_assessment.json)
  and immutable
  [archive dc7c02c00cbe](https://github.com/Gilzuk/relaynet2/tree/dc7c02c00cbebdfb566362a810ab4b45cb6abbe0/results/reproduction).
  Differences do not invalidate the originals automatically or identify changed
  seeds as their sole cause. Repeated seed IDs are not independent new seeds.
- **Replay limits:** 12 additional canonical and 36 sequence checkpoints are
  retained. The coded classifier weights were not saved. A seed-42 native MLP
  control matched twice on one host; it does not guarantee other models or hardware.
- **One-script execution:** `scripts/reproduce_round2.py` handles the four focused
  jobs with explicit RNG policies. `scripts/reproduce_all.py` defaults to a plan
  and requires `--run` to execute; its global seed defaults to 42 and preserves
  driver-local seeds. The complete 73-entry plan has not been executed end to end.

The numerical verifier covers 892 values, not every claim. No exact historical
learned replay or statistical equivalence is claimed. Configurations and budgets
are experiment-specific; the compiled thesis and linked records take precedence
over this short overview.

## Document structure

Chapters 1–4 give background, objectives and methods; Chapter 5 gives the canonical
and coded experiments; Chapter 6 gives the unknown/mismatched-channel studies;
Chapters 7–8 discuss and summarize; Chapter 9 contains Appendices 9.1–9.7.
The standalone historical 16-QAM classifier extension is not included; the coded
16-QAM controls are included. The PDF has 120 Arabic-numbered body pages and 136
physical pages (13 front-matter and three Hebrew back-matter pages).

A GitHub update to this generated repository is not itself evidence that a linked
Overleaf project has pulled the update. Use Overleaf's GitHub pull before compiling
there.
