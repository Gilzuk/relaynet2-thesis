# Deep Learning Architectures for Two-Hop Relay Communication

M.Sc. thesis, Tel Aviv University, Gil Zukerman, 2026.

This project is generated from `thesis/` in Gilzuk/relaynet2. Edit that source
repository, not this mirror. Compile `main.tex` with XeLaTeX; `thesis.pdf` is
the accompanying built artifact.

## Scope and main observations

The canonical experiment is uncoded QPSK on a two-hop SISO i.i.d. Rayleigh link.
DF matches or exceeds the tested learned relays from 6 dB upward. Separate
studies examine selected ISI/composite channels, finite-pilot and blind
receivers, and finite-length coded forwarding.

The fixed three-tap BPSK MLP has BER 0.0065 at 8 dB versus matched genie MLSE
0.001354. Required-SNR penalties depend on the target (0.26–2.53 dB at the stated
targets), not a fixed offset. The 16-dB MLP confirmation records 36 errors in
300M bits; the 18–20-dB MLP tail is not validated.

The QPSK BCJR study measures relay-output BER only; it is not an end-to-end
BCJR-versus-MLP comparison. Zero observed errors are insufficient data for a
positive BER estimate, not proof of zero true BER. Nominal rule-of-three
bounds require an independent-bit assumption for their stated coverage.

The learned relays are trained on the impairment families tested. Their results
do not establish new-family generalization, a universal advantage over
classical receiver design, or hardware latency and energy savings. The separate
coded-QPSK cost study uses a 220-parameter, 208-MAC relay, not the 170-parameter
real BPSK model.

For configurations, uncertainty, and limitations, read the compiled thesis
and its source tables. Do not treat this short overview as a substitute for the
experiment-specific methods.
