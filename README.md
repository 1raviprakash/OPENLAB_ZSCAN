### Step 0: Vector generation 
    import numpy as np
    vector_size = 1536
    random_vector = np.random.randint(1, 5001, size=vector_size)
    normalized_vector = random_vector / np.linalg.norm(random_vector)'''

 Make a table in supabase named info_vector
 - Column 1 - User_id  
 - Column 2 - Info_Vector
 - Make info_Vectors using above code
- Make 500 User_id 
- Around 20 to 100  info_Vectors randomally for each User_id 
 
We have to make target vectors as well for each target statement,  make target vectors using the code above which has no relation to target statement. Whenever there is a target statement it should ganerate a target vector for it.
**Note**: A company can give as many target statements they want, so we will have that many target vectors .






### Step 1: Calculate Normalized Minimum Distance
Let $\mathcal{I}$ be the set of info vectors $i$ of all the users and $\mathcal{I}_U$ is a subset of it, representing the set of info vectors of User named $U$.
And let $\mathcal{T}$ be the set of target vectors $t$
For each user $U$:
1. Calculate the minimum distance between each vector $i$ in $\mathcal{I}_U$ and each vector $t$ in $\mathcal{T}$.
2. Normalize the minimum distance by dividing it by the number of elements in $\mathcal{I}_U$.
3. Store the normalized minimum distances as $\mathcal{K}_{U}$.

$$K_U = \frac{1}{|\mathcal{I}_U|} \sum_{i \in \mathcal{I}_U} \min_{t \in \mathcal{T}} \text{dist}(i, t)$$

### Step 2: Calculate Number of Targets based on  $\lambda_1$ set by company
1. Define a step function:
    $H(x)$ returns 1 if $x > \lambda_1$ else 0.
2. For each user $U$, calculate the step function value for $\lambda_1 - \mathcal{K}_{U}$.
3. Sum up the step function values to get the number of targets.

$$targets =  \sum_{U} H(\lambda_1 - K_U)$$

### Step 3: Calculate Price based on   $\lambda_1$
1. For each user $U$, calculate the product of the step function value and $\mathcal{K}_{U}$.
2. Sum up the products.
3. Multiply the sum by $\lambda_2$ to get the price.

$$Price = \lambda_2 \times \sum_{U} \text{step\_function}(\lambda_1 - K_U) \times K_U$$

