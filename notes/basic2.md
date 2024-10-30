## 书生大模型实战营第4期 - 入门关卡第2关

### 关卡名称
Python 基础知识

### 关卡任务
1.Leetcode 383
2. Vscode连接InternStudio debug笔记

### 作业
1. Leetcode 383
    ![](https://pic2.zhimg.com/80/v2-aa29ce66191e8bd22b740239fc157b83_1440w.webp)
    ![](https://pic3.zhimg.com/80/v2-4550dd630bc71ab5dc2015f0bce30b18_1440w.webp)

2. Vscode连接InternStudio debug
  * 定位错误位置：
  ![](https://picx.zhimg.com/80/v2-009812b055050a08b068c904034313d9_1440w.webp)

  * 打断点到对应行数的代码
  ![](https://pic4.zhimg.com/80/v2-1333a8a51d4765e5e117524f2237a5f5_1440w.webp)
  调试时发现相应结果并不是一个标准的json字符串，看起来像是markdown格式的字符串，并且带有换行符。

  * 对相应结果进行处理
  ![](https://pic3.zhimg.com/80/v2-3e858a3234fb7ddf09397e2fec5cb8ac_1440w.webp)

  * 运行结果
  ![](https://pic4.zhimg.com/80/v2-903f0f1c4e0d0e59a8361ad745a5406f_1440w.webp)

  * 完整代码
  ```python
  import json

from openai import OpenAI


def internlm_gen(prompt, client):
    """
    LLM生成函数
    Param prompt: prompt string
    Param client: OpenAI client
    """
    response = client.chat.completions.create(
        model="internlm2.5-latest",
        messages=[
            {"role": "user", "content": prompt},
        ],
        stream=False,
    )
    return response.choices[0].message.content


api_key = "eyJ0eXBlIjoiSldUIiwiYWxnIjoiSFM1MTIifQ.eyJqdGkiOiI1MDE3NDIyMCIsInJvbCI6IlJPTEVfUkVHSVNURVIiLCJpc3MiOiJPcGVuWExhYiIsImlhdCI6MTczMDI1OTAwMiwiY2xpZW50SWQiOiJlYm1ydm9kNnlvMG5semFlazF5cCIsInBob25lIjoiMTM1NTg4NjE1NDYiLCJ1dWlkIjoiZTMwMTI0ZDItZDMwYi00MWMxLWFhMjEtZDM4MzliNWUyMzNkIiwiZW1haWwiOiIiLCJleHAiOjE3NDU4MTEwMDJ9.qw0hEV-FvOr-TGR5a0qfyGdxZl42GM-6kHxjLPNibTn6oAmwWIP4PDmHW2GN80pYBQEFQwh8nNBhQ7viE149Ow"
client = OpenAI(
    base_url="https://internlm-chat.intern-ai.org.cn/puyu/api/v1/", api_key=api_key
)

content = """
书生浦语InternLM2.5是上海人工智能实验室于2024年7月推出的新一代大语言模型，提供1.8B、7B和20B三种参数版本，以适应不同需求。
该模型在复杂场景下的推理能力得到全面增强，支持1M超长上下文，能自主进行互联网搜索并整合信息。
"""
prompt = f"""
请帮我从以下``内的这段模型介绍文字中提取关于该模型的信息，要求包含模型名字、开发机构、提供参数版本、上下文长度四个内容，以json格式返回。
`{content}`
"""
res = internlm_gen(prompt, client)
res_json = json.loads(res.strip("```json\n").strip("\n```"))
print(res_json)
  ```

