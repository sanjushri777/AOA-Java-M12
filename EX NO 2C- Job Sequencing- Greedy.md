
# EX 2C Job Sequencing using Greedy Approach
## DATE: 14.3.26
## AIM:
To write a Java program to for given constraints.
Given an integer array nums and an integer k, return the number of pairs (i, j) where i < j such that |nums[i] - nums[j]| == k.

The value of |x| is defined as:

x if x >= 0.
-x if x < 0.You're given N jobs, each with:

A unique jobId

A deadline (by which it must be completed)

A profit (earned only if completed on or before the deadline)

Each job:

Takes exactly 1 unit of time

Only one job can be done at a time

Your goal is to maximize total profit while completing the maximum number of jobs possible within their deadlines.

## Algorithm
1. Sort all jobs in decreasing order of profit.

2. Find the maximum deadline among all jobs to determine the number of time slots needed.

3. Create a boolean array slot[] of size maxDeadline + 1 to track free time slots.

4. Initialize count = 0 (jobs done) and totalProfit = 0.

5. For each job in sorted order, try to assign it to the latest free slot before its deadline. if a free slot is found, mark it, increase count, and add the job’s
   profit.

6. After processing all jobs, return {count, totalProfit}.

## Program:
```
import java.util.*;

public class JobScheduling {

    static class Job {
        int id, deadline, profit;
        Job(int id, int deadline, int profit) {
            this.id = id;
            this.deadline = deadline;
            this.profit = profit;
        }
    }

    public static int[] jobScheduling(Job[] jobs, int n) {
        Arrays.sort(jobs, (a, b) -> b.profit - a.profit);

        int maxDeadline = 0;
        for (Job job : jobs) maxDeadline = Math.max(maxDeadline, job.deadline);

        boolean[] slot = new boolean[maxDeadline + 1];
        int count = 0, totalProfit = 0;

        for (Job job : jobs) {
            for (int j = job.deadline; j > 0; j--) {
                if (!slot[j]) {
                    slot[j] = true;
                    count++;
                    totalProfit += job.profit;
                    break;
                }
            }
        }

        return new int[]{count, totalProfit};
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Job[] jobs = new Job[n];

        for (int i = 0; i < n; i++) {
            int id = sc.nextInt();
            int deadline = sc.nextInt();
            int profit = sc.nextInt();
            jobs[i] = new Job(id, deadline, profit);
        }

        int[] result = jobScheduling(jobs, n);
        System.out.println(result[0] + " " + result[1]);
    }
}
```

## Output:

<img width="365" height="501" alt="image" src="https://github.com/user-attachments/assets/8d4d8525-ad30-4bcb-8e04-a582c6240662" />


## Result:
The program successfully implemented and the expected output is verified.
