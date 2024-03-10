# Knapsack_Annealing

## *1.	Code Overview* 
*1.1	Instructions*

For this problem it was chosen to have a predefined dataset of number of items, capacity and utility. All created by random function of numpy. 
When defining the initial conditions and objective of the problem we need to make sure that the maximum capacity doesn’t exceed 2500, for that this part of the code should be run as many times as needed until this condition is met. From there we can proceed to the rest of the code. 

*1.2	Functions Explanations*

1.2.1	Objective_function
        
The objective_function is designed to calculate the total utility based on a random selection of items created by random_choice. It calculates the total utility by multiplying the utility vector by the random choice vector, while total capacity is calculated by multiplying the capacity vector by the random choice vector. The function returns the total utility if the total capacity does not exceed the maximum allowable capacity. Otherwise, it returns 0.

1.2.2	Create_neighbor

There are two methods to create a neighbor of the previous random_choice, selecting the item with the highest utility-to-weight ratio or randomly choosing an item and flipping its selection status in a given random choice vector: 
Please NOTE: run only one option at the time!

1.2.2.1	Create_neighbor by utility-to-weight ratio

The function generates a neighbor solution by selecting the item with the highest utility-to-weight ratio and flipping its selection status in a given random choice vector. It operates by computing the utility-to-weight ratio for each item based on the provided utility and capacity vectors. It then identifis the item with the highest ratio and flips its selection status in the random_choice vector, creating a neighboring solution.
To avoid division by zero, a small value (1e-10) is added to the denominator when calculating ratios.

1.2.2.2	Create_neighbor by random choice of item

The function provides a simple method for generating a neighbor solution by randomly selecting an item from the random_choice and flips its status (0 to 1 or 1 to 0).
 
1.2.3	Simulated_annealing

This function implements the Simulated Annealing optimization algorithm to find a solution for an optimization problem. The algorithm iteratively explores neighboring solutions, accepting improvements or suboptimal solutions based on a probability distribution that depends on the current "temperature."
It initializes with the random_choice and iteratively explores neighbors solutions using create_neighbor. The algorithm accepts a new solution if it improves the objective_function value or based on the probability of accepting suboptimal solutions.
The temperature parameter is gradually decreased during each iteration, controlling the likelihood of accepting suboptimal solutions. 
The optimization process is visualized with a plot showing the changes in utility, temperature, and capacity throughout the iterations.

## *2.	Analysis of influence of temperatures and cooling_rates on results*
   For this analysis it was only used the simulated_annealing function. Here the preseted values for initial_temperature and cooling_rate were changed and the main optimal solutions recorded in the following table. 

     Consider the initial conditions:
       initial_temperature = 150
       cooling_rate = 0.99

From the results it is possible to see that a cooling_rate of 0,99 gives in general better results than 0,95. A higher cooling rate will cause the temperature to decrease more rapidly. This can lead to more exploitation of the current region and can result in quicker convergence to a local optimum.
For the temperature is also noticeble that too high and too low initial temperatures give worse values of utility. So in a range of 100-300 we get the best results. Which means that there is a better ratio of exploitation and exploration of the data. 
 
     *Temperature   Cooling_rate    Number of Items 	Utility*
       1000	        0,99               47	         2928
       1000	        0,95	           51	         2768
       300         	0,99	           53	         3047
       300	        0,95	           47            2458
       150	        0,99	           49       	 2871
       150         	0,95               43	         2199
       100         	0,99               50	         3051
       100         	0,95	           47	         2382
       50          	0,99               52	         2920
       50          	0,95               44	         2245


## *3.	Testing the code considering each iteration the higher ratio utility and capacity is chosen.* 
   For this analysis check jupyter file: 	Knapsack_Annealing.ipynb
   To know if the optimal solution would be best considering that in every iteration the higher ratio of utility and capacity is the chosen item, it was added a new function to create_neighbor that makes this selection. 

    def create_neighbor(random_choice):
        # Escolher o item com o maior rácio de utilidade/peso
        ratios = utility / (capacity + 1e-10)  # Adiciona um pequeno valor para evitar divisão por zero
        chosen_index = np.argmax(ratios)
    
    vizinho = random_choice.copy()
    vizinho[chosen_index] = 1 - vizinho[chosen_index]
    return vizinho

NOTE: Be careful when running the code to only run this function. The original create_neighbor function is also in this file in order to allow comparison of results. But you can only run one at a time.

With this 2 results it is possible to see that chosing the higher ratio doesn’t necessary mean better results. Although it may seem that prioritizing items that offer the best utility-to-weight ratio, can lead to more efficient utilization of the backpack's total capacity, the reality is that other factors stop being take into account. The overall disavantages of this approach are the lack of diversity, since all the same items are being picked every time, or if there are items with very high utilities, even if their utility-to-weight ratios are slightly lower, the final solution might be better if those items are very high.
