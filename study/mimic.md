mimic数据集介绍 [1](https://blog.csdn.net/qq_43787862/article/details/105028846?ops_request_misc=&request_id=&biz_id=102&utm_term=mimiciii%E6%95%B0%E6%8D%AE%E5%BA%93%E4%BB%8B%E7%BB%8D&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-5-105028846.142^v88^control,239^v2^insert_chatgpt&spm=1018.2226.3001.4187)  [2](https://blog.csdn.net/weixin_44285445/article/details/109355391?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168853445616782427413893%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168853445616782427413893&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-109355391-null-null.142^v88^control,239^v2^insert_chatgpt&utm_term=mimiciii%E6%95%B0%E6%8D%AE%E5%BA%93%E4%BB%8B%E7%BB%8D&spm=1018.2226.3001.4187)   [代码](https://github.com/linzhenyuyuchen/kddMIMIC)   sql[操作汇总](https://blog.csdn.net/m0_71741835/article/details/127624612?ops_request_misc=&request_id=&biz_id=102&utm_term=sql%E5%A4%84%E7%90%86%E8%AF%AD%E5%8F%A5&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-127624612.142^v88^control,239^v2^insert_chatgpt&spm=1018.2226.3001.4187)

```sql
#1提取患者住院号和病案号列表
SELECT subject_id,hadm_id
FROM admissions;
#2从入院列表一共有多少入院类型
select distinct admission_type
from admissions;
#3提取院内死亡的病人
select subject_id,hadm_id
from admissions
where ospital_expire_flag = 1;
#提取院内死亡的病人并且入院途径为急症的病人信息
select subject_id,hadm_id
from admissions
where ospital_expire_flag = 1 
and admission_type = 'EMERGENCY';
#提取入院途径为急症或择期的病人信息
SELECT subject_id,hadm_id
FROM admissions
WHERE admission_type IN ('EMERGENCY',ELECTIVE);
#提取在ICU期间住院天数为1~3天的病人信息
select subject_id,hadm_id,icustay_id
from icustays
WHERE los BETWEEN 1 AND 3;
#提取血清白细胞的项目标志符

```

![image-20230706131211741](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061313986.png)

![image-20230706131430311](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061314403.png)

![image-20230706131600338](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061316472.png)

![image-20230706131631129](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061316243.png)

![image-20230706131646066](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061316245.png)

![image-20230706131719418](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061317508.png)

![image-20230706131739511](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061317619.png)

![image-20230706131813000](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061318115.png)

![image-20230706131831149](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061318261.png)

![image-20230706131902925](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061319064.png)

![image-20230706132001032](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061320153.png)

![image-20230706132100877](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061321023.png)

![image-20230706132140162](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061321250.png)

![image-20230706132250183](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061322292.png)

![image-20230706132309229](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061323333.png)

![image-20230706132742105](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061327257.png)

![image-20230706132849497](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061328626.png)

![image-20230706133039726](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061330846.png)

![image-20230706133111756](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202307061331913.png)
