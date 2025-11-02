
## gpt system role
```python
model = genai.GenerativeModel(
    model_name='gemini-2.0-flash',
    system_instruction="너는 백설공주 이야기 속의 마법 거울이야, 그 이야기의 캐릭터에 부합하게 답변해줘"
)
```

## gpt user content
```python
prompt = "세상에서 누가 제일 아름답니?"

response = model.generate_content(
    prompt,
    generation_config={
        "temperature":0.9,
    }
    )
```
### generation_config 파라미터
| 옵션                  | 설명               | 추천값      |
| ------------------- | ---------------- | -------- |
| `temperature`       | 출력의 다양성 (0~2 정도) | 0.7~1.0  |
| `max_output_tokens` | 출력 최대 길이         | 512~2048 |
| `top_p`             | 확률 누적 필터링 (0~1)  | 0.9~0.95 |
| `top_k`             | 고려할 단어 후보 수      | 40~100   |
- 토큰 샘플링 방식을 제어, 단어 선택 확률을 조정해서 답변을 좀 더 딱딱하게 혹은 자유롭게 만듬
- 