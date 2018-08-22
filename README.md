# airflow-fix

# 修改airflow scheduler 触发逻辑
>  默认的触发逻辑为,根据已有的start_date, 进行出发,如果没有配置catchup=False (在airflow.cfg中配置),其会执行从开始日期到现在满足条件的所有任务.但是
配置了catchup=False 后其会执行所配置interval 前一个周日的任务,后续的任务都是根据前一个任务进行推算执行的.每次执行的任务日期都活落后一个周期.这里修改为正常
的逻辑


# 使用scheduler(坑)
> scheduler启动任务后会有两个进程, 
```
work     24014  5558  0 13:02 ?        00:01:13 /home/work/software/python3/bin/python3.6 /home/work/software/python3/bin/airflow run spider_365House group_rentplat_365_nanjing 2018-08-22T06:00:00 --local -sd /home/work/airflow/dags/spider_365House.py
work     24023 24014  0 13:02 ?        00:00:01 /home/work/software/python3/bin/python3.6 /home/work/software/python3/bin/airflow run spider_365House group_rentplat_365_nanjing 2018-08-22T06:00:00 --job_id 1170 --raw -sd DAGS_FOLD

```

> 当出现异常 24014 进程退出后会 24023 job进程会托管到系统进程1 下面继续运行. 这是需要注意的地方


### version 1.8.0
