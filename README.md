
#include<stdio.h>
int main()
{   
    int at[10],at2[10],bt[100],ex[100],seq[100],re[100],wt[100],tat[100];
    int n,i,j,start,pos,max=0,min,idle=0,k=0;
    float av1=0,av2=0;

    printf("INPUT\n");
    printf("Enter number of process\n");
    scanf("%d",&n);
    printf("Enter arrival time for processess\n");
    for(i=0;i<n;i++)
    {
     scanf("%d",&at[i]);
     at2[i]=at[i];
    }
    printf("Enter burst time for processess\n");
    for(i=0;i<n;i++)
    {
     scanf("%d",&bt[i]);
    }
    start=at[0];
    for(i=1;i<n;i++)
    {
      if(start>at[i])
       {
       start=at[i];
       }
     }
    printf("OUTPUT\n");
    printf("Sequence of execution is\n");
    for(i=0;i<n;i++)
    {
    if(max<at[i])
     {
      max=at[i];
     }
    }
    max=max+1;
   for(i=0;i<n;i++,k++)
     {  min=max;
       for(j=0;j<n;j++){  
           if(at[j]!=-1)
             {
               if(at[j]<min)
                 {
                  min=at[j];
                  pos=j;
                 }
              }
         }
      printf("[P%d]  ",pos);
      seq[k]=pos;
      if(start<at[pos]){
         re[pos]=start;
         idle+=at[pos]-start;
         start=at[pos];
         start+=bt[pos];
         at[pos]=-1;
         ex[pos]=start;
      }
      else{
        re[pos]=start;
        start+=bt[pos];
        at[pos]=-1;
        ex[pos]=start;
       }
     }
    printf("\n");
    for(i=0;i<n;i++)
    {
       tat[i]=ex[i]-at2[i];
      
       wt[i]=tat[i]-bt[i];
    }
 printf("Process  AT    BT      CT       WT   TAT \n");
   for(i=0;i<n;i++)
    {
      printf("P%d        %d      %d      %d      %d     %d\n",i,at2[i],bt[i],ex[i],wt[i],tat[i]);
    }
   for(i=0;i<n;i++)
   {
    av1+=tat[i];
    av2+=wt[i];
   }
  printf("Average waiting time(s) %f\nAverage turnaroundtime(s) %f\nCPU idle time(s)%d\n",av2/n,av1/n,idle);
}





#include<stdio.h>
int main()
{
int i,n,p[10]={1,2,3,4,5,6,7,8,9,10},min,k=1,btime=0;
int bt[10],temp,j,at[10],wt[10],tt[10],ta=0,sum=0;
float wavg=0,tavg=0,tsum=0,wsum=0;
printf(" -------Shortest Job First Scheduling ( NP )-------\n");
printf("\nEnter the No. of processes :");
scanf("%d",&n);
 
for(i=0;i<n;i++)
{
printf("\tEnter the burst time of %d process :",i+1);
scanf(" %d",&bt[i]);
printf("\tEnter the arrival time of %d process :",i+1);
scanf(" %d",&at[i]);
}
 
//Sorting According to Arrival Time/
 
for(i=0;i<n;i++)
{
for(j=0;j<n;j++)
{
if(at[i]<at[j])
{
temp=p[j];
p[j]=p[i];
p[i]=temp;
temp=at[j];
at[j]=at[i];
at[i]=temp;
temp=bt[j];
bt[j]=bt[i];
bt[i]=temp;
}
}
}
 
/*Arranging the table according to Burst time,
Execution time and Arrival Time
Arrival time <= Execution time
*/
 
for(j=0;j<n;j++)
{
btime=btime+bt[j];
min=bt[k];
for(i=k;i<n;i++)
{
if (btime>=at[i] && bt[i]<min)
{
temp=p[k];
p[k]=p[i];
p[i]=temp;
temp=at[k];
at[k]=at[i];
at[i]=temp;
temp=bt[k];
bt[k]=bt[i];
bt[i]=temp;
}
}
k++;
}
wt[0]=0;
for(i=1;i<n;i++)
{
sum=sum+bt[i-1];
wt[i]=sum-at[i];
wsum=wsum+wt[i];
}
 
wavg=(wsum/n);
for(i=0;i<n;i++)
{
ta=ta+bt[i];
tt[i]=ta-at[i];
tsum=tsum+tt[i];
}
 
tavg=(tsum/n);
 
printf("");
printf("\n RESULT:-");
printf("\nProcess\t Burst\t Arrival\t Waiting\t Turn-around\t Completion" );
for(i=0;i<n;i++)
{
    int completion_time = at[i] + tt[i];
printf("\n p%d\t %d\t %d\t\t %d\t\t\t%d\t\t\t%d",p[i],bt[i],at[i],wt[i],tt[i],completion_time);
}
 
printf("\n\nAVERAGE WAITING TIME : %f",wavg);
printf("\nAVERAGE TURN AROUND TIME : %f",tavg);
return 0;
}
