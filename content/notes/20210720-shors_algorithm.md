+++
title = "Shor's Algorithm"
author = ["Victor Vialard"]
date = 2021-07-20
lastmod = 2021-07-21
draft = false
+++

-   _Goal:_ factor a number \\(N = p \times q\\) where p and q are primes
    -   Classically -&gt; \\(O \left[ exp( x \cdot n^{1/3} (\log n)^{1/3} ) \right]\\)
    -   Shor's algorithm -&gt; \\(O( n^{3} )\\)

-   Why is it important?
    -   Cryptographic operations are based on integer factoring...


## The Algorithm {#the-algorithm}

source
: <https://riliu.math.ncsu.edu/437/notes3se4.html>


### Classical Part {#classical-part}

-   _Protocol for Shor's algorithm_
    1.  Pick a number a that is _co-prime_ with n (no common factors)
    2.  Find order r of the function \\(a^{r} (mod N)\\) (i.e. the _period_ of this function, i.e. smallest r such that \\(a^{r} \equiv 1 (mod N)\\))
    3.  If r is _odd_ : pick a new a and start over
    4.  If r is _even_ : \\(x \equiv a^{r/2} (mod N)\\)
        -   And if \\(x+1 \not\equiv 0 (mod N)\\) -&gt; \\(\\{p, q\\} \in \left\\{ gcd(x+1, N), gcd(x-1, N) \right\\}\\)

-   This procedure is effective since half of the choices for a will work!
    -   But the order is hard to find...


### Discrete Fourier Transform {#discrete-fourier-transform}

-   _Magical trick_: turning a problem of factoring into a problem of <span class="underline">period-finding</span>
    -   Use the discrete Fourier transform!

-   \\(y\_{k} = \frac{1}{\sqrt{N}} \sum\_{j=0}^{n-1} x\_{j} \omega^{jk}\\), where \\(\omega = e^{2 \pi i / N}\\)
    -   This sum is maximum whenever \\(\frac{r k}{N}\\) is close to an integer

-   There should be several \\(k\\) satisfying this property...
    -   Use _continued fractions_, i.e \\(z = a\_{0} + \frac{1}{a\_{1} + \frac{1}{a\_{2} + ...}}\\)
    -   _Theorem:_ let z be a real number and \\(\frac{s}{r}\\) a rational number such that \\(\left| \frac{s}{r} -z \right| < \frac{1}{2r^{2}}\\), then \\(\frac{s}{r}\\) is a convergent of the continued fraction for z


### QFT (Quantum Fourier Transform) {#qft--quantum-fourier-transform}

-   Classically, computing the Fourier transform takes \\(O( n 2^{n})\\)
    -   QFT -&gt; \\(O(n^{2})\\)

-   QFT (recall)
    -   \\(|j> \mapsto \frac {1}{\sqrt N} \sum \_{k=0}^{N-1}e^{2\pi i j k/N} |k>\\)


### The circuit... {#the-circuit-dot-dot-dot}

{{< figure src="/ox-hugo/shors.jpeg" caption="<span class=\"figure-number\">Figure 1: </span>Shor's Algorithm - Circuit" >}}

-   Caveats of this circuit
    -   registers if \\(|x>\\) has n qubits -&gt; \\(2 \times n\\) qubits for input register
    -   with probability \\(1/2\\), r will be even


## Experimental Proof {#experimental-proof}

source
: <vandersypenExperimentalRealizationShor2001>


## Links to this note {#links-to-this-note}

-   [Introduction to Quantum Computing And Quantum Hardware]({{< relref "20210505-introduction_to_quantum_computing_and_quantum_hardware.md" >}})
