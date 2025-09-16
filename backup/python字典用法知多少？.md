## 1. 字典存储任意可调用对象（Callable）
可以混合存储各种 Callable
比如：

| 名称         | 举例代码                                                                                                                                                                                                                        |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 类          | class SMSNotifier:<br>    def `__init__`(self, number, message):<br>        self.number = number<br>        self.message = message<br>    def send(self):<br>        print(f"Sending SMS to {self.number}: {self.message}") |
| `__call__` | class PushNotification:<br>    def `__call__`(self, user_id, content):<br>        print(f"Sending push to user {user_id}: {content}")                                                                                       |
| Lambda 表达式 | log_to_file = lambda message: print(f"Logging to file: {message}")                                                                                                                                                          |
| 普通函数       | def send_email(to, subject, body):<br>    print(f"Sending email to {to} with subject '{subject}'")                                                                                                                          |
对以上创建字典
```python
notifiers = {
    'email': send_email,          # 函数
    'sms': SMSNotifier,           # 类
    'push': PushNotification(),   # 可调用实例
    'log': log_to_file,           # Lambda
    'alert': lambda msg: print(f"🚨 ALERT: {msg}") # 内联 Lambda
}
```
然后用函数导出
```python
def notify(method, *args, **kwargs):
    notifier = notifiers[method]
    return notifier(*args, **kwargs)
    
notify('email', 'user@example.com', 'Hello', 'This is a test')
notify('sms', '+1234567890', 'Hi there!') 
notify('push', 'user_123', 'You have a new message!')
notify('log', 'System started')
notify('alert', 'CPU usage high!')
```

实际运用1：在游戏设计技能当中，可以利用字典嵌套和函数将文字说明和效果实现绑定，
- 函数也能“存起来”：不像数字或字符串，函数（包括 lambda）是可以“保存”和“传递”的对象。你可以把它们存在字典、列表，甚至作为参数传给其他函数。
- 动态调用：通过字典键取出 lambda 函数并调用，感觉像“按需加载技能”，非常适合游戏开发这种需要动态效果的场景。

比如
```python
RUNES = {  
    'cooldown_reduction': {  
        'name': 'Cooldown Reduction',  
        'description': 'Reduces laser cooldown by 20%.',  
        'apply': lambda player: setattr(player, 'cooldown_duration', player.cooldown_duration * 0.8)  
    },  
    'eureka': {  
        'name': 'Eureka',  
        'description': 'Each meteor destroyed reduces cooldown by 10ms (no limit).',  
        'apply': lambda player: setattr(player, 'eureka_active', True)  
    },  
    'dive_bomb': {  
        'name': 'Dive Bomb',  
        'description': 'Press Q to destroy all meteors (60s cooldown).',  
        'apply': lambda player: setattr(player, 'dive_bomb_active', True)  
    },  
    'star_shield': {  
        'name': 'Star Shield',  
        'description': 'Grants a shield that blocks one collision (30s cooldown).',  
        'apply': lambda player: setattr(player, 'shield_active', True)  
    },  
    'comet_burst': {  
        'name': 'Comet Burst',  
        'description': 'Lasers move faster and can hit up to 3 meteors.',  
        'apply': lambda player: setattr(player, 'comet_burst_active', True)  
    }  
}
```

实际运用2：可以自己用字典写个简单计算器：
```python
operation = {'add' : lambda x,y : x + y,  
             'sub' : lambda x,y : x - y,  
             'mul' : lambda x,y : x * y,  
                'div' : lambda x,y : x / y if y != 0 else print("Error: Division by zero")}  
print(operation['add'](10,5))  
print(operation['sub'](10,5))  
print(operation['mul'](10,5))  
print(int(operation['div'](10,5)))  
print(operation['div'](10,0))
```

 ---


## 2.字典存储嵌套配置（类似 JSON）
字典可以更复杂，像 JSON 一样存储多层配置



 ---



## 3.字典推导式（Dictionary Comprehension）

用法和列表推导式相似，不多赘述

```python
# 将一个列表的元素映射为其平方
numbers = [1, 2, 3, 4, 5]
squared_dict = {x: x**2 for x in numbers}
print(squared_dict) # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# 交换一个字典的键和值 (前提是值都是可哈希的，才能作为新键)
original_dict = {'a': 1, 'b': 2, 'c': 3}
reversed_dict = {v: k for k, v in original_dict.items()}
print(reversed_dict) # {1: 'a', 2: 'b', 3: 'c'}

# 带有条件判断的推导式
even_squares = {x: x**2 for x in numbers if x % 2 == 0}
print(even_squares) # {2: 4, 4: 16}
```


 ---



## 4.特殊字典`defaultdict`

defaultdict能够访问不存在的值。
倘若是普通字典，则会弹出KeyError，
而 defaultdict 会自动为这个键生成一个默认值，避免错误。


需要
```python
```python
from collections import defaultdict
d = defaultdict(factory)
```
创建


比如：
##### 按首字母分组
```python
```python
from collections import defaultdict
words = ['apple', 'bat', 'bar', 'atom', 'book']
grouped_by_first_letter = defaultdict(list)  # 默认值是空列表 []

for word in words:
    key = word[0]
    grouped_by_first_letter[key].append(word)  # 无需判断 key 是否存在！

print(dict(grouped_by_first_letter))
# 输出: {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}
```
- 初始化：defaultdict(list) 意味着如果访问一个不存在的键，defaultdict 会自动创建一个空列表 [] 作为值。
- 循环过程：
    - 第一个单词 apple，key = 'a'：
        - grouped_by_first_letter['a'] 不存在，defaultdict 自动创建 grouped_by_first_letter['a'] = []。
        - 然后执行 .append('apple')，结果是 {'a': ['apple']}。  
            然后执行 .append（'apple'），结果是 {'a'： ['apple']}。
    - 第二个单词 bat，key = 'b'：
        - grouped_by_first_letter['b'] 不存在，自动创建 grouped_by_first_letter['b'] = []。
        - 然后 .append('bat')，结果是 {'a': ['apple'], 'b': ['bat']}。
    - 第三个单词 bar，key = 'b'：
        - grouped_by_first_letter['b'] 已存在（值为 ['bat']），直接 .append('bar')，变成 ['bat', 'bar']。  
            grouped_by_first_letter['b'] 已存在（值为 ['bat']），直接 .append（'bar'），变成 ['bat'， 'bar']。
    - 依此类推，最终得到 {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}。  
        依此类推，最终得到 {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}。


对比普通代码，普通代码需要多执行一步判断：

```python
grouped = {}
for word in words:
    key = word[0]
    if key not in grouped:
        grouped[key] = []  # 初始化空列表
    grouped[key].append(word)
```

