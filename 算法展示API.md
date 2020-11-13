# 算法展示项目





## API设置

1. start algo:开始算法

```json
Requst:
POST /api/algo   
{
    "game":"Alien",
    "algo":"NCSCC",
    "parameter":{
    	"k":7
    }
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
   ```

3. get best parameter ：获取最优参数

   ```json
   Request:
   GET /api/best_param
   
   Response:
   200
   用这个链接就可以进行文件下载
   ```
   
4. 获取每个个体的下一张图片

   ```json
   Request:
   GET /api/photo/个体id
   
   Response:
   200
   {
   	"link":...,
   }
   ```

5. 获取最优个体仿真的下一张图片

   ```json
   Request:
   GET /api/best_simulation/photo
   
   Response:
   200
   {
   	"link":...,
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

   
   
   8.查看算法运行状态：
   
   ```
   Request:
   GET /api/check
   
   Response:
   200
   {	
       "g_time": 
       "itemstatus": 
       "runninggame": 
   }
   ```
   
   

注意：

4，5，7这三个API的Response中状态码等于200表示结果返回正常，等于404表示没有新的数据。

第8个api 参数说明：

 g_time：如果有游戏在运行表示已经运行的时间，如没有游戏运行则打印当前时间

itemstatus：有游戏在运行 为 1 ，没游戏运行为0

runninggame：打印当前正在运行的游戏的名字 ，如没有游戏打印 not game





