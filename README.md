\documentclass{article}
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{float}

\begin{document}

% ----- Headline -----
\section*{Do You Know Why We Use \( n - 1 \) to Estimate the Variance of a Sample?}

% ----- Introduction -----
In descriptive statistics, it is common to define measures that evaluate the central tendency and dispersion of a population distribution. The most popular measures are the mean, median, variance, and standard deviation, defined as follows for a complete population:

Let \( X = \{x_1, x_2, \dots, x_N\} \) be a dataset of size \( N \).

\begin{itemize}
    \item \textbf{Mean (Arithmetic Average):}
    \begin{equation}
        \mu = \frac{1}{N} \sum_{i=1}^{N} x_i
        \label{eqn:mean-pop}
    \end{equation}
    \item \textbf{Variance:}
    \begin{equation}
        \sigma^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2
        \label{eqn:variance-pop}
    \end{equation}![distribution-height](https://github.com/user-attachments/assets/cbdf5186-e888-4c44-8ef0-8dbb4b6d5b3b)
![biased-vs-unbiased](https://github.com/user-attachments/assets/432e83b9-0e9a-4659-bb01-c0b2b724efa3)

    \item \textbf{Standard Deviation:}
    \begin{equation}
        \sigma = \sqrt{ \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2 }
        \label{eqn:std-dev-pop}
    \end{equation}
\end{itemize}

These formulas assume access to the entire population. However, in practice, we often only have access to a sample from the population. We use this sample to estimate the population’s true parameters.

Let \( \bar{X} = \{x_1, x_2, \dots, x_n\} \) be a sample of size \( n \). Then the sample mean and sample variance are defined as:

\begin{equation}
    \bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_i
    \label{eqn:mean-sample}
\end{equation}

\begin{equation}
    s^2 = \frac{1}{n - 1} \sum_{i=1}^{n} (x_i - \bar{x})^2
    \label{eqn:variance-sample}
\end{equation}

Here, \( \bar{x} \), \( s^2 \), and \( s \) are the sample estimates of the population mean, variance, and standard deviation, respectively.

But why do we divide by \( n - 1 \) instead of \( n \) in Equation~\ref{eqn:variance-sample}?

\section*{Expectation of a Distribution}

To understand this, we must first define the expectation (also called "esperance") of a random variable \( X \), denoted by \( E[X] \). For a discrete random variable:

\begin{equation}
    E[X] = \sum_{i=1}^{n} x_i \cdot p_i
    \label{eqn:expectation}
\end{equation}

where \( p_i \) is the probability that \( X = x_i \), and:

\begin{equation}
    \sum_{i=1}^{n} p_i = \sum_{i=1}^{n} P(X = x_i) = 1
    \label{eqn:probability-sum}
\end{equation}

\section*{Bias of an Estimator}

In statistics, we are often concerned with whether an estimator is biased or unbiased. An estimator is unbiased if its expectation equals the true population parameter. That is, the sample variance \( s^2 \) is an unbiased estimator of the population variance \( \sigma^2 \) if and only if:

\begin{equation}
    E[s^2] = \sigma^2
    \label{eqn:main}
\end{equation}

\section*{Empirical Test Using Python}

Before diving into the mathematical proof, let’s look at a simple Python simulation. It will help us understand why we divide by \( n - 1 \) when calculating the sample variance.

\subsection*{Simulation Steps:}

\begin{enumerate}
    \item Simulate a population of 300,000 people with normally distributed heights.
    \item Compute the true population variance.
    \item Take 20,000 random samples (each of size 20).
    \item Calculate variance for each sample using \( n - 1 \).
    \item Plot the distribution of sample variances.
\end{enumerate}

\subsection*{Python Code}

You can find the full Python simulation code in the following GitHub repository:

\begin{center}
\href{https://github.com/yourusername/your-repo-name/tree/main/folder-name}{\texttt{github.com/yourusername/your-repo-name}}
\end{center}

\subsection*{Visual Results}

\begin{figure}[h]
    \centering
    \includegraphics[width=0.9\textwidth]{distribution-height.png}
    \caption{Distribution of height vs. mean of $s^2$ from 20,000 samples of size $n = 20$. The green continuous line (mean sample variance) closely matches the dashed line (true variance).}
    \label{fig:distribution}
\end{figure}

\subsection*{What This Tells Us}

The histogram shows that the average sample variance (green line) closely matches the population variance (dashed line). This suggests:

\begin{equation}
    E[s^2] \approx \sigma^2
    \label{eqn:expected-s2}
\end{equation}

Using \( n - 1 \) makes the sample variance an unbiased estimator of the population variance.

\section*{What If We Use $n$ Instead?}

Now, let's see what happens if we use $n$ instead of $n-1$.

The formula for the biased estimator is:

\begin{equation}
    s^2_{\text{biased}} = \frac{1}{n} \sum_{i=1}^{n} (x_i - \bar{x})^2 \label{eqn:biased-estimator} 
\end{equation}

This is a biased estimator because it tends to underestimate the population variance.
\subsection*{Comparative Plot}

In Figure \ref{fig:biased}, we compare the biased and unbiased estimators using 20,000 samples of size n=20n=20.

\begin{figure}[H] 
    \centering 
    \includegraphics[width=0.9\textwidth]{biased-vs-unbiased.png} 
    \caption{Comparison of biased vs. unbiased variance estimators from 20,000 samples of size $n=20$.}
    \label{fig:biased} 
\end{figure}

The plot shows that the unbiased estimator (using $n-1$) stays closer to the true population variance (dashed line), while the biased estimator (using $n$) is consistently lower. This shows that using $n-1$ gives a more accurate estimate of the population variance.

\section*{Mathematical Proof: Why We Use \( n - 1 \)}

Let’s prove that the sample variance

\begin{equation}
    s^2 = \frac{1}{n - 1} \sum_{i=1}^n (x_i - \bar{x})^2
    \label{eqn:sample-variance}
\end{equation}

is an \textbf{unbiased estimator} of the population variance \( \sigma^2 \), meaning:

\begin{equation}
    E[s^2] = \sigma^2
    \label{eqn:unbiased}
\end{equation}

\subsection*{Step 1: Assumptions}

Assume the sample \( x_1, x_2, \dots, x_n \) comes from a population with mean \( \mu \) and variance \( \sigma^2 \), and that these are independent random variables.

\[
E[x_i] = \mu, \quad Var(x_i) = \sigma^2
\]

Let the sample mean be:

\begin{equation}
    \bar{x} = \frac{1}{n} \sum_{i=1}^n x_i 
    \label{eqn:sample-mean}
\end{equation}
\begin{equation}
    n \cdot \bar{x} = \sum_{i=1}^n x_i
\end{equation}

\subsection*{Step 2: Use an Equivalent Formula}

\begin{align}
    \sum_{i=1}^{n} (x_i - \bar{x})^2 
    &= \sum_{i=1}^{n} \left( x_i^2 - 2x_i\bar{x} + \bar{x}^2 \right) \notag \\
    &= \sum_{i=1}^{n} x_i^2 - 2\bar{x} \sum_{i=1}^{n} x_i + \sum_{i=1}^{n} \bar{x}^2 \notag \\
    &= \sum_{i=1}^{n} x_i^2 - n\bar{x}^2
    \label{eqn:expanded-sum}
\end{align}

So:

\[
E[s^2] = \frac{1}{n - 1} E\left[ \sum_{i=1}^n x_i^2 - n\bar{x}^2 \right]
\]

Break into two terms:

\[
E[s^2] = \frac{1}{n - 1} \left( \sum_{i=1}^n E[x_i^2] - nE[\bar{x}^2] \right)
\]

\subsection*{Step 3: Compute Expectations}

In this step, we compute the expectations of \( x_i^2 \) and \( \bar{x}^2 \) using properties of variance and expectation.

\subsubsection*{1. Expectation of \( x_i^2 \)}

We begin by calculating the expectation of \( x_i^2 \). By the definition of variance, we know:

\begin{equation}
    \text{Var}(x_i) = E[x_i^2] - (E[x_i])^2
    \label{eqn:var-xi}
\end{equation}

Rearranging this equation to solve for \( E[x_i^2] \):

\begin{equation}
    E[x_i^2] = \text{Var}(x_i) + (E[x_i])^2
    \label{eqn:expectation-xi}
\end{equation}

Since \( x_i \) is a random variable with variance \( \sigma^2 \) and expectation \( \mu \), we substitute these values into the equation:

\begin{equation}
    E[x_i^2] = \sigma^2 + \mu^2
    \label{eqn:xi-squared}
\end{equation}

Thus, we have:

\begin{equation}
    E[x_i^2] = \sigma^2 + \mu^2
\end{equation}

\subsubsection*{2. Expectation of \( \bar{x}^2 \)}

Next, we calculate the expectation of \( \bar{x}^2 \), where \( \bar{x} \) is the sample mean. We know that the expectation of \( \bar{x} \) is:

\begin{equation}
    E[\bar{x}] = \mu
    \label{eqn:expectation-x-bar}
\end{equation}

We also need to compute the variance of \( \bar{x} \). Since \( \bar{x} \) is the average of \( n \) independent observations \( x_1, x_2, \dots, x_n \), we have:

\begin{equation}
    \text{Var}(\bar{x}) = \frac{1}{n^2} \sum_{i=1}^{n} \text{Var}(x_i) = \frac{\sigma^2}{n}
    \label{eqn:var-x-bar}
\end{equation}

Now, using the definition of variance for \( \bar{x} \), we can write:

\begin{equation}
    \text{Var}(\bar{x}) = E[\bar{x}^2] - (E[\bar{x}])^2
    \label{eqn:var-x-bar-definition}
\end{equation}

Rearranging this equation to solve for \( E[\bar{x}^2] \), we get:

\begin{equation}
    E[\bar{x}^2] = \text{Var}(\bar{x}) + (E[\bar{x}])^2
    \label{eqn:expectation-x-bar-squared}
\end{equation}

Substitute the known values for \( \text{Var}(\bar{x}) \) and \( E[\bar{x}] \):

\begin{equation}
    E[\bar{x}^2] = \frac{\sigma^2}{n} + \mu^2
    \label{eqn:expectation-x-bar-squared-final}
\end{equation}

Thus, we have:

\begin{equation}
    E[\bar{x}^2] = \frac{\sigma^2}{n} + \mu^2
\end{equation}

Substitute this into the expression for \( E[s^2] \):

\begin{equation}
    E[s^2] = \frac{1}{n - 1} \left( n(\sigma^2 + \mu^2) - n\left( \frac{\sigma^2}{n} + \mu^2 \right) \right)
\end{equation}

\subsection*{Step 4: Simplify}

Simplifying the above expression:

\begin{equation}
    E[s^2] = \frac{1}{n - 1} \left( n\sigma^2 + n\mu^2 - \sigma^2 - n\mu^2 \right)
\end{equation}

\begin{equation}
    E[s^2] = \frac{1}{n - 1} \left( (n - 1)\sigma^2 \right)
\end{equation}

\begin{equation}
    E[s^2] = \sigma^2
\end{equation}

Thus, we have:

\begin{equation}
    \boxed{E[s^2] = \sigma^2}
\end{equation}

Therefore, the sample variance is an unbiased estimator of the population variance when we divide by \( n - 1 \).

\subsection*{Conclusion}

We have shown that when we divide by \( n - 1 \), the expectation of the sample variance equals the population variance:

\begin{equation}
    E\left[ \frac{1}{n - 1} \sum (x_i - \bar{x})^2 \right] = \sigma^2
\end{equation}

In contrast, if we divide by \( n \), the variance is underestimated:

\begin{equation}
    E\left[ \frac{1}{n} \sum (x_i - \bar{x})^2 \right] < \sigma^2
\end{equation}

Thus, we conclude that the correction factor \( n - 1 \) (known as Bessel's correction) ensures that the sample variance is an unbiased estimator of the population variance.

% ----- About the Author -----
\section*{About the Author}

I have a Bachelor's degree in Mechanical Engineering at the Federal University of Rio de Janeiro (UFRJ). I have a passion for math and chess, which help me sharpen my analytical thinking and problem-solving skills. Additionally, I am an enthusiast of statistics and data analysis.

\medskip

I am open to discussions, suggestions, and corrections regarding this article. Constructive feedback is always welcome!

\begin{itemize}
    \item Email: \href{mailto:flaviosds@poli.ufrj.br}{flaviosds@poli.ufrj.br}
    \item LinkedIn: \href{https://www.linkedin.com/in/flaviosds95}{https://www.linkedin.com/in/flaviosds95}
    \item GitHub: \href{https://github.com/flaviosds}{https://github.com/flaviosds}
\end{itemize}

\end{document}
