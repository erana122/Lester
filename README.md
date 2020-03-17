# Reuben Ross Virtucio
# Junkyle Santerna
# Den Pither Negapatan
# Daniel Sanchez
# Lester Erana

Scheduling

import java.util.Scanner;
public class Main
{

    public Main(){
        Scanner sc = new Scanner(System.in);
        
        firstComeFirstServe sc1 = new firstComeFirstServe();
        shortestJobFirst sc2 = new shortestJobFirst();
        preEmptiveScheduling sc3 = new preEmptiveScheduling();
        RoundRobin sc4 = new RoundRobin();
        
        int input = 1;
        System.out.println("SCHEDULING");
        while(input!=5){
        System.out.println("\nPlease Select Type of Scheduling: \n1. First Come First Serve");
        System.out.println("2. Shortest Job First");
        System.out.println("3. Priority Scheduling");
        System.out.println("4. Round Robin Scheduling");
        System.out.println("5. EXIT");
        input = sc.nextInt();
        
        switch(input){
            case 1:
            sc1.Print();
            break;
            case 2:
            sc2.Print();
            break;
            case 3:
            sc3.Print();
            break;
            case 4:
            sc4.Print();
            break;
            case 5:
            break;
           }
        }
    }
}

import java.util.Scanner;
public class firstComeFirstServe
{


    public void Print(){
         Scanner scanner = new Scanner(System.in);
       
         float averageWaiting = 0;
         System.out.println("Enter Number of Processes:");
         int num = scanner.nextInt();
         int burstTime[]=new int[num];

         System.out.println("Enter Burst Time:");
         for(int x = 0; x < num; x++)
         {   
             System.out.println("Burst Time for Process"+(x+1)+":");
             burstTime[x] = scanner.nextInt();
         }
         int waitingTime[] = new int[num];
         waitingTime[0] = 0;
         for(int x =1; x < num; x++)
         {
             waitingTime[x] = burstTime[x-1] + waitingTime[x-1];
             averageWaiting+=waitingTime[x];
         }
         System.out.println("Process\t\t\tBurst time\tWaiting time");
         for(int x = 0; x < num; x++)
         {
            System.out.println("Process"+(x+1)+"\t\t"+burstTime[x]+"\t\t"+waitingTime[x]);
         }
         float awt,atat;
         System.out.println("Average Waiting time: "+averageWaiting/num);
        
    }
}



import java.util.Scanner;
public class shortestJobFirst
{
   public void Print(){
   
       Scanner scanner = new Scanner(System.in);
       int processNumber[]=new int[10];
       int burstTime[] = new int[10];
       int waitingTime[] = new int[10];
       int tempWaitingTime[] = new int[10];
       int tempProcessNumber[] = new int[12];//stores process no temporary
       int temp[]=new int[12];//represent Gantt chart
       int num, x, y, z, t, t2;
       float averageWaitingTime ,totalWaitingTime = 0;
       System.out.println("Enter Number of Processes(Less than 10): ");
       num = scanner.nextInt();
       for(x = 0; x < num; x++)
       {
           System.out.println("Enter The Burst Time of Process"+(x+1)+":");
           burstTime[x] = scanner.nextInt();
           temp[x] = burstTime[x];
           processNumber[x] = x+1;
           tempProcessNumber[x] = processNumber[x];
        }
        for(x = 0; x < num; x++)
        {
            z = 0;
            while(z <= num-x)
            {
                if(temp[z] > temp[z+1])
                {
                    t = temp[z];
                    temp[z] = temp[z+1];
                    temp[z+1] = t;
                    t2 = tempProcessNumber[z];
                    tempProcessNumber[z] = tempProcessNumber[z+1];
                    tempProcessNumber[z+1] = t2;
                }
                z++;
            }
        }   
        for(x=0; x < num; x++)
        {
            temp[x] = temp[x+2];
            tempProcessNumber[x] = tempProcessNumber[x+2];
        }
        tempWaitingTime[0] = 0;
        for(x = 1; x < num; x++)
        tempWaitingTime[x] = tempWaitingTime[x-1] + temp[x-1];
        for(x = 0; x < num; x++)
        {
            y = 0;
            while(tempProcessNumber[x] != processNumber[y] && y < num)
            y++;
            waitingTime[y] = tempWaitingTime[x];
        }
        
        
        for(x = 0; x < num; x++)
        {
            totalWaitingTime = totalWaitingTime + waitingTime[x];
        }
        averageWaitingTime = totalWaitingTime/num;
        System.out.println("Process\t\tBurst Time\tWaiting Time");
        for(x = 0; x < num; x++)
        {
            System.out.print("Process "+processNumber[x]+"\t"+burstTime[x]+"\t\t"+waitingTime[x]);
            System.out.println();
        }
        System.out.println("Average Waiting Time: " + averageWaitingTime);
    }
       
}


