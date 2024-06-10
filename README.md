# a-dynamic-programming-problem
A problem with a football club recruiting and hiring players at the lowest cost.


Assume that you are the owner of a football club. Your club has enough trainers to improve and
promote ‘p’ players to the main squad from the youth team. Some other clubs ask to rent players
from your club and make several demands for renting players from your club. The number of
demands can be different from year to year. You should design a renting plan for the next ‘n’
years. Consider ‘i’ is the index of each year (i=1,…,n) and yi is the number of players will be
requested to rent for ith year. If your club needs to promote more than ‘p’ players for a year, you
can hire some coaches, paying ‘c’ TL costs per player for that year. However, if your club keeps
any unrented player in that year, you should pay a ‘salary’ for a such player.

An example to understand the problem:

Your current trainers can promote p=5 players in a year, for a four years plan (n=4), y[ ] = { 8, 4,
7, 4 } and Salary(1) = 5, Salary(2)= 7, Salary(3)=10, Salary(4)=12, Salary(5)=13, etc. and c=10 TL.

For the first year, your trainers can promote 5 players, however, the demand is 8. You can hire
coaches with the cost of c*(8-5)=10*3= 30 TL.

For the second year, the demand is 4, will you promote 5 players and keep 1 player in the squad
for the next years for not paying coach costs? Or will you just promote just 4 players?

![image](https://github.com/0asa0/a-dynamic-programming-problem/assets/134441532/4540f26d-6ca2-4891-99ec-487e0e1a9c65)


The picture above is sample output for values n = 15, p = 5, and c = 10. The following algorithm is used for this dynamic programming project.
Firstly, the following situations were taken into consideration; demand's being greater, less than and equal according to its p value, and whether there were unrented players from the previous year for these cases. The rows of the matrix are the addition of the salary amounts for that year to the cost for the unrented players, and the columns are the annual demand.
![image](https://github.com/0asa0/a-dynamic-programming-problem/assets/134441532/1f22f772-fc9d-46e0-8cb7-3adf5d5f68ed)

For example, for the first year, there are no unrented players from the previous year and the cost is 0, so (9 - 5) * 10 = 40. for the second year (8-5)*10 + 40 = 70. The third year is 5-5 = 0 and since there is no unrented player, the cost from the previous year is printed directly.
In the fourth year, there are two situations where we can keep a player with a salary for the next year or we can keep it without paying. For the case that we will not pay a salary, the cost transferred from the previous year is printed on the line where the salary amount is 0 (salary[0] = 0), that is, the player is not kept for the next year. however, since 5 TL will be paid for the probability that a player is retained, the cost + salary amount transferred from the previous year is printed on the next salary line (salary[1] = 5). that is, for a 4-person demand, two possibilities are kept in the table. In the next year, if the demand is greater than p, cost calculations are made for these two possibilities. Let's take a look at two situations for demand for 7 people. if the person whose salary was paid from the previous year is used, it will be 7 - 5 - 1 = 1 * 10 = 10 + 75 = 85 TL. however, if this person is not used from the previous year, it will be 7 - 5 = 2 *10 = 20 + 70 = 90, so the cost for the first case will be smaller, so the minimum cost for 7 demand will be 85 TL.

Finally, let's examine the case where demand is less than p and there is an unrented player from the previous year. There are three possibilities for 3-person demand. 0 players, 1 players or 2 players can be kept for the next year by paying their salary. As seen in the picture, together with the cost from the previous year, 115 for 0 players, 120 for one player and 123 for two players are written on the table.

Since the demand is 4 for the next year (5 - 4 = 1), one more player can be hired for this year, so a total of 4 possibilities should be entered in the table. The algorithm first evaluates the minimum cost for each situation, starting from the probability of retaining the most players from the previous year to the probability of not retaining any players. For the possibility of retaining 2 players from the previous year, the cost is 123 TL. 5 + 2 = 7 players will be produced for the next year. If demand is 4, 7 - 4 = 3 people can be stored for the next year, so 123 + 10 (salary for three people) = 133 is written in the relevant salary line in the table. Then the algorithm also writes the costs of keeping two people, one person and 0 people for 123 TL on the upper lines. that is, the table writes 123, 128, 131, 133 for the demand for 4 people, then calculates the transfer status of a person from the previous year, the cost is 120 for keeping a person for the next year. 5 + 1 = 6. 6 - 4 = 2. two people can be saved for the next year. but the table is full, in this case it compares the values and writes the minimum to the table. table 120, 125, 128, 133 is updated. then the probability of retaining 0 players from the previous year is calculated. 115, 120, 128, 133 will be written in 4 demand columns.

![image](https://github.com/0asa0/a-dynamic-programming-problem/assets/134441532/7200fb66-ab8f-40eb-92ee-e761a8f32953)

123 possibility of 2 person can be kept for next year. In four demand year 3 player can be kept. 120 possibility of 1 person can be kept for next year. In four demand year 2 player can be kept. 115 possibility of 0 person can be kept for next year. In four demand year 1 player can be kept. 115 final result with comparisons of minimum.
