# 算法展示项目





## API设置

1. start algo:开始算法

```json
Requst:
POST /api/algo   
{
  'game':,
  'algo':,
  'parameter':{
  
	},
}

Response:
200
```

2. end algo: 终止算法

   ```json
   Request:
   DELETE /api/algo 
   
   Response: 
   200
   {
     'score':
     'coststeps':
     ...
   }
   ```

3. get best parameter ：获取最优参数

   ```json
   Request:
   GET /api/best_param
   
   Response:
   200 
   {
     'link':...,
   }
   ```

4. 获取每个个体的下一张图片

   ```json
   Request:
   GET /api/photo/个体id
   
   Response:
   200
   {
   	'link':...,
   }
   ```

5. 获取最优个体仿真的下一张图片

   ```json
   Request:
   GET /api/best_simulation/photo
   
   Response:
   200
   {
   	'link':...,
   }
   ```

6. reload最优参数

   ```json
   Request:
   POST /api/best_simulation/reload
   
   Response:
   200
   ```

7. 获取算法运行过程中的数据

   ```json
   Request:
   GET /api/algo/state
   
   Response:
   200
   {
   	"score": ,
     "timestep": ,
   }
   ```

   

注意：

4，5，7这三个API的Response中状态码等于200表示结果返回正常，等于404表示没有新的数据。