import java.util.*;
public class preEmptiveScheduling {
    public static void Print()
    {
    
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter Number of Process: ");
        int num = scanner.nextInt();
        
        int[][] array = new int[num][2];
        
        for(int x = 0; x < array.length; x++ )
        {
            System.out.print("Enter Burst Time for Process" + " " + (x+1) + ": ");
            array[x][0] = scanner.nextInt();
            
            System.out.print("Enter Priority Number for Process" + " " +(x+1) +": ");
            array[x][1] = scanner.nextInt();
            
           
        }
            double ave = 0;
            double count = 0;
            
            Arrays.sort(array, (a, b) -> Double.compare(a[1], b[1]));
             
            for(int y=0; y < array.length-1; y++)
            {
                
                count += array[y][0];
                ave += count;
                System.out.println("Average Waiting Time: " + ave + " ,Count: " + count);
            }
            
            ave /= num;
            System.out.print(ave);
    }    
}


import java.util.Scanner;
public class RoundRobin
{
    public void Print(){
    
        Scanner scanner = new Scanner(System.in);
        int x, y, z, quantum, sum = 0;
        System.out.println("Enter Number of Process:");
        int num = scanner.nextInt();
        int burstTime[] = new int[num];
        int waitingTime[] = new int[num];
        int totalAverageTime[] = new int[num];
        
        for(x = 0; x < num; x++)
        {
            System.out.println("Enter Burst Time For Process"+(x+1)+":");
            burstTime[x] = scanner.nextInt();
        }
        System.out.println("Enter Time Quantum:");
        quantum = scanner.nextInt();
        
        for(x = 0; x < num; x++)
        totalAverageTime[x] = burstTime[x];
        for(x = 0; x < num; x++)
        waitingTime[x] = 0;
        do
        {
            for(x = 0; x < num; x++)
            {
                if(burstTime[x] > quantum)
                {
                    burstTime[x]-=quantum;
                    for(y = 0; y < num; y++)
                    {
                        if((y!=x) && (burstTime[y] != 0))
                        waitingTime[y]+=quantum;
                    }
                }
                else
                {
                    for(y = 0; y < num; y++)
                    {
                        if((y!=x) && (burstTime[y] != 0))
                        waitingTime[y]+=burstTime[x];
                    }
                    burstTime[x] = 0;
                }
            }
            sum = 0;
            for(z = 0; z < num; z++)
            sum = sum+burstTime[z];
        }
        while(sum!=0);
        
        System.out.println("Process\t\tBurst Time\tWaiting Time");
        for(x = 0; x < num; x++)
        {
            System.out.println("Process "+(x+1)+"\t"+totalAverageTime[x]+"\t"+waitingTime[x]);
        }
        float avg_wt=0;
        for(y = 0; y < num; y++)
        {
            avg_wt+=waitingTime[y];
        }
        System.out.println("Average Waiting Time "+(avg_wt/num));
    }   
}
