今年7月18日Facebook把llama2开放开源，对微软openai造成了很大的威胁，为了应对此威胁：

# 8月23日，GPT-3.5 Turbo 的微调推出，GPT-4 的微调将于今年秋天推出。
此更新使开发人员能够自定义更适合其用例的模型。早期测试表明，GPT-3.5 Turbo 的微调版本在某些狭窄任务上可以匹配甚至超越GPT-4 级别的功能。与我们所有的 API 一样，传入和传出微调 API 的数据归客户所有， OpenAI或任何其他组织不会使用该数据来训练其他模型。

## 微调用例的意义？
### 改进的可操纵性
	例如，开发人员可以使用微调来确保模型在提示使用德语时始终以德语进行响应。
### 可靠的输出格式
	开发人员可以使用微调来更可靠地将用户提示转换为可在自己的系统中使用的高质量 JSON 片段。
### 自定义音调
	拥有知名品牌声音的企业可以对模型进行微调，使其与其基调更加一致。

## 微调步骤
### 准备您的数据
```
{
  "messages": [
    { "role": "system", "content": "You are an assistant that occasionally misspells words" },
    { "role": "user", "content": "Tell me a story." },
    { "role": "assistant", "content": "One day a student went to schoool." }
  ]
}
```
### 上传文件
```
curl https://api.openai.com/v1/files \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F "purpose=fine-tune" \
  -F "file=@path_to_your_file" 
```
### 创建微调作业
```
curl https://api.openai.com/v1/fine_tuning/jobs \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-d '{
  "training_file": "TRAINING_FILE_ID",
  "model": "gpt-3.5-turbo-0613"
}'
```

## 安全
微调的部署是否安全对我们来说非常重要。为了通过微调过程保留默认模型的安全功能，微调训练数据通过我们的审核 API 和 GPT-4 支持的审核系统传递，以检测与我们的安全标准相冲突的不安全训练数据。

首先小科普：什是token？
“You can think of tokens as pieces of words, where 1,000 tokens is about 750 words”
## 价钱
微调成本分为两部分：初始训练成本和使用成本：
培训：0.008 美元/1K token
使用输入：0.012 美元/1K token
使用输出：0.016 美元/1K token
例如，一个gpt-3.5-turbo包含 100,000 个token的训练文件并训练 3 个 epoch 的微调作业的预期成本为 2.40 美元。


2023 年 8 月 22 日
作者：彭安德 迈克尔·吴 约翰·阿拉德 洛根·基尔帕特里克 史蒂文·海德尔
