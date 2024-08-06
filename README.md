# CS454 Assignment 3: Genetic Programming for SBFL

Automated debugging and, in particular, fault localisation is a technique that aims to tell developer where the source of the observed failure is. In other words, if you provide test results as well as other inputs, the technique will tell you where the buggy line/method/class/file is. The aim of the second coursework is to implement a learning mechanism for automated debugging.

## Aim

The aim of this coursework is essentially to replicate a paper that evolved fault localisation techniques using Genetic Programming:

- Evolving Human Competitive Spectra-Based Fault Localisation Techniques, Search Based Software Engineering. G. Fraser and J. Teixeira de Souza, eds. Springer Berlin Heidelberg. 244–258. [PDF](https://coinse.github.io/publications/pdfs/Yoo2012kx.pdf)

Please read the paper to understand the task, as well as SBFL in general. You can also refer to the Spectrum Based Fault Localization part in [this course material from CS453](https://coinse.github.io/assets/files/teaching/cs453/cs453slide09.pdf).

## Data Preparation

You will be given raw coverage data collected from [Defects4J](https://github.com/rjust/defects4j). You need to process the data to program spectrum, following the paper and the SBFL course material. Please refer to the included Jupyter Notebook file for the tutorial on how to use the given data.

## Genetic Programming

Implement your own GP engine, and use it to find a suitable SBFL formula that ranks the faulty program element as high as possible. You are free to choose the non-terminal operators yourself. Typically SBFL formulas use the basic arithmetic operators: addition, subtraction, multiplication, and division, but feel free to expand the set if you think it helps. The aim is to lower the rank of the faulty program element as much as possible, for as many bugs as possible.

Note that, for division, you have to use the following _safe_ definition:

```
def div(x, y): # divide x with y
	if y == 0:
		return 1
	else:
		return x / y
```

## Evaluation

We will consider two metrics.

- acc@1 (accuracy at 1): this is the number of bugs that you correctly rank at the top.
- wef (wasted effort): this is essentialy the average of the absolute rank of the buggy program element, i.e., the amount of effort (= number of elements you need to investivate) needed to find the bug and do the debugging.

## Deliverables and Report

Your repo should include the underlying GP implementation as well as any code that uses it to evolve SBFL formulas: it should be self-contained. In addition, please include a `best.py` file that contains a single best formula you evolved, as follows:

```Python
def sbfl(ep, ef, np, nf):
	suspiciousness = 0.0 # Your evolved SBFL formula
	return suspiciousness
```

We will use this file against a held out set of bugs to evaluate how much your formula generalizes. Make sure you use the name `best.py` and `def sbfl(ep, ef, np, nf):` for the sake of automated grading.

In addition to your implementation, please include a PDF of your report. It should contain the following:

- A brief description of your approach: how you implement the GP engine, any unique features, etc
- The same best formula you have evolved (use the variable names 'ep', 'ef', 'np', and 'nf' to denote the formula): try to describe why it works well :)
- The evaluation results of your best formula against the bugs included in the repo: compute acc@1 against the 119 included bugs, andd also report the average wef metric per project (i.e., `Math`, `Lang`, `Time`, and `Chart`).