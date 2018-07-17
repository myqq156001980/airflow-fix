# airflow-fix

# 修改airflow scheduler 触发逻辑
>  默认的触发逻辑为,根据已有的start_date, 进行出发,如果没有配置catchup=False (在airflow.cfg中配置),其会执行从开始日期到现在满足条件的所有任务.但是
配置了catchup=False 后其会执行所配置interval 前一个周日的任务,后续的任务都是根据前一个任务进行推算执行的.每次执行的任务日期都活落后一个周期.这里修改为正常
的逻辑


### version 1.8.0
