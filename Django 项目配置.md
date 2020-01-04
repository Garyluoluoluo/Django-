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
	path("banner/",views.)
]
```

api/urls.py 增加路由

```python
    urlpattners = [
    	path = ("home/",include(homes.urls))
    ]
```

### 安装插件xadmin