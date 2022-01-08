# LaTeX

### indicator variable style equations

    \[
    x_i = \left\{
      \begin{array}{l l}
      1 & \quad \text{if the ith person is female}\\
      0 & \quad \text{if the ith person is male}\\
      \end{array} \right.
    \]

### figure

    \begin{figure}
      \centering
      \includegraphics[height=0.32\textheight]{RecursionTree}
      \caption{A caption.}
      \label{fig:recursiontree}
    \end{figure}

### use numbers instead of letters in the appendix

    \appendix
    \renewcommand{\thesection}{\arabic{section}}

### footnotes

    \footnote{text, blah, blah}

### urls

    \usepackage{hyperref}

Then:

    \url{www.example.com}

### enumerations

Use `\setcounter{enumi}{<value>}` before an `item` to change the value of an
enumeration counter.

To get different markers,

```
\usepackage{enumitem}

%Roman numbers
\begin{enumerate}[label=\roman*)]
%...

% Arabic numbers
\begin{enumerate}[label=\arabic*)]
%...

% Alphabetical
\begin{enumerate}[label=\alph*)]
%...
```

Also,

```
\begin{itemize}
	\item[--] Dash
  \item[$-$] Dash
  \item[$\ast$] Asterisk
\end{itemize}
```

### matrices

We can use `bmatrix`, `pmatrix`, etc.

    \begin{pmatrix}
    \Sigma_x & \Sigma_{xy} \\
    Sigma_{xy}^T & \Sigma_y
    \end{pmatrix}

### nice limits

    \lim\limits_{x \to y}

### tables

```
\begin{table}[htb]
\centering
\begin{tabular}{crr}
\toprule
Target & $z$-location (cm) & Thickness (cm) \\
\midrule
1-Fe  & 448.1 & $2.567 \pm 0.006$ \\
1-Pb  & 448.1 & $2.578 \pm 0.012$ \\
2-Fe  & 470.2 & $2.563 \pm 0.006$ \\
2-Pb  & 470.2 & $2.581 \pm 0.016$ \\
3-Fe  & 492.3 & $2.573 \pm 0.004$ \\
3-Pb  & 492.3 & $2.563 \pm 0.004$ \\
3-C   & 492.3 & $7.620 \pm 0.005$ \\
Water & 528.4 & $17 - 24$ \\
4-Pb  & 564.5 & $0.795 \pm 0.005$ \\
5-Fe  & 577.8 & $1.289 \pm 0.006$ \\
5-Pb  & 577.8 & $1.317 \pm 0.007$ \\
\bottomrule
\end{tabular}
\caption{Neutrino target thicknesses. \cite{Aliaga2014130}
The water target thickness varies (when filled) because it is built from flexible materials and bows out in the center.
Here we work with samples that featured an empty water target.}
\label{tbl:tgtthick}
\end{table}
```

```
\begin{table}[htb]
\centering
\begin{tabular}{cccccccc}
\toprule
         & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
\midrule
2 floats (train) & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
         (train) & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
\midrule
8 floats (train) & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
         (train) & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
\midrule
16 bits (train)  & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
        (train)  & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
\midrule
64 bits (train)  & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
        (valid)  & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\
\bottomrule
\end{tabular}
\caption{Training and validation accuracy for different data representations and qubit numbers.}
\label{tbl:acctable}
\end{table}
```

### multiline equations

Note that `split` lives in the `amsmath` package.

```
\begin{equation}
\begin{split}
a =&~ b \\
  =&~ c \\
d =&~ e
\end{split}
\label{eq:eq}
\end{equation}
```

### strikethrough text

```
\usepackage{ulem} % get strikeout
\normalem         % but don't change behavior of `\emph`
```

Then, use: `\sout{text we want to strikethrough}`