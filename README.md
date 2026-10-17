# Deep Learning Architectures for Two-Hop Relay Communication

M.Sc. thesis, Tel Aviv University, Gil Zukerman, 2026.

This project is generated from `thesis/` in Gilzuk/relaynet2. Edit that source
repository, not this mirror. Compile `main.tex` with XeLaTeX; `thesis.pdf` is
the accompanying built artifact.

## Scope and main observations

The canonical experiment is uncoded QPSK on a two-hop SISO i.i.d. Rayleigh link.
DF matches or exceeds the tested learned relays from 6 dB upward. The feedforward
relays' low-SNR advantage is over the implemented block-normalized AF; against
a conventional variable-gain AF the MLP's 0 dB margin is 0.007. Separate studies
examine selected ISI/composite channels, finite-pilot and blind receivers, and
finite-length coded forwarding.

On the coded link, the original comparisons used decoder metrics that ignore
symbol-dependent reliability. With reliability-weighted (matched) metrics at the
relay and the destination, block decode-and-forward has lower BER than both
MLP read-outs at every tested SNR (30 of 30 paired trials), so their published
high-SNR advantage came from the metric.

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

For configurations, uncertainty, and limitations, read the compiled thesis
and its source tables. Do not treat this short overview as a substitute for the
experiment-specific methods.
