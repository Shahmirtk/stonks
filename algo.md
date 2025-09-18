# **Optimal Portfolio**
## **- Using Genetic Algorithm**


### Summary

We start by initializing a population of portfolios. Then generations are run until max number of generations are run or delta is below threshold.

In each generation, the following happens:

1. Fitness of each individual is stored.
2. The best fit in the population is stored.
3. Half of the population size is selected using roulette wheel selection as parents.
4. Pairs of parents are made.
5. For all the pairs of parents, two children are produced using crossover.
6. Mutation occurs in the population.
7. A new population is made by vertical stack of the parents and the mutated offspring.


Key parameters are:

* POP\_SIZE
* CHROMOSOME\_LENGTH
* MUTATION\_RATE
* NUM\_GENERATIONS
* DELTA\_THRESHOLD


### Details

#### Population

Population is represented as a 2D array of size(POP\_SIZE, CHROMOSOME\_LENGTH), where each individual in the population has a certain weight for each stock and the weights sum to 1.00. The stock at index is 0 is the largest stock by market cap and that at POP\_SIZE - 1 is the smallest. The population is initiated as a spectrum from fully invested in the biggest stock to fully invested in the smallest stock, with only positive weights.

#### Fitness

A key metric for measuring the fitness of a portfolio is the Sharpe ratio, however, for this purpose we can do a simple return per unit of risk, as follows,
1. First, if no returns csv is available, store stock monthly returns in a csv like so,
    1. Iterate over the files in /data/kse100.
    2. In each file, select the Date and Close column.
    3. Only select the rows with the max date per month.
    4. Calculate return as current / previous then subtracting 1. For the last row, there will be no return.
    5. Add the returns to a table, such that by the end of iteration, you have 100 by 60 returns (100 stocks, 60 months).
2. Read the csv of returns, then select two periods of data, one for the stagnant period, and one for the period of growth: 0:24; 36:48. Leave some data for testing.
3. Multiply each stock's returns by its weight in the portfolio. 100x1 * 100xN.
4. Add the weighted returns in each column to form a 100x1 portfolio return array.
5. The avg of this arr divided by the std. dev. will give you the fitness in one period.
6. Finally, (0.6 * the first period's fitness + 0.4 * the second period's fitness) is the overall fitness of the portfolio.

#### Crossover

Crossover happens in the following steps:

1. A crossover point c is randomly selected, a float between 0.0 and 1.0.
2. c is converted into actual index by multiplying it with CHROMOSOME\_LENGTH.
3. Weights at indices less than c are selected from P1, and the rest from P2.
4. Since the weights will not necessarily add to 1.0, the new weights are normalized.
5. Steps 3 and 4 are repeated for Child2 with P1 and P2 swapped.

This way, the relative proportions of weights in the two parent portfolios are preserved.

#### Mutation

Mutation happens in the following steps:

1. A random number is generated, which if less than the mutation rate, causes mutation.
2. A random index is generated just like how a crossover point index is calculated.
3. The weight at the random index is halved.
4. The weights are normalized, so that they add to 1.0.
