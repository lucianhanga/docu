# Probabilities

## Calculating probabilities

**Simple probability distribution** means that the probability of an event is the **same** for all possible **outcomes**.

$$ P(A) = \frac{number\ of\ outcomes\ in\ A}{total\ number\ of\ outcomes} $$

## The addition rule

$\cup$ means **union** and also known as **or**. Either one of the events is happening.
$\cap$ means **intersection** and also known as **and**. Means all events are happening at the same time. 

The **addition rule** is used to calculate the probability of **two or more events**.

$$ P(A \cup B) = P(A) + P(B) $$

$$ P(A \cup B \cup C) = P(A) + P(B) + P(C) $$

Attention should be paid to the **overlapping** events.

$$ P(A \cup B) = P(A) + P(B) - P(A \cap B) $$

for example:  for a coin toss, in two tosses, the probability of getting two heads is 1/4, but the probability of getting a head in the first toss and a tail in the second toss is 1/2, so the probability of getting a head or a tail is 1/2 + 1/2 - 1/4 = 3/4.

 another example: for two dices roll event A is getting a 6, event B is getting a 5, then the probability of getting a 6 or a 5 is 1/6 + 1/6 - 1/36 = 1/3.

# Independent vs dependent events

**Independent events** are events that do not affect each other. For example, the probability of getting a head in a coin toss is 1/2, and the probability of getting a head in a second coin toss is also 1/2. The probability of getting two heads in two coin tosses is 1/4.

**Dependent events** are events that affect each other. For example having a deck of cards, the probability of getting a red card is 26/52, and the probability of getting a red card after getting a red card is 25/51 because the first card is removed from the deck.


## The multiplication rule

The **multiplication rule** is used to calculate the probability of **two or more independent events**.

$$ P(A \cap B) = P(A) \times P(B) $$

$$ P(A \cap B \cap C) = P(A) \times P(B) \times P(C) $$

> **Important note:** the **order** of the events does not matter.

For **dependent** events, the multiplication rule is working as well, but the probability of the second event is calculated based on the first event.

$$ P(A \cap B) = P(A) \times P(B|A) $$

$$ P(A \cap B \cap C) = P(A) \times P(B|A) \times P(C|A \cap B) $$

The notation $P(B|A)$ means the probability of event B given that event A has already happened. It is also known as the **conditional probability**.

**example**: for a deck of cards, the probability of getting a red card is 26/52, and the probability of getting a red card after getting a red card is 25/51 because the first card is removed from the deck. So the probability of getting a red card and then a red card is 26/52 * 25/51 = 325/2652.

## The complement rule

The **complement rule** is used to calculate the probability of **an event not happening**.

$$ P(\overline{A}) = 1 - P(A) $$


## Bayes' theorem

$$ P(A \cap B) = P(A) \times P(B|A) $$

$$ P(B \cap A) = P(B) \times P(A|B) $$

because $P(A \cap B) = P(B \cap A)$, we can write:

$$ P(A|B) = \frac{P(B|A) \times P(A)}{P(B)} $$

This is the **Bayes' theorem**. It is used to calculate the probability of an event given that another event has already happened.

Example: A coin ist toss twice.

Event A: There is a least one head in the two tosses.
$ P(A) = 1 - P( \overline{A}) = 1 - (1/2 \times 1/2) = 3/4 $
Event B: There are two heads in the two tosses.
$ P(B) = 1/2 \times 1/2 = 1/4 $

What is the probability of getting two heads in the two tosses given that there is at least one head in the two tosses?
Apply Bayes' theorem:
$ P(B|A) = \frac{P(A|B) \times P(B)}{P(A)} = \frac{1 \times 1/4}{3/4} = 1/3 $


##  Expected value

Having an experiment: $X$ with possible outcomes $x_1, x_2, x_3, ...$ and their probabilities $p_1, p_2, p_3, ...$:
$E(X)$ is the **expected value** of the experiment. It is the **average** of the possible outcomes.

$$ E(X) = \sum_{i=1}^n x_i \times p_i $$


## Law of large numbers

Also known as Embler's paradox. The **law of large numbers** states that the **expected value** of an experiment is **equal** to the **average** of the **results** of the experiment.

For an experiment $X$ with possible outcomes $x_1, x_2, x_3, ...$. The **average** of the **results** of the experiment is:
$$ \overline{x} = \frac{1}{n} \sum_{i=1}^n x_i $$

The **expected value** of the experiment is:
$$ E(X) = \sum_{i=1}^n x_i \times p_i $$

The **law of large numbers** states that the **expected value** of an experiment is **equal** to the **average** of the **results** of the experiment.

$$ \frac{1}{n} \sum_{i=1}^n x_in \xrightarrow[n \to \infty]{} E(X)$$

## Central limit theorem

For an experiment $X$ with possible outcomes $x_1, x_2, x_3, ...$ and their probabilities $p_1, p_2, p_3, ...$:

$$ \overline{x_{n_k}} = \frac{1}{n_k} \sum_{i=1}^{n_k} x_i$$

$ k = 1\to m $

The distribution of the values $\overline{x_{n_k}}$ are approaching a **normal distribution** as $m$ increases.

The distribution of **samples means** approaches a **normal distribution** as the sample size increases even if the original experiment is **not normally distributed**.

- The mean of the **samples means** is equal to the mean of the **original experiment**.

$$\mu_s = \mu$$ 

$\mu_s$ is the **mean** of the **samples means**.
$\mu$ is the **mean** of the **original experiment**.


- The standard deviation of the **samples means** is equal to the standard deviation of the **original experiment** divided by the square root of the sample size.

$$\sigma_s = \frac{\sigma}{\sqrt{n}}$$

where $n$ is the sample size.
$\sigma_s$ is the **standard deviation** of the **samples means**.
$\sigma$ is the **standard deviation** of the **original experiment**.
