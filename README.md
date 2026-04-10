# Answer-me

根据指定命令回复相应内容

## 使用教程

### 建议使用配置文件 

根路径 data 


文件详解 answer-me.json

使用说明：
    1.单文字回复 
        {
            "command": "我是命令词",
            "text": "我是回复词"
        }
    2.单图片回复 
        {
            "command": "我是命令词",
            "image": "./****/****.jpg"
        }
    3.图文回复 
        {
            "command": "我是命令词",
            "replyText":"我是回复词",
            "replyImages": "./****/****.jpg"
        }
    4.文件回复 
        {
            "command": "我是命令词",
            "replyFiles": ["./****/****.txt"]
        }
额外参数
    alias 别名  另外图片，别名都支持数组形式




