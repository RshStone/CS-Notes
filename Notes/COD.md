## 读书摘抄

#### About This Book

Whether your primary interest is hardware or
software, computer science or electrical engineering, the central
ideas in computer organization and design are the same. Thus, our
emphasis in this book is to show the relationship between hardware
and software and to focus on the concepts that are the basis for
current computers.

While the goal of many researchers is to make it possible for programmers to be unaware of the underlying parallel nature of the hardware they are programming, it will take many years to realize this vision. Our view is that for at least the next decade, most programmers are going to have to understand the hardware/software interface if they want programs to run efficiently on parallel computers.



The audience for this book includes those with little experience in
assembly language or logic design who need to understand basic
computer organization as well as readers with backgrounds in
assembly language and/or logic design who want to learn how to
design a computer or understand how a system works and why it
performs as it does.



We used an approach that
combined examples and measurements, based on commercial
systems, to create realistic design experiences. Our goal was to
demonstrate that computer architecture could be learned using
quantitative methodologies instead of a descriptive approach. It
was intended for the serious computing professional who wanted a
detailed understanding of computers.

#### Why RISC-V 

We didn’t want an
instruction set that required describing unnecessary baroque
features for someone’s first instruction set, no matter how popular
it is. Ideally, your initial instruction set should be an exemplar, just
like your first love. Surprisingly, you remember both fondly.

The good news is that an open instruction set that adheres closely
to the RISC principles has recently debuted, and it is rapidly
gaining a following. RISC-V, which was developed originally at UC
Berkeley, not only cleans up the quirks of the MIPS instruction set,
but it offers a simple, elegant, modern take on what instruction sets
should look like in 2017.



Readers will not only benefit from studying these RISC-V designs,
they will be able to modify them and go through the
implementation process in order to understand the impact of their
hypothetical changes on performance, die size, and energy.



The only changes for the RISC-V edition from the MIPS edition
are those associated with the change in instruction sets, which
primarily affects Chapter 2, Chapter 3, the virtual memory section
in Chapter 5, and the short VMIPS example in Chapter 6. In
Chapter 4, we switched to RISC-V instructions, changed several
figures, and added a few “Elaboration” sections, but the changes
were simpler than we had feared. Chapter 1 and the rest of the
appendices are virtually unchanged. The extensive online
documentation and combined with the magnitude of RISC-V make
it difficult to come up with a replacement for the MIPS version of
Appendix A (“Assemblers, Linkers, and the SPIM Simulator” in the
MIPS Fifth Edition). Instead, Chapters 2, 3, and 5 include quick
overviews of the hundreds of RISC-V instructions outside of the
core RISC-V instructions that we cover in detail in the rest of the
book.

#### Changes for the Fifth Edition