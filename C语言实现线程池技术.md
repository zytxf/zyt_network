# C语言实现线程池技术

![<div align=center>C语言实现线程池技术](assets/113103unlcfktpn9lqlqof-1542253374925.jpg)

**线程池(thread pool)技术**是指能够保证所创建的任一线程都处于繁忙状态，而不需要频繁地为了某一任务而创建和销毁线程，因为系统在创建和销毁线程时所耗费的cpu资源很大。如果任务很多，频率很高，为了单一一个任务而起线程而后销线程，那么这种情况效率相当低下的。线程池技术就是用于解决这样一种应用场景而应运而生的。



**线程池技术的工作原理**：在起先就创建一定数量的线程以队列形式存在，并为其分配一个工作队列，当工作队列为空时，表示没有任务，此时所有线程挂起等待新的工作到来。当新的工作到来时，线程队列头开始执行这个任务，然后依次是第二、第三个线程执行新到来的任务，当其中某个线程处理完任务后，那么该线程立马开始接受任务分派，从而让所有线程都处于忙碌的状态，提高并行处理效率。



**线程池技术是一种典型的生产者-消费者模型**。因此，无论用哪种语言实现，只要遵循其原理本身就能够很好的工作了。那么实现线程池技术我们需要考虑到哪些技术性的问题？



**C语言线程池技术的实现：**

需要考虑的技术问题一，线程池应该包含哪些成员变量。

既然要开一定数量的线程，那么这个**“一定数量(max_thread_num)”**必定是线程池的一个成员。

如何表示一个线程池是否已经关闭？如果关闭那么必需要立马释放资源。所以“**是否关闭(shutdown)”**也是一个成员。

创建线程需要有id，必需要为每个线程准备一个id，所以需要一个id数组，其长度就是max_thread_num。

线程锁，用以保证对线程操作时的互斥性。所以需要一个锁,queue_lock。

条件变量(condition_variable)，这里使用条件变量主要是为了广播任务到来的消息给所有线程。当有处于空闲的线程，则由此线程

接受任务分派。所以需要一个条件变量queue_ready。

最为重要的就是任务本身，也就是工作。那么工作本身又需要哪几个成员变量？首先肯定是任务入口，routine函数；

其次是routine函数的参数args；再次任务是以队列存在着的，所以任务本身应该包含一个next。



需要考虑的技术问题二，线程池应该包含哪些api。

一、创建线程池，create_tpool

二、销毁线程池，destroy_tpool

三、分派任务，add_task_2_tpool



基于上述分析，我们可以先构造头文件。

tpool.h

```c
#ifndef T_POOL
#define T_POOL
 
#include <pthread.h>
#include <ctype.h>
 
typedef struct tpool_work
{
   void* (*work_routine)(void*); //function to be called
   void* args;                   //arguments 
   struct tool_work* next;
}tpool_work_t;
 
typedef struct tpool
{
   size_t               shutdown;     //is tpool shutdown or not, 1 ---> yes; 0 ---> no
   size_t               maxnum_thread; // maximum of threads
   pthread_t            *thread_id;     // a array of threads
   tpool_work_t*        tpool_head;     // tpool_work queue
   pthread_cond_t       queue_ready;    // condition varaible
   pthread_mutex_t      queue_lock;     // queue lock
}tpool_t;
 
 
/***************************************************
*@brief:
*       create thread pool
*@args:   
*       max_thread_num ---> maximum of threads
*       pool           ---> address of thread pool
*@return value: 
*       0       ---> create thread pool successfully
*       othres  ---> create thread pool failed
***************************************************/
 
int create_tpool(tpool_t** pool,size_t max_thread_num);
 
/***************************************************
*@brief:
*       destroy thread pool
*@args:
*        pool  --->  address of pool
***************************************************/
void destroy_tpool(tpool_t* pool);
 
/**************************************************
*@brief:
*       add tasks to thread pool
*@args:
*       pool     ---> thread pool
*       routine  ---> entry function of each thread
*       args     ---> arguments
*@return value:
*       0        ---> add ok
*       others   ---> add failed        
**************************************************/
int add_task_2_tpool(tpool_t* pool,void* (*routine)(void*),void* args);
 
#endif//tpool.h
```

需要考虑的技术问题三，线程池的所有权应该交予谁。

这里我们需要考虑到，将线程池封装成一个so库是比较好的想法，那么，线程池的所有权就应该交予调用它的函数。所以我这里采取的就是这个方法。

tpool.c

```c
#include "tpool.h"
#include <unistd.h>
#include <errno.h>
#include <string.h>
#include <stdlib.h>
#include <stdio.h>
 
 
static void* work_routine(void* args)
{
   tpool_t* pool = (tpool_t*)args;
   tpool_work_t* work = NULL;
 
   while(1)
   {
        pthread_mutex_lock(&pool->queue_lock);
        while(!pool->tpool_head && !pool->shutdown)
        { 
            // if there is no works and pool is not shutdown, it should be suspended for being awake
            pthread_cond_wait(&pool->queue_ready,&pool->queue_lock);
        }
 
        if(pool->shutdown)
        {
           pthread_mutex_unlock(&pool->queue_lock);//pool shutdown,release the mutex and exit
           pthread_exit(NULL);
        }
 
        /* tweak a work*/
        work = pool->tpool_head;
        pool->tpool_head = (tpool_work_t*)pool->tpool_head->next;
        pthread_mutex_unlock(&pool->queue_lock);
 
        work->work_routine(work->args);
 
        free(work);
   }
	
   return NULL;
}
 
int create_tpool(tpool_t** pool,size_t max_thread_num)
{
   (*pool) = (tpool_t*)malloc(sizeof(tpool_t));
   if(NULL == *pool)
   {
        printf("in %s,malloc tpool_t failed!,errno = %d,explain:%s\n",__func__,errno,strerror(errno));
        exit(-1);
   }
   (*pool)->shutdown = 0;
   (*pool)->maxnum_thread = max_thread_num;
   (*pool)->thread_id = (pthread_t*)malloc(sizeof(pthread_t)*max_thread_num);
   if((*pool)->thread_id == NULL)
   {
        printf("in %s,init thread id failed,errno = %d,explain:%s",__func__,errno,strerror(errno));
        exit(-1);
   }
   (*pool)->tpool_head = NULL;
   if(pthread_mutex_init(&((*pool)->queue_lock),NULL) != 0)
   {
        printf("in %s,initial mutex failed,errno = %d,explain:%s",__func__,errno,strerror(errno));
        exit(-1);
   }
 
   if(pthread_cond_init(&((*pool)->queue_ready),NULL) != 0)
   {
        printf("in %s,initial condition variable failed,errno = %d,explain:%s",__func__,errno,strerror(errno));
        exit(-1);
   }
 
   for(int i = 0; i < max_thread_num; i++)
   {
        if(pthread_create(&((*pool)->thread_id[i]),NULL,work_routine,(void*)(*pool)) != 0)
        {
           printf("pthread_create failed!\n");
           exit(-1);
        }
   }
   
   return 0;
}
 
void destroy_tpool(tpool_t* pool)
{
   tpool_work_t* tmp_work;
 
   if(pool->shutdown)
   {
        return;
   }
   pool->shutdown = 1;
 
   pthread_mutex_lock(&pool->queue_lock);
   pthread_cond_broadcast(&pool->queue_ready);
   pthread_mutex_unlock(&pool->queue_lock);
 
   for(int i = 0; i < pool->maxnum_thread; i++)
   {
        pthread_join(pool->thread_id[i],NULL);
   }
   free(pool->thread_id);
   while(pool->tpool_head)
   {
        tmp_work = pool->tpool_head;
        pool->tpool_head = (tpool_work_t*)pool->tpool_head->next;
        free(tmp_work);
   }
 
   pthread_mutex_destroy(&pool->queue_lock);
   pthread_cond_destroy(&pool->queue_ready);
   free(pool);
}
 
int add_task_2_tpool(tpool_t* pool,void* (*routine)(void*),void* args)
{
   tpool_work_t* work,*member;
 
   if(!routine)
   {
        printf("rontine is null!\n");
        return -1;
   }
 
   work = (tpool_work_t*)malloc(sizeof(tpool_work_t));
   if(!work)
   {
        printf("in %s,malloc work error!,errno =        %d,explain:%s\n",__func__,errno,strerror(errno));
        return -1;
   }
 
   work->work_routine = routine;
   work->args = args;
   work->next = NULL;
 
   pthread_mutex_lock(&pool->queue_lock);
   member = pool->tpool_head;
   if(!member)
   {
        pool->tpool_head = work;
   }
   else
   {
        while(member->next)
        {
           member = (tpool_work_t*)member->next;
        }
        member->next = work;
   }
 
   //notify the pool that new task arrived!
   pthread_cond_signal(&pool->queue_ready);
   pthread_mutex_unlock(&pool->queue_lock);
   
   return 0;
}
```

demo.c

```c
#include "tpool.h"
#include <stdio.h>
#include <unistd.h>
#include <time.h>
 
void* fun(void* args)
{
   	int thread = (int)args;
   	printf("running the thread of %d\n",thread);
	return NULL;
}
 
int main(int argc, char* args[])
{
   tpool_t* pool = NULL;
   if(0 != create_tpool(&pool,5))
   {
        printf("create_tpool failed!\n");
        return -1;
   }
 
   for(int i = 0; i < 1000; i++)
   {
        add_task_2_tpool(pool,fun,(void*)i);
   }
   sleep(2);
   destroy_tpool(pool);
   return 0;
}
```

Makefile

```kconfig
pool: tpool.c demo.c
        gcc tpool.c demo.c -o pool -lpthread -std=c99 
 
clean:
        rm ./pool
```




