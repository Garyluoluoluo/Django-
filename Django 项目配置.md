# Django 项目配置

### 项目结构设计

### 数据库设置

### 日志设置

### 异常处理设置

### 独立域名运行及跨域设置

### 项目和导包设置

```python
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
sys.path.insert(0,os.path.join(BASE_DIR,"apps"))
```

### 创建分支

创建开发分支完成，创建分支

```
#创建分支
git branch 分支

#切换分支
git checkout 分支

#删除分支
git branch -d 分支

#查看分支
git branch
```

### 创建数据模型

apps/home/models.py

```python
class BaseModel(models.Model):
	"""公共模型"""
	...
	...
	class Meta:
		#抽象模型，设置abstract为True时，Django不会创建数据库表
		abstract=True
```

创建模型文件类

数据迁移

```
python manage.py makemigrations
python manage.py migrate
```

### 创建序列化器

模型序序列化

```python
class BannerModelSerializer(Serializers.ModelSerializer):
	class Meta:
		model = banner
		fields = ['image','link']	
```



### 创建视图

试图列表：

```python
from rest_framework.generics import ListAPIView

class BannerListAPIView(ListAPIView):
    
```

### 模型查询

查询指定条件数据

```python
from rest_framework.generics import ListAPIView

class BannerListAPIView(ListAPIView):
    
    queryset = banner.objects.filter(is_show = True, is_delete=False).order_by("-orders")[:7]#切片查询结果
```

序列化查询数据

```python
from rest_framework.generics import ListAPIView

class BannerListAPIView(ListAPIView):
    
    queryset = banner.objects.filter(is_show = True, is_delete=False).order_by("-orders").limit(7)	
    serializer_class = BannerModelSerializer
```

### 增加路由

apps/urls.py 增加

```python
urlpattners =[
	path("banner/",views.BannerListView.as_view())
]
```

api/urls.py 增加路由

```python
    urlpattners = [
    	path = ("home/",include(homes.urls))
    ]
```

### 安装插件xadmin





## 用户登录模型

​	权限机制：

​					1.Role-base-access[基于角色的权限认证] RBAC

​					2.Auth[授权认证机制]

​	Django 内部集成了Auth模块。

​	RBAC权限机制，一般有2种不同的设计方式

​	3表RBAC

​		用户【user】：id/ username / role_id

​       角色【role】：id / role_name/auth_list

​		权限【Auth】：id/ auth_name/

​	5表RBAC

​				用户【user】：id/ username/

​       		角色【role】：id / role_name

​				权限【Auth】：id/ auth_name

​				用户角色关系表：id/uid/rid

​				角色权限关系表：id/rid/aid