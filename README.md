### 2024-07 업데이트 요약

#### 업데이트 1: 입력 벡터 정규화
- **위치:** SoftRenderer::Update2D 함수.
- **설명:** 
  - GetNormalize 함수를 사용하여 입력 벡터를 정규화하는 로직을 추가.
  - 이를 통해 입력 방향이 입력 크기에 관계없이 일관되게 유지됨.

- **코드:**
```cpp
    // 입력 벡터 정규화
    Vector2 inputVector = Vector2(input.GetAxis(InputAxis::XAxis), input.GetAxis(InputAxis::YAxis)).GetNormalize();
    Vector2 deltaPosition = inputVector * moveSpeed * InDeltaSeconds;
```

#### 업데이트 2: 원 그리기
- **위치:** SoftRenderer::Render2D 함수.
- **설명:** 
  - 화면에 원을 그리는 로직을 추가.
  - 원의 반지름은 50 단위로 고정.
  - 원의 중심을 currentPosition으로 설정.
  - 원의 좌표를 계산한 후, 이 좌표를 사용하여 원을 그림.

- **코드:**
```cpp
    // 원 그리기
    static float radius = 50.f; // 원의 반지름
    static std::vector<Vector2> circles; // 원의 좌표를 저장할 벡터

    if (circles.empty()) // 원의 좌표를 계산하지 않은 경우
    {
        for (float x = -radius; x <= radius; ++x) 
        {
            for (float y = -radius; y <= radius; ++y)
            {
                Vector2 pointToTest = Vector2(x, y);
                float squaredLength = pointToTest.SizeSquared();
                if (squaredLength <= radius * radius)
                {
                    circles.push_back(Vector2(x, y));
                }
            }
        }
    }

    for (auto const& v : circles)
    {
        r.DrawPoint(currentPosition + v, LinearColor::Red);
    }
```